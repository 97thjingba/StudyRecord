
两个组件配合起来用.可以达到微信发送语音的功能  
[https://github.com/jsierles/react-native-audio](https://github.com/jsierles/react-native-audio)

[https://github.com/zmxv/react-native-sound](https://github.com/zmxv/react-native-sound)

一个已经封装好的 录制，停止，发送的 model 类

```js
import { Alert } from  'react-native';
import  RNFS  from  'react-native-fs';
import { AudioRecorder } from  'react-native-audio';
import  Sound  from  'react-native-sound';
import  BaseApi  from  '../../../api/BaseApi';
import  ApiConfig  from  '../../../api/ApiConfig';
import  UserModel  from  '../../../model/user/UserModel';
import  ApiHeaderFactory  from  '../../../api/ApiHeaderFactory';
export  default  class  AudioModel  extends  BaseApi {

// 为录制声音进行必要的初始化
constructor() {
super();
this.initialForRecord();
}

initialForRecord() {
this.currentTime = 0.0;
this.recording = false;
this.paused = false;
this.didSucceed = false;
this.audioPath = `${RNFS.DocumentDirectoryPath}/texas_hold_em_message.aac`;
this.hasPermission = undefined;
this.isSend = false;
this.roomId = undefined;
	AudioRecorder.onProgress = (data) => {
	this.currentTime = Math.floor(data.currentTime);
	console.log('currentMetering', data.currentMetering, data.currentPeakMetering);
	};

	AudioRecorder.onFinished = async (data) => {
	try {
	await  this._finishRecording(data.status === 'OK', data.audioFileURL, data.audioFileSize, data.base64);
	} catch (error) {
	console.log(error);
	}
	};
}

async  checkPermission() {
const  isAuthorised = await  AudioRecorder.requestAuthorization();
this.hasPermission = isAuthorised;
return  isAuthorised;
}

prepareRecordingPath = (audioPath) => {
AudioRecorder.prepareRecordingAtPath(audioPath, {
SampleRate:  22050,
Channels:  1,
AudioQuality:  'Low',
AudioEncoding:  'aac',
AudioEncodingBitRate:  32000,
IncludeBase64:  true,
MeteringEnabled:  true,
});
};

async  record() {
	if (this.recording) {
	return;
	}
	if (!this.hasPermission) {
	return;
	}
	this.prepareRecordingPath(this.audioPath);
	this.isSend = false;
	this.recording = true;
	this.paused = false;
	await  AudioRecorder.startRecording();
}

  

async  stop() {
	if (!this.recording) {
	return;
	}
	this.recording = false;
	this.paused = false;
	await  AudioRecorder.stopRecording();
}

async  playAudio(fileData: string) {
try {
	const  path = await  this._convertBase64ToFile(fileData);
	// 第二个参数不能填写, 填写之后无法读取
	const  sound = new  Sound(path, '', (error) => {
	if (error) {
	console.log(error);
	return;
	}
	sound.play((success) => {
	if (success) {
	console.log('play sound success');
	} else {
	console.log('play sound failed!!!');
	}
	});
	});
	} catch (error) {
	console.log(error);
	}
}

  

_convertBase64ToFile = async (fileData: string) => {
	const  path = `
	${RNFS.DocumentDirectoryPath}/${new	Date().valueOf()}_texas_hold_em`;
	await  RNFS.writeFile(path, fileData, 'base64');
	return  path;
};

async  _finishRecording(didSucceed, filePath, fileSize, fileData) {
	this.didSucceed = didSucceed;
	this.playAudio(fileData);
}
}

}

}

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY1Mjg5NTczOF19
-->