# Work & Development Environment

## 1. 업무 관련 정리 사항

- 업무시간 : 9시~6시- 수습기간 : 3개월
- 담당업무 : 슈퍼조인 프론트엔드, 백엔드 로직(앱의 주요기능들은 구현되어 있는 상황으로 주로 유지보수 위주로 진행 예정)
- 이용 프로그래밍 언어 : 자바스크립트
- 서버 관련 사항 : 파이어베이스(주언어 : 타입스크립트)에서 이관 진행 중
  (1.파이어베이스 외 다른 서버 이용 / 2.백엔드 로직 구현 중에 이뤄질 것이며 1.다른 서버 이용 예정일 것)
- 공유 사항 : 개인블로그/노션 혹은 지라에 공유 가능
- 재플린 이용 방법
  - 현재 재플린에는 개선 중인 화면 확인 가능
  - 아이콘 모인 탭에서 기존 아이콘, 신규 아이콘 확인, svg 파일 다운로드 가능
  - 신규 아이콘 적용 방법
    1. 슈퍼조인 프로젝트>resources/icon 폴더 이동
    2. 제목에 붙은 ic- 빼고 저장하기
    3. 기존 아이콘 svg 파일 참고해서 색상 변경해야함(#00000~으로 변경, 이렇게 지정해야 소스에서 색변경이 가능)(superjoin으로 감싸는 것까지 따라서 해도 괜찮은데 그 이후 그룹으로 감싸는 부분은 안해줘도 됨!)
    4. 프로젝트>shared>icon>basic.js 파일에 추가한 아이콘 리소스 import 후, export 설정
    5. 사용하려는 소스에서는 touchable opacity 안에 넣어서 사용(fill 프로퍼티를 이용해 color 사용)
    6. 아이콘 업로드에 이상 발생하면 수연님께 말씀드리기
- git repo 이름 규칙
  - 영문 이니셜 3글자/업무성격/변경화면 이런 식으로 repo 따기
  - 업무성격
    - f : feature, 기능 구현
    - b : 버그픽스

## 2. 개발 환경 관련 정리 사항

- IDE : VS Code
- 협업툴 : 슬랙(업무연락), 지라(todo 관리)
- 디자인툴 : 재플린- 기획툴 : 피그마
- 형상관리 : github
- 개발 환경 세팅
  1.  Iterms(Iterm2) 설치 : 맥에서 제공하는 기본 터미널 대신 사용
  2.  기본 shell bash -> zsh로 변경
  3.  oh my zsh 설치 (https://velog.io/@xedni/I-Term-%EB%82%B4-%ED%84%B0%EB%AF%B8%EB%84%90-%EC%98%88%EC%81%98%EA%B2%8C-%EA%BE%B8%EB%AF%B8%EA%B8%B0 ) -> iterms 화면 꾸미기
  4.  Mac OS 패키지 관리자 Homebrew 설치(https://brew.sh/index_ko)
  - 일반 설치 : brew install + 패키지명
  - 런치패드 자동 등록 + 설치 : brew install —cask + 패키지명
  - 설치된 패키지 확인 : brew list로 확인
  5.  iterm2 커맨드 환경에서 homebrew 이용하여 vscode 설치: brew install -- cask visual-studio-code6)
  6.  openjdk 11버전 설치
  - brew tap adoptopenjdk/openjdk
  - brew search idk
  7.  node 버전 관리자 설치(nvm)
  - brew install nvm
  - nvm list
  - nvm install 12( node 12.22.11 버전 확인 후 설치)
  8.  Xcode(앱스토어에서 설치), 안드로이드 스튜디오 설치(https://developer.android.com/studio?gclid=CjwKCAjwrqqSBhBbEiwAlQeqGn7_cEpbWyyVvOF43CMgxNEakbbNdgsrZ5WJrrS_TdSx3oZ_Tyr1bBoCdeUQAvD_BwE&gclsrc=aw.ds)
  9.  노드 프로젝트 설치시 노트 패키지 매니저 이용하여 설치해도 되나 yarn 패키지 매니저 이용 권장(npm과 비교하여 설치가 빠르고, 서버가 안정적, dependency 관리가 편리(dependency 충돌 이슈가 적음)
  10. yarn 설치
  - nvm install --global yarn
  - global 붙이는 경우 프로젝트 단위가 아니라 pc 단위로 yarn 가능해짐
  - yarn에서 관리하는 패키지 확인시 package.json, index.js 통해 확인/관리 가능
  - yarn 설치시 이슈 발생 : 프로젝트에 git config 파일 생성, GitHub 계정에 ssh 추가 확인
  11. 노드 프로젝트에서 설치된 패키지는 node-modules 폴더에서 확인 가능
  12. 리액트 네이티브 프로젝트인 경우 플젝 안에 iOS/android 폴더 구성되어 있음(각각이 네이티브 프로젝트 구성)
  13. cocoapods (iOS 전용 패키지 매니저) 설치
  - brew install cocoapods
  - pod 명령어 이용
  - pod file은 yarn의 package.json과 유사
  14. iOS 전용 패키지 설치
  - iOS 프로젝트 안에서 pod install
  15. xcode에 Apple 계정 등록 및 슈퍼조인 팀 계정 초대 확인
  16. iOS 프로젝트 빌드 및 실행
  - yarn iOS (yarn run v1.22.18)
  - peeps.xcworksapce : 실행 파일
  - peeps.xcodeproj : 설정 파일
  - 개발서버 빌드 시 metro가 뜨며 javascript 코드 실행 (로그도 메트로 실행 화면에서 뜸)
  - 안드보다 ios가 더 빨라 로컬 테스트시 iOS 이용(개발서버 로그인 번호 : 166666666)
  17. 안드로이드는 별도 패키지 매니저 설치 x gradle 빌드 후 실행 가능
  18. zshrc 파일(Mac os에서 사용하는 경로/설정 등에 대해 관리)에 android_home 경로 설정(sdk, emulator 경로 등 설정)
  ```
  # Android studioexport ANDROID_HOME=/Users/bggong/Library/Android/sdkexport PATH=$PATH:$ANDROID_HOMEexport PATH=$PATH:$ANDROID_HOME/emulatorexport PATH=$PATH:$ANDROID_HOME/toolsexport PATH=$PATH:$ANDROID_HOME/tools/binexport PATH=$PATH:$ANDROID_HOME/platform-tools
  ```
  19. android 프로젝트 빌드 및 실행
  - npx reactive-native run-android
  - yarn android (package.json script에 약어 설정되어 있음)
  20. web 개발 환경 설정
  - react를 next js로 감싼 구조
  - git clone 하여 프로젝트 받아오기
  21. web 환경 빌드 및 배포
  - yarn dev (로컬 빌드)
  - yarn build (개발 후 서버에 올릴 때 사용 html javascript 올림. Product 모드로 로컬에서 빌드
  - yarn start (로컬 build 후 로컬에서 시작)
  - yarn deploy (호스트 서버에 배포. 로컬에 있는 빌드/export 된 out > index.html -> firebase 웹서버에 배포)
  - yarn export : nextjs로 빌드된 결과를 static html로 쪼개주어 웹서버 세팅이 어려운 Firebase에 배포할 수 있는 상태로 변환해주는 명령어
  - yarn lint (코드 검사)
  - 웹서버(파이어베이스) 배포 전 배포를 위한 파이어베이스 cli 환경 설치 필요
  - yarn global add firebase-tools
  - firebase login : yarn deploy 전에 cli 환경에서 firebase 계정 연동
  - yarn dev 로 테스트 > yarn lint > yarn build > yarn start > yarn export > yarn deploy 순으로 진행

## 3. 개발 방법 및 환경 관련 정리 사항

1. Xcode

   - 맥에 깔리는 프로그램 만들때 사용. ios는 xcode에서만 개발 가능

2. ios 환경
   - xcworkspace : ios 워크스페이스
   - ios>peeps : 메인 프로젝트 소스 확인 가능
   - ios>pods : xcode, ios 관련 라이브러리 관리. 이용 중인 라이브러리 확인 가능
   - ios>podfile : 라이브러리에 대한 선언(pom.xml, gradle.config 비슷한거로 보면 될것 같음)
   - podfile에 정의되지 않은 라이브러리 : node_modules>라이브러리폴더>podfile 이 쪽에 정의되어 있음
   - 외부 라이브러리 사용시 installation 방법 확인 필요
     - 프로젝트 podfile에 직접 명시, 설치 필요한 경우 있음
     - yarn add 라이브러리 + pod install로 설치 가능한 경우 있음
   - podfile 상세
     - react-native-permission : 리액트 네이티브에서 제공해주는 앱 권한 관련 모듈 사용 가능한 라입브러리
     - 필요한 권한에 대해서만 podfil에 명시 : permission은 직접 명시 필요
     - pods 폴더는 수정x, podfile 정도만 수정한다고 보면 될듯
   - peep.xcodeproj : xcode 프로젝트 설정 파일
   - xcode workspace로 프로젝트 여는게 좋음(xcodeproj로 열면 꼬일 수 있음)
   - peeps-bridging-header
     - 리액트 네이티브는 당시에 많이 쓰인 objective-c로 작성됨. 현재는 swift 많이 사용 중. objective-c , swift 코드의 연결을 가능하게 해주는 파일로 보면 됨
     - 해당 파일에 헤더 파일을 명시해 사용 가능(ios는 파일 하나가 header, main으로 나뉜 것 같음)
   - peeps>main : 자바의 main 메소드와 동일. 앱 실행의 시작점
   - peeps>launch screen : 앱이 맨 처음에 켜질때 스크린 수정 가능
     - ios에서는 코드가 본격적으로 실행하기 전에 무조건 lauch screen 띄우고 있음, 자바스크립트로 작성이 불가하여 xcode + objective-c로 코딩 필요
     - lauch screen이 종료되면 작성한 자바스크립트 코드 동작이 시작됨
   - peeps>AppDelegate
     - 자바스크립트 코드를 읽어와 ios에 적용해주는 파일
     - react native 프로젝트 생성시 기본으로 만들어지는 파일
     - didfinish launch with ption : 런치 이후 설정 가능
     - init with delegate : 자바스크립트 코드 실행을 위한 로직 시작점
     - 관련 동작 원리 확인해보면 좋을듯
     - pod에서 설치한 리액트 네이티브 관련 코드 중 네이티브 소스 수정이 필요한 패키지들이 있음
       - appdelegate 파일에서 관련 내용 추가가 가능
     - js 코드로 작성이 가능하도록 appdelegate에 관련 내용 작성해줄 수 있음
3. 슈퍼조인 관리자 접속 방법

   - 016666666 /123456 으로 접속

4. 슈퍼조인 프로젝트 구조

   - index.js
     - 프로젝트의 시작점. 그 이후 app.js 실행
     - 모달 : 사용자 작업을 방해하는 요소. 팝업/광고 등
     - index.js 안에 있는 모달 요소
       - 앱 업데이트 버전 체크, 업데이트 팝업 모달. app.js와 같은 레이어에 위치. 업데이트 관련 app.js 밖에서 상위나 동일 레이어에 위치해야 함
     - appearanceprovider : 앱 라이트/다크 모드와 같은 테마 정보를 갖고 있어, 하위 요소은 app, modal에 앱 테마 정보 전달해줄 수 있는 역할 수행
     - paperprovider : 리액트 페이퍼 패키지 관련 정보 전달해주는 역할
     - persistgate
       - provider의 프로퍼티인 리덕스 스토어 정보 중 앱 내부 로컬 스토리지에 영구히 저장되면 좋을 것 같은 state 관리를 위해 사용하는 요소
     - provider
       - 부모의 state는 하위 컴포넌트의 프로퍼티가 되고 있음
       - 자식의 state는 부모에서 사용이 어려움 > 이에 대한 해결책으로 state 관리 프레임워크 리덕스 사용
       - 리덕스로 state의 글로벌한 사용이 가능
       - 리적스 store는 root 요소에서 관리 필요 > 이 때 provider 이용, index.js 최상단 요소인 provider에서 설정
   - app.js
     - safeareaprovider
       - 아이폰 노치, 핸드폰 기종마다 화면구성이 다름 > 이를 위한 제한 영역 관리 설정 가능
     - 내비게이션 컨테이너
       - 내비게이션을 이용하기 위해 감싸주는 내비게이션 컨테이너 요소
     - rootstacknavigator
       - 모바일은 화면이 스택처럼 쌓이는 개념
       - 리액트 라우터처럼 리액트 네이티브에서는 내비게이션을 이용해 화면 전환 진행
       - 실제 화면이 시작되는 시작점으로 봐도 좋을 듯
   - components
     - navigations
       - 내비게이션 파일들 저장. 전환할 화면, 화면 전환 애니메이션/로직 설정 가능
       - 내비게이터 안에 내비게이터 들어갈 수 있음
       - 내비게터 옵션 중 screen options는 애니메이션 설정이 가능 (관련 doc 참고하면 좋음)
       - 화면 전환의 종류
         - 스택
           - 화면이 덮으면서 쌓이는 느낌이면 스택 내비게이터 이용
           - 전환되는 화면으로 들어가서야 렌더링 진행
         - 탭 내비게이터
           - 탭 전환처럼 화면이 바뀌는 느낌이면 탭 내비게이터 이용, material-top-tap-navigator 같은 외부 라이브러리 활용
           - 탭 내비게이터 안의 스크린 전부 렌더링 진행
           - 탑 탭
             - 홈 화면의 아이콘, 슈퍼조인, 채팅창 탭 구성시 이용
           - roottabnavigator
             - 앱이 켜질때 채팅창 미리 렌더링 하기 위해 탑탭 내비게이터 이용
             - 메인탭, 채트리스트로 메인 화면 구성
             - common popup stack
               - 메인스택 네비게이터 등에 영향 받지 않도록 루트 단에 위치. 내비게이터로 선언되어 스크린 옵션 적용도 가능
               - options 요소로 화면 전환 애니메이션을 이쪽 요소에만 다르게 적용 가능
               - 여기서 선언한 화면들은 훅을 이용해 호출함
     - screens
       - 화면 소스 파일들 저장. 내비게이터에 들어가는 스크린들
     - shared
       - 공통으로 자주 쓰이는 컴포넌트들 저장. button 등의 컴포넌트들이 들어있음
     - providers
       - 전체 화면에 모달 띄워야하는 경우 있음
       - root provider
         - root 단위에서 선언되어야 하는 컴포넌트들이 선언되어 있음
         - 내비게이터의 상태와 상관 없이 떠야하는 화면에도 비슷하게 선언되고 있음
         - 팝업 화면 전체에 반영되도록 하려고 이 곳에서 선언
         - 안에 선언된 popup 종류 : bottom popup(밑에서 뜨는 팝업), report popup(신고하기를 눌렀을 때 뜨는 화면)
         - 여기에 선언된 팝업들은 훅을 이용해서 호출함
       - 메인 화면의 bottom tab 까지 덮어서 팝업, 모달창이 떠야 함 > 컴포넌트의 최상단이나 메인 컴포넌트 상위에 작성 필요
   - hooks
     - 훅 관련 파일들 저장
     - 카메라 촬영을 해야하는 경우 os에서 기본 제공해주는 촬영 화면 이용 가능
     - ios/안드로이드 네이티브 화면들 > 관련 라이브러리를 이용해서 자바스크립트에서 코딩, 화면 띄우고 있음(라이브러리에서 제공하는 메소드 이용)
     - usekeyboard
       - 키보드, 이전 화면간 전환 관련으로 전환이 쉽게 되도록, 키보드가 나오고 들어갈때의 이벤트 등록 / 키보드 높이 가져올 수 있는 기능이 들어있음
       - 운영체제별 키보드를 다루는 방식이 다름
       - ios : 키보드를 앱의 구성 요소와 동일하게 보고 있음
       - 안드로이드
         - 키보드는 앱 밖에 있는 것으로 취급하고, 키보드 영역을 생성함. 키보드가 띄워지면 그 나머지 공간에 앱이 띄워지는 개념. 신경 써야 하는 부분임
         - 키보드가 내려갈때는 차지했던 화면에 전환되는 화면이 렌더링 되어야 함
         - 리액트 네이티브는 키보드를 다룰 때 문제가 있어 원활한 동작을 위해 키보드 높이 계산이 필요함
   - constants
     - style
       - light theme, dark theme 으로 라이트 테마, 다크 테마 관련 색상 값을 따로 저장하고 있음
       - 앱에서 다크모드 설정시 index.js appearance provider에서 정보 저장하고 그 하위 컴포넌트에 전달하고 있음
       - 색상 사용시 useColor라는 커스텀 훅 사용
   - db
     - 현재는 사용하지 않는 폴더
   - context
     - 리액트 기본 구조에서 자식 -> 부모로 데이터 전달이 어려움. 이런 부분 극복, 자식 부모 간 데이터 전달이 쉽도록 글로벌한 상태 관리하는 폴더
     - redux는 앱 전체에서 사용하는 상태값 관리 / context는 그 보다 좁은 모듈 단위에서 공통적으로 ㅆ느느 상태값 관리
     - 어떤 컴포넌트의 자식들까지 사용이 가능하다는 시점 지정이 가능
     - 프로젝트에서는 일정(이벤트) 기능 관련으로 context 사용하고 있음
     - 리덕스는 이런 context를 감싸서 만들어진 것으로 사용시 충돌을 막도록 사용법에 제한이 있음
   - i18m
     - 다국어 지원을 위한 폴더
     - usetranslation 훅을 이용하여 사용
     - t(문구) 라는 메소드를 호출해서 디바이스 설정에 따라 영문/한글 적용 시켜줄수 있음
   - proptypes
     - js에서의 타입 체크를 도와줄 수 있는 타입 지정 파일들 저장
     - 공통 적으로 많이 사용하는 컴포넌트의 프로퍼티 타입을 정의해두고 있음
     - 타입 지정시 사용하는 shape 메소드는 해당 타입이 오브젝트임을 명시할 때 사용함
   - redux 관련 폴더 : actions, reducer, store
   - 리덕스 스토어는 최상단에 저장되고 있음
   - component => action => reducer => store => component 이렇게 데이터 흐름이 단방향임(더 자세히 알고 싶으면 플럭스 구조체 확인 필요)
     - reducer
       - state의 생김새를 정의
       - store에 저장되는 state를 명시
       - 디스패치된 action을 받아 store의 state를 변경해줌
       - persist conifg : 영구 저장(로컬 스토리지 저장) 하고 싶은 상태들 명시
         - blacklist : 영구 저장에서 제외할 state 지정
     - action
       - state의 사용에 대한 정의
       - store 안에서 관리되는 state를 바꾸는 방법을 정의해줌
       - store.변수명으로 직접 변경하는 구조라면 코드가 꼬일 수 있음
       - store에 저장된 state 수정 방법을 여기서 정해놓고, 개발자는 수정 요청만 전달할 수 있도록 함
       - state 변경이 필요할 때 action을 발행함(액션을 디스패치함) -> 여기서 액션이 수행되면 데이터가 변경되는데, 이 때 변경된 데이터는 리듀서가 스토어에 적용시켜 줌
       - 리듀서의 데이터 적용이 완료되면 해당 state를 사용하는 전체 컴포넌트에도 적용되게 됨
     - store
       - root reducer를 가지고 생성도미
     - 관련 훅들
       - useSelector : store에서 state를 가져오는 훅
       - useDispatch : 액션을 수행하기 위해 액션을 발행해주는 훅
   - utils
     - 권한 등을 요청하는 유틸 파일들 모여 있음
   - api
     - 파이어베이스에 접근하는 코드들 저장
     - 실시간으로 반영 필요한 정보 있어, 파이어베이스에 실시간 소켓이 연결되어 있음 (리액트네이티브에서 제공하는 파이어베이스 docs, 파이어베이스 자체에서 제공하는 docs 확인해보면 좋음)
     - api 통해 callback으로 들어온 데이터들은 리덕스 스토어에도 반영됨

5. 파이어베이스 환경

- 현재 운영 서버만 제공 중이고 개발 서버 확인이 필요하면 서버에 대한 에뮬레이터 띄워서 작업해보면 됨
- 파이어베이스 functions
  - 클라이언트에서 db 조작하면 안되는 부분들은 functions 안에서 구현되어 있음
- 파이어스토어
  - 파이어베이스의 db
- 파이어베이스 관련 명령어 이용
  - npm 키워드 사용. yarn 키워드 사용이 권장되지 않음
  - 함수 배포시 npm run deploy 명령어 이용
  - 에뮬레이터 띄울때 npm run serve 명령어 이용 (프로젝트 안에 데이터가 저장되어있는 경우 사용)
  - 애뮬레이팅 서버 꺼지면 저장된 데이터도 다 날아가는데 npm run export 라는 명령어로 지금 서버에 저장된 데이터를 firebase store에 올려줄수 있음 (현재 운영서버에 붙지 않고, 애뮬레이팅 서버에 붙었다는 걸 꼭 확인해야할듯)
  - 애뮬레이팅 서버는 실제 호나경과 다르게 동작할 수 있어 유의
  - 앱에서 애뮬레이팅된 서버에 붙고 싶은 경우
    1. 기존에 띄워진 ios,안드로이드 시뮬레이터에서 로그아웃해서 운영 서버와의 연결 해제 (릴리즈 서버에 붙은 상태에서 다른 서버에 붙으면 꼬일 수 있음) > 앱 끄기
    2. index.js import set debugenv ~ set debugenv 쪽 주석해제하고 소스 저장
    3. 애뮬레이팅된 서버 올리고 다시 시뮬레이터 로드
- 메트로 서버 관련 프로세스가 꼬이는 경우
  - pkill java 명령어로 프로세스 킬하고 이용하면 될듯

6. 리액트 권장 패턴

- 컨테이너 - 프레젠테이션 구조
  - useSelector를 사용하려면 컨테이너 단에서 state를 다 가져온 후 프레젠테이션 단에 property 내려주는 것이 좋음
  - prop + useSelector 같이 사용하다보면 state가 꼬일 수 있음
  - useSelector 사용시 받아온 객체에 대한 메모이제이션 안되는 문제 있어서, 받아온 state 들을 실제 이용하려는 프레젠테이션 단의 prop으로 내려줘서 관리하는 게 좋음
- 맵뷰 관련 유의 사항
  - 맵뷰는 자원 소모가 커 리렌더링을 막는게 중요함

## 3. 기타 정리 사항

1.  Mac 단축키 : windows에서 control -> mac에서는 command 이용한다고 보면 됨

- command+q : 이용 중인 앱 닫기
- cntrl+command+q : 화면 잠금
- command+t : 탭추가
- command+w : 탭닫기
- 그외 단축키 : https://firetoad.me/mac/%EC%B4%88%EB%B3%B4%EC%9E%90%EB%A5%BC-%EC%9C%84%ED%95%9C-%EB%A7%A5-%ED%95%84%EC%88%98-%EB%8B%A8%EC%B6%95%ED%82%A4-%EB%AA%A8%EC%9D%8C-mac-shortcut/

2.  터미널 명령어

- code . (해당 위치에서 vscode 실행)
- open . (해당 위치에서 finder 열기)

3.  javascript core

- 리액트 네이티브로 작성됨
- javascript 코드를 android/iOS 네이티브 코드로 변환해줌

## 공부 todo 정리

1.  Yarn dev, yarn start, yarn build, yarn deploy, yarn export 의미

- next dev vs next build : dev할때 external libaray purge X, build할때는 external library purge되는게 다르다는 설명도 있음
- next dev : 개발모드에서 next js 실행. 실행하면 .next 폴더가 생김
- yarn dev (next dev 호출시) 충돌 해결 방법
- lsof -i tcp:3000
- kill -9 (PID숫자)
- next build : 프로덕션 용도로 애플리케이션을 빌드
- next start : nextjs 프로덕션 서버를 실행
- next export
  - nextjs로 빌드된 결과를 리액트 프로젝트 빌드 결과처럼 전환해주는 개념 ? ststic html로 쪼개주어 이때 nextjs에서 사라지는 장점을 보완해줌, export 하면 out 폴더 생성 out>index.httml을 웹서버에 배포(크롬 개발자 도구 element에 노출되는 정보가 이것이었군...! 이 index.html은 자바스크립트코드를 static html로 변경해준 것임!!)
  - 만들어진 static html은 nextjs sever 이외에서 돌아갈 수 있어 serverless development 가능
  - static site generator meaning : 빌드 시점에, 미리 진입할 수 있는 Page 를 파악하고, 이를 각각의 HTML 로 만들어 낸다. 이렇게 만들어진 static 파일 (html, css, js) 들은 S3 같은 호스팅 서버에 업로드하여 사이트를 구성 할 수 있음

2.  csr
    1. 개념/특징
    2. 장점
       - 초기 로딩이 오래 걸리지만 반응성이 좋음
    3. 단점
3.  ssr(server-side-rendering)

    1. 개념/특징
       - JSP와 비슷한 느낌
    2. 장점
       - 검색엔진 최적화(SEO) : 클라이언트만 렌더링되면 검색엔진 크롤러가 어플리케이션 데이터를 제대로 수집하지 못하는데, 이 부분을 해결할 수 있음(검색엔진 크롤러에서 데이터가 제대로 수집되어 검색결과 상위노출 검색시 원하는 정보 노출이 가능하므로... 크롤러에 정보가 잘 표시되도록 해줘야겠지..? ssr이 어렵다면 메타태그나 prerender쓴다고함(리액트 코드를 문자열로 반환하지 않고 자바스크립트 렌더링 엔진 통해 자스 ㅋ코드 실행시켜 뷰 렌더링한 결과값 반환스..)
       - 첫 렌더링된 html을 클라이언트에게 전달하므로 초기 로딩 속도가 빠름. 자바스크립트 파일 불러오고 렌더링 작업 완료 전에 사이드 컨텐츠 이용 가능
    3. 단점
       - 성능악화 가능성(동기적으로 작용하는 ReactDOMServer.renderToString 함수 >> 렌더링 되는 동안 다른 작업 불가) : 써드파티 라이브러리로 비동기 작동은 가능(rapascallion, hypernova, react-router-server)
       - 프로젝트 구조가 복잡해짐

4.  react vs nextjs

    1. react의 단점

       - spa로 로딩중일 때 검색엔진에 잘 안걸림(csr로 동작해서 seo 어렵)
       - 한번에 모든 데이터 가져오므로 비효율적(이건 코드 스플리팅으로 해결 가능)
       - ssr , 코드 스플리팅은 볼륨 커져도 효율성 위해 적용해야 하는데 b2c 서비스는 웬만하면 서버사이드 렌더링 고려 필요
       - 해결하려면 프리렌더(검색엔진 알아차리고, 검색엔진일 때에만 백엔드 서버에서 데이터 가져와서 줌 , 일반 유저일 땐 기존 리액트 방식으로 줌), ssr 구현하면 됨(첫 방문만 전통적인 방식대로 하고, 그 이후의 페이지 방문은 리액트 방식)

    2. nextjs의 장점
       - 리액트 프로젝트의 한계가 있어 nextjs 사용
       - nextjs 처음 시작시 ssr(server-side rendering) 그 이후에는 csr(client-side-rendering) 동작
       - react와 다르게 next는 static한 페이지를 만들며 pages 폴더안에 있는 js파일이 하나의 url처럼 작동
       - nextjs의 SSR
         - 첫 요청하는 페이지에 대해서만 SSG 혹은 SSR으로 Server Side에서 미리 구어 놓은 파일을 응답하는 것이고 그 이후부터는 router를 통해 이동하는 것은 CSR
         - nextjs의 ssg : build 시점에 server side에서 렌더
         - nextjs의 ssr : request 발생시 server sided에서 렌더

5.  nextjs with firebase

- react 한계 극복을 목적으로 nextjs 사용하려면 웹서버 특수 환경 세팅 필요
- 파이어베이스 서버 환경에서는 이런 환경 세팅이 어려움
- nextjs로 빌드된 결과 이용이 어려우므로 리액트 플젝으로 빌드된 내용 배포가 가능(현재 yarn build로 빌드된 nextjs 플젝 파이어베이스에 배포가 어려운 상황)
- yarn export : nextjs로 빌드된 결과를 리액트 프로젝트 빌드 결과처럼 전환해주는 개념 ? ststic html로 쪼개주어 이때 nextjs에서 사라지는 장점을 보완해줌, export 하면 out 폴더 생성 out>index.httml을 웹서버에 배포(크롬 개발자 도구 element에 노출되는 정보가 이것이었군...! 이 index.html은 자바스크립트코드를 static html로 변경해준 것임!!)

6.  github

    1. action
       - main branch에 merge라는 특정 동작 수행시 자동으로 빌드/배포 등의 동작을 수행해주도록 하는 것(일종의 트리거 같은건가?)
       - 현재는 main branch merge시 자동 빌드/배포는 안되고 있지만 추후에 action 이용하여 연동 가능
    2. git checout branch meaning
    3. git pull --reabase meaning

7.  firebase

- firebase 배포 경로 설정등은 아마 firebase.json(플젝 폴더 안에 있음)에 있지 않을가 싶음

8.  code split

- 코드 스플릿 : 더 빠르게 페이지 불러올 수 있음
