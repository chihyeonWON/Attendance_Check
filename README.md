# Attendance_Check 출석체크 앱 프로젝트

```
개발 툴 : Flutter
개발 언어 : Dart
개발 일시 : 2023-02-09 ~
개발자 : Won Chi Hyeon
```

## 앱 개요
```
기능 : 구글 지도를 활용해서 지도 UI를 구현합니다.
       현재 위치로 이동 버튼을 눌러서 GPS 상의 현재 위치로 이동합니다.
       출근 가능한 위치로 이동하면 [출근하기] 버튼을 눌러서 출근 체크를 할 수 있습니다.
       출근 가능한 위치가 아니라면 [출근하기] 버튼은 보이지 않습니다.
       
사용한 플러그인 : google_maps_flutter, geolocator
```

## 구글 지도 API 발급받기
```
구글 클라우드 사이트에서 프로젝트를 만들고 API를 받는 과정은 전에 google_maps 라이브러리 사용을 학습하면서
한번 경험한 적이 있기에 API 발급받는 과정은 쉽게 해결할 수 있었습니다.
Maps SDK for Android, iOS 모두 사용하고 API를 1개 발급받았습니다.
```
![image](https://user-images.githubusercontent.com/58906858/217715999-37c18b5e-4dc0-400d-9858-7d568b25a1b0.png)   
![image](https://user-images.githubusercontent.com/58906858/217716053-a084640b-c995-4a50-8fd1-a8c8f398c5f5.png)

## 필요한 라이브러리 설치
```
flutter pub add google_maps_flutter, flutter pub add geolocator 명령어로 필요한 라이브러리를 설치하였습니다.
google_maps_flutter와 geolocator의 최신 플러그인을 설치하였습니다.
```
![image](https://user-images.githubusercontent.com/58906858/217716324-6cc260b1-6514-4946-a5a0-e1162747a8a1.png)

## 네이티브 코드 설정하기(Android, iOS)
[google_maps_flutter 개발문서](https://pub.dev/packages/google_maps_flutter)
```
먼저 안드로이드 관련 설정입니다. compileSdkVersion을 33으로 minSdkVersion 20으로 수정합니다.

AndroidManifest.xml 파일에 상세 위치 권한과 manifest 태그의 apllication 태그 안에 발급받은 API 키를 등록해주어야 합니다.

발급받은 API키는 실제 프로젝트에서는 노출되면 보안에 위협이 될 수 있습니다. 하지만 연습하는 프로젝트이기에 그냥 올려두었습니다.

다음은 iOS 관련 설정입니다. ios/Runner/AppDelegate.swift 파일을 열고 구글 API를 넣는 코드를 복사해서 붙여넣습니다.
ios/Runner/Info.plist 파일에 권한 요청 메시지를 추가합니다.

이로써 안드로이드와 iOS의 플러그인을 사용하기 위한 설정은 끝이 났습니다.
```
### [compileSdkVersion, minSdkVersion 수정]
![image](https://user-images.githubusercontent.com/58906858/217716979-ceb8a404-5fd0-4a84-a1a2-a796c1dac736.png)     
![image](https://user-images.githubusercontent.com/58906858/217717008-382a629d-7a52-47a3-a505-8e748db8c501.png)

### [상세 위치 권한 설정]
![image](https://user-images.githubusercontent.com/58906858/217717610-37be3f9e-3bf7-468d-8cf2-65819852e51e.png)

### [Android 구글 API 키 등록]
![image](https://user-images.githubusercontent.com/58906858/217717628-68b55424-b027-49ae-9836-2f91f3de1533.png)

### [iOS 구글 API 키 등록]
![image](https://user-images.githubusercontent.com/58906858/217718537-90b1ad6e-b74e-4b96-8260-81ab0663005d.png)

### [iOS 권한 요청 메시지] 
![image](https://user-images.githubusercontent.com/58906858/217718424-568efd98-8050-49bf-9043-501986980d99.png)

## AppBar 구현하기
```
AppBar는 renderAppBar 함수를 만들어서 구현하였습니다.
흰색 배경색에, 제목은 가운데 정렬, 제목의 폰트사이즈 등을 설정하였습니다.
```
![image](https://user-images.githubusercontent.com/58906858/217996556-89a20ff4-03cd-4cf3-9938-a0fdb50864fb.png)   
![image](https://user-images.githubusercontent.com/58906858/217996598-474ab492-2128-46d4-acda-422ca38a7f32.png)

## 지도 초기화 위치 생성
```
google_maps_flutter 라이브러리를 import 해주고 라이브러리에 들어있는 LatLng 클래스를 사용해서
지도의 초기화 위치를 설정해줍니다. 
위도 37.5233273, 경도 126.921252 의 위치값을 companyLatLng 객체에 저장하였습니다.
```
![image](https://user-images.githubusercontent.com/58906858/217997178-ad94342f-e6c5-4e07-9794-5960c97c31c5.png)      
![image](https://user-images.githubusercontent.com/58906858/217997235-45a9835b-b67c-4c9b-bff4-15f9b9524e14.png)

