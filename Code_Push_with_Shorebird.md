# # Code Push with Shorebird
 [🚀 Getting Started | Shorebird](https://docs.shorebird.dev/) 
### 코드 푸시를 하게 된 계기
* 업데이트 주기가 잦은 잼핏, 근데 업데이트때마다 사용자가 마켓에서 업데이트 버튼을 눌러야 한다면? : 사용자의 이탈로 이어질 우려가 크다. 실제로 이탈하는 경우가 있었다.
* 여기에 더해, 매번 검수를 넣고, 기다려야 하는 문제도 있었다. 검수가 짤리기라도 하면? 그대로 계획엔 차질이 생긴다.
⇒ 더 이상 이렇게는 안 된다! 코드 푸시를 도입하자~!

### 코드 푸시란?
플러터 개발자가 서비스 업데이트를 검수 절차 없이, 온라인으로 할 수 있도록 지원하는 클라우드 서비스.

### Shorebird란?
* 플러터 초기 개발자 중 한 명인 **Eric Seidel**와, 그가 꾸린 팀이 만들고 있는 Flutter 기반의 Code Push 서비스.
* 참고로 Google의 Flutter 팀에서는 당분간 Code Push를 개발할 계획이 없다고 한 만큼, 유일한 Flutter 코드 푸시 서비스라고 보면 된다.

### Shorebird 가격 정책
1. Hobby(공짜) : 1달에 최대 5,000번의 패치 설치 가능. 앱 당 계정 1개만 사용 가능하며, 다른 계정 초대 불가.
2. Team(1달에 **$20**) : 1달에 최대 50,000번의 패치 설치 가능. 다른 개발자 계정을 초대할 수 있음.
3. Enterprise(비용 협의) : 매우 큰 서비스를 대상으로 함. 협의 후 가격 및 지원 범위 산정.
🧮 참고로 1달에 몇 번이나 패치 설치가 이루어지는지는 다음 수식으로 계산해보실 수 있습니다.
**(1달에 발생하는 최대 패치 설치 횟수) = (MAU) X (1달에 이루어지는 업데이트 횟수)**
ex) 만약 1달에 방문하는 유저 수가 140명이고, 매달 2번에 패치가 올라간다면, (해당 달에 발생한 패치 설치 횟수) = 140 * 2 = 280(번) 입니다.


# Shorebird, 설치부터 첫 적용까지
1  [https://console.shorebird.dev/login](https://console.shorebird.dev/login)  에 들어가서 계정을 만듭니다.
2 로그인하고, 약관에 동의하면, 아래와 같은 화면이 나옵니다. 절차에 맞게 쭈욱~ 따라가시면 됩니다. 다만 이렇게만 해두고 설치 부분을 끝내면 심심하니, 현재(2023.11.20) 기준 설치법을 아래에 적겠습니다.
3 Shorebird CLI를 설치합니다. 터미널을 열고, 아래 명령어를 입력합니다.
	* **MacOS/Linux**
`curl —proto ‘=https’ —tlsv1.2 <https://raw.githubusercontent.com/shorebirdtech/install/main/install.sh> -sSf | bash` 
	* **Windows** (PowerShell에서 실행)
`Set-ExecutionPolicy RemoteSigned -scope CurrentUser # Needed to execute remote scripts`
`iwr -UseBasicParsing ‘<https://raw.githubusercontent.com/shorebirdtech/install/main/install.ps1'|iex>`

4 로그인합니다.
`shorebird login`
5 Shorebird를 적용할 Flutter 프로젝트로 가서, init 명령어를 실행합니다.
`shorebird init`
실행 후, 프로젝트 폴더 내부에 shorebird.yaml 파일이 생겼다면 성공!
	* 위 명령어 실행 시, 안드로이드 프로젝트에 INTERNET permission이 없다면 자동으로 추가됩니다. 만약 자동으로 추가가 되지 않는다면, android_app_src_main_AndroidManifest.xml에 INTERNET uses-permission을 아래처럼 넣으시면 됩니다.
`<manifest …>`
`<uses-permission android:name=“android.permission.INTERNET” />`
`…`
`</manifest>`
	* 중간에 아래와 같은 메세지가 나올 수 있습니다. 이 경우, 플러터 버전이 맞지 않는 것이니 플러터를 최신 버전으로 올릴 것을 권장드립니다! (Shorebird 공식 문서에 따르면, Flutter 최신 버전에서는 잘 동작하지만, Flutter 이전 버전에서는 오류가 발생할 수 있다고 합니다. 따라서 Flutter 버전을 올린 후 Shorebird를 사용할 것을 권장하고 있습니다.) 참고로 Flutter 최신 버전으로 올리는 명령어는 `flutter upgrade` 입니다.
`✗ Flutter install is correct (0.0s)`
` [!] The version of Flutter that Shorebird includes and the Flutter on your path are different.`

6 첫 release 버전을 만듭니다. 명령어는 아래와 같습니다.
`shorebird release android`
