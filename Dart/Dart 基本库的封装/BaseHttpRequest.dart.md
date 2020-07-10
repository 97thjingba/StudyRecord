```dart
import  'dart:convert';
import  'dart:io';
import  'package:dio/dio.dart';

class  HttpRequest {
	static  getRequest(url) async {
try {
	Response response = await  Dio().get(url);
	return response;
} catch (error) {
print(error);
}
}

  

static  postRequest(url, data, accessToken) async {
try {
	Response response = await  Dio().post(url,
	data: data,
	options: Options(headers: {'authorization': 'Bearer $accessToken'}));
	return response;
} catch (error) {
print(error);
}

}

  

static  putRequest(url, data, accessToken) async {

try {

Response response = await  Dio().post(url,

data: data,

options: Options(headers: {'authorization': 'Bearer $accessToken'}));

return response;

} catch (error) {

print(error);

}

}

  

static  deleteRequest(url) async {

// 待封装

try {

Response response = await  Dio().delete(url);

return response;

} catch (error) {

print(error);

}

}

  

static  patchRequest(url) async {

// 待封装

try {

Response response = await  Dio().get(url);

return response;

} catch (error) {

print(error);

}

}

}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk3MjI2MTAyNl19
-->