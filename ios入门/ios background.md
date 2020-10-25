下面说一下background modes  
最近开发的时候在 background modes 遇到的一些问题先简单街道一个background modes

iOS 后台运行的规则

应用的运行状态分为以下五种：

**Not running**：应用还没有启动，或者应用正在运行但是途中被系统停止。

**Inactive**：当前应用正在前台运行，但是并不接收事件（当前或许正在执行其它代码）。一般每当应用要从一个状态切换到另一个不同的状态时，中途过渡会短暂停留在此状态。唯一在此状态停留时间比较长的情况是：当用户锁屏时，或者系统提示用户去响应某些（诸如电话来电、有未读短信等）事件的时候。

**Active**：当前应用正在前台运行，并且接收事件。这是应用正在前台运行时所处的正常状态

**Suspended**：应用处在后台，并且已停止执行代码。系统自动的将应用移入此状态，且在此举之前不会对应用做任何通知。当处在此状态时，应用依然驻留内存但不执行任何程序代码。当系统发生低内存告警时，系统将会将处于 Suspended 状态的应用清除出内存以为正在前台运行的应用提供足够的内存。

**Background**：应用处在后台，并且还在执行代码。一般的应用，都只会在这个状态短暂停留（最多十分钟），然后就会被系统强制进入 Suspended 状态。而 iOS 为了在某些情况下提供更好的体验，提供了一些选项，只要满足这些选项的条件，就可以在后台运行很长的一段时间，下面我们将重点讨论可以使应用在后台长时间运行的方法。  

![](//upload-images.jianshu.io/upload_images/2460743-bdf0e4549f804e6c.png?imageMogr2/auto-orient/strip|imageView2/2/w/368/format/webp)

iOS 应用状态切换示意图.png

**iOS 提供的后台运行方式**  

![](//upload-images.jianshu.io/upload_images/2460743-9d38ad164fc5dc6a.png?imageMogr2/auto-orient/strip|imageView2/2/w/996/format/webp)

iOS 提供的后台运行方式列表.png

上图为 iOS 提供的后台运行方式列表，如果需要，可在 Xcode 的项目设置中开启对应的选项。App Store 的审核人员会检查应用中是否有必要开启该后台运行模式选项，如果应用中不需要，而又开启了这个选项，可能会被拒.

网址:[https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/BackgroundExecution/BackgroundExecution.html](https://link.jianshu.com?t=https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/BackgroundExecution/BackgroundExecution.html)

**Audio, AirPlay and Picture in Picture**  
此个选项包含四种场景，分别是：音频的播放，录音，AirPlay 及画中画的视频播放。

**音频的播放**：在播放音频时，即使应用退到后台，只要一直有音频在播放，那应用就可以一直在后台运行。代码实现可参考：[http://www.jianshu.com/p/348e0f9ffde9](https://www.jianshu.com/p/348e0f9ffde9)

** Audio**：应用可以请求使用麦克风，而当开启了此后台选项，应用在使用麦克风的时候，即使退到后台，也可以一直后台运行，通过查看微信安装包中的 plist 文件，微信的语音聊天，就是通过这种方式实现的。而当该类应用退到后台后，iOS 系统的状态栏会变成红色，并在状态栏中显示正在使用麦克风的应用的名称，如下图所示。

  

![](//upload-images.jianshu.io/upload_images/2460743-4710f7ffdd55852f.png?imageMogr2/auto-orient/strip|imageView2/2/w/370/format/webp)

正在使用麦克风提示.png

**AirPlay**：AirPlay 是指将 iOS 设备，或者 Mac 设备上的音视频，同步到另一个设备中播放。举两个例子，第一个是把 iPhone 上的音乐通过蓝牙的方式在汽车的蓝牙音响播放，第二个是把 iPhone 上的视频，同步到智能电视屏幕上播放。此功能一般用于多端及多屏的交互。  
关于 AirPlay 的开发文档：[http://nto.github.io/AirPlay.html](https://link.jianshu.com?t=http://nto.github.io/AirPlay.html)

**Picture in Picture**：画中画是 iPad 版本的 iOS 9 新增加的功能，可以在 iOS 的桌面，或者其他应用的界面的上面播放视频，从而该视频区域所属的应用就可以后台运行了。**此功能现在只在 iPad 应用中提供**。  
代码实现可参考：[http://www.jianshu.com/p/27ce4ada48da](https://www.jianshu.com/p/27ce4ada48da)

**Location updates**  
一般用于导航应用中，开启此选项后，应用退到后台，还可以得到系统的定位更新，从而使得应用可以根据定位的变化做出不同的反应。  
代码实现可参考：[https://github.com/W-King/Location](https://link.jianshu.com?t=https://github.com/W-King/Location)

**Voice over IP**  
VOIP 类的应用允许用户使用网络而不是手机打电话，因此这一类的应用需要保持同它相关的服务的网络连接，用以收到来电事件和其他数据。iOS 不是通过一直让该应用处于激活状态来达到这个目的，而是**同样也会将这类的应用挂起**，但同时会在应用被挂起期间**由系统接管它的 VOIP 的 Socket**，**当这个 Socket 有数据通信时**，**系统会再次唤醒处于挂起状态的应用**，同时将 Socket 的控制权交还给该应用，以让其正常的处理来电事件和其他数据。

**Newsstand downloads**  
在 iOS 开发中，有一类叫报刊杂志类应用比较特别，在 iOS 9 之前的系统中，此类应用会统一收在系统内置的「报刊杂志」应用中，在 iOS 9 中则去掉了内置的「报刊杂志」应用，此类应用得以以单独的图标入口出现在桌面中。此后台运行的选项就是提供给报刊杂志类应用可以在后台下载及处理报刊杂志内容，而下载的过程需要使用 NewsstandKit 中的 NKAssetDownload 进行下载。需要注意的是，**下载的过程中**，**应用可能还是会被挂起**，**甚至应用被退出**，而 iOS 会在 Wi-Fi 环境下继续下载，直到下载完成。而一旦下载完成，**如果应用只是被挂起**，则** iOS 会唤醒对应的应用**，回调对应的事件；**如果应用已经退出**，**则会启动应用**，在启动参数中会带上对应的标识表示这次启动是因为下载报刊杂志内容完成。  
代码实现可参考：[http://www.viggiosoft.com/blog/blog/2011/10/17/ios-newsstand-tutorial/](https://link.jianshu.com?t=http://www.viggiosoft.com/blog/blog/2011/10/17/ios-newsstand-tutorial/)

**External Accessory communication**  
此选项提供给一些 MFi 外设通过蓝牙，或者 Lightning 接头等方式与 iOS 设备连接，从而可在外设发送消息时，唤醒已经被挂起的应用。而一旦被唤醒，一般情况下， 应用只有最多 10 秒钟的执行时间。MFi 外设：是指通过苹果 MFi 认证的设备，而 MFi 认证是对其授权配件厂商生产的外置配件的一种标识使用许可，是 Made for iOS 的英文缩写。

**Uses Bluetooth LE accessories**  
此选项与 External Accessory communication 类似，只是此选项无需限制 MFi 外设，而需要的是 Bluetooth LE 设备。

**Acts as a Bluetooth LE accessory**  
此选项是指 iOS 设备作为一个蓝牙外设连接时，对应的应用可以后台运行，但是使用此模式需要用户进行授权认证。

**Background fetch**  
iOS 7 新增加的一个选项，用于即使在后台，也需要频繁更新数据的应用。例如一个 PM2.5 的应用，需要几个小时更新一次数据，那么可以开启此选项，设置一个时间间隔，从而让 iOS 在间隔时间内在后台启动该应用，执行指定数据的获取工作，而此过程最多只能执行 30 秒钟。  
代码实现可参考：[http://www.jianshu.com/p/82f639012f3e](https://www.jianshu.com/p/82f639012f3e)

**Remote notifications**  
iOS 7 新增加的一个选项，是一种静默推送，它有别于一般的推送，应用收到此类推送后，不会有任何的界面提示，而当应用退出或者挂起时收到此类推送，iOS 也会启动或者唤醒对应的应用。例如一个阅读应用，用户订阅的博客更新了，那么可以先发一个静默推送，应用收到此种推送后，可以先把用户订阅的博客内容都下载好，再通知用户，这样用户一打开应用就可以马上开始阅读。收到静默推送，会回调对应的回调方法，而此回调方法最多只能执行 30 秒钟。  
代码实现可参考：[http://www.jianshu.com/p/82f639012f3e](https://www.jianshu.com/p/82f639012f3e)

**基于 NSURLSession 的后台传输**  
此为 iOS 7 新增加的特性，用于在后台下载或者上传大文件，步骤如下：创建后台传输用的 NSURLSession 对象；向这个对象中加入对应的传输的 NSURLSessionTask，并开始传输；在实现 AppDelegate 里实现 -application:handleEventsForBackgroundURLSession:completionHandler: 方法，以刷新 UI 及通知系统传输结束。一旦后台传输的状态发生变化（包括正常结束和失败）的时候，应用将被唤醒并运行 AppDelegate 中的回调。但是也有一些限制，后台传输只会通过 Wi-Fi 来进行。后台下载的时间与以前的关闭应用后X分钟的模式不一样，而是为了节省电力变为离散式的下载。  
代码实现可以参考：[http://onevcat.com/2013/08/ios7-background-multitask/](https://link.jianshu.com?t=http://onevcat.com/2013/08/ios7-background-multitask/)

**其他后台运行黑魔法**

**一直循环播放一段没声音的音频**  
可以在后台选项中选择「Audio, AirPlay and Picture in Picture」，而开始循环播放一段是没声音的音频，即在 Audio Unit 回调函数中使用 kAudioUnitRenderAction_OutputIsSilence 标志位，但是这种方式两个大的缺点：

1.  苹果的审核人员如果发现，会被拒；
2.  应用程序的 Audio Session 不能被打断。当应用执行在后台时，只要另一个应用使用 kAudioSessionCategory_RecordAndPlay （比如 Skype）或者 kAudioSessionCategory_SoloAmbientSound，那么该应用就会被立即打断。  
    代码实现可参考：[https://github.com/marcop/MMPDeepSleepPreventer](https://link.jianshu.com?t=https://github.com/marcop/MMPDeepSleepPreventer)

**越狱下开发 System 级别的应用**  
一般的应用都是 Mobile 级别的，在越狱的情况下，可以开发一个 System 级别的应用，从而使得应用不受 iOS 一般应用的限制，实现真正的后台运行，但是缺点就是应用只能运行在越狱设备上，也不能上 App Store。  
代码实现可参考：[http://www.jianshu.com/p/50b7b27ba828](https://www.jianshu.com/p/50b7b27ba828l)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5OTcxNDMxOTNdfQ==
-->