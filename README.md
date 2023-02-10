# Attendance_Check 오늘도 출근 앱 프로젝트

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

## body에 지도 구현하기
```
GoogleMap 위젯을 사용해서 구글 지도를 body에 나타내었습니다.
initialCameraPosition 필수 매개변수에는 CameraPosition 클래스를 입력해주고 필수 정보인 target에는 
위에서 설정한 LatLng 위치정보를 zoom에는 확대 정도 값을 double타입으로 지정합니다.

정상적으로 초기 위치정보(37.5233273, 126.921252)를 보여주는 구글 지도가 화면에 나타납니다.
```
![image](https://user-images.githubusercontent.com/58906858/217998071-b1d486b5-56e9-4894-9f16-31d4a4e5e484.png)         
![image](https://user-images.githubusercontent.com/58906858/217998136-55e51ee3-0221-416b-acf5-e15a9ec011eb.png)      
![image](https://user-images.githubusercontent.com/58906858/217998320-bcde9ada-e4c1-44bb-a1a9-e22e1d72a273.png)   
![image](https://user-images.githubusercontent.com/58906858/217998513-b7d4fdab-7039-464a-9a57-f5fde60e38c0.png)

## Footer에 시계아이콘, 버튼 구현하기
```
body의 구글 지도가 차지하는 공간을 Expanded로 감싸고 flex 2 (전체의 2/3)을 주고 전체를 Column으로 감싸줍니다.
남은 1/3의 공간에 시계 아이콘과 출근하기 버튼을 생성하였습니다.
```
![image](https://user-images.githubusercontent.com/58906858/217999503-7e2ce257-c5e0-4e1d-af5e-6ed58237e636.png)   
![image](https://user-images.githubusercontent.com/58906858/217999531-541553a9-0d9b-4d75-9b3b-e9c0fea42863.png)

## GPS 위치 권한 관리하기
```
GPS 위치 권한을 확인하고 앱에서 위치 서비스를 사용할 수 있는지 확인한 후 위치 권한을 사용할 수 없는 상태면 권한을 재요청하는 로직을
구현하였습니다. 위치권한 사용을 위해서 geolocator 라이브러리를 사용합니다.
앱마다 모두 권한을 처리하는 방식이 다릅니다. 이번에는 위치 권한이 없으면 앱을 일부 기능이 아닌 전체 기능을 사용할 수 없다는 가정하에 만들었습니다.

권한이 허가되면 위치 권한이 허가되었습니다. 라는 String 값을 반환하고 아니라면 문제되는 사항에 대한 정보가 담긴 String 값을 반환하는
String Future 타입의 checkPermission 함수를 구현하였습니다.
```
![image](https://user-images.githubusercontent.com/58906858/218001144-9635146d-773b-443b-bb9a-9c3ea4501581.png)


## checkPermission 함수의 값에 따라 변경되는 UI
```
checkPermission의 리턴값에 따라 권한 유무를 알 수 있고 권한 유무에 따라 다른 ui를 보여주기 위해서
FutureBuilder 를 사용하였습니다. 전에 웹툰 앱 프로젝트를 하면서 FutureBuilder의 사용법은 알고 있었습니다.

로딩상태(hasData == null 이거나 connectionState가 waiting 일때) 로딩 위젯을 보여주고
위치 권한이 허가되었습니다.라는 String 값이 넘어오면 Column의 위젯들을 보여주고
그외 (위치 권한이 거절되거나 앱에서 권한 설정이 거부되었을 때) 해당하는 문구를 보여줍니다.
```
### [앱을 켰을 때 위치 권한 사을 사용자에게 요청하는 화면]
![image](https://user-images.githubusercontent.com/58906858/218002965-b5b2862e-1e43-46e3-a16a-401b691a89ff.png)

### [위치 권한을 거부하였을 때의 화면]
![image](https://user-images.githubusercontent.com/58906858/218003087-1283cafa-9e56-4013-8612-c2bd776cbb21.png)

### [앱 사용중에만 허용, 이번만 허용을 했을 때의 화면]
![image](https://user-images.githubusercontent.com/58906858/218003470-87e12fb3-aacc-4aa7-832d-a61d4cc466dc.png)
