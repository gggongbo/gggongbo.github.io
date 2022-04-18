# Work & Development Environment

## 1. 업무 관련 정리 사항

- 업무시간 : 9시~6시- 수습기간 : 3개월
- 담당업무 : 슈퍼조인 프론트엔드, 백엔드 로직(앱의 주요기능들은 구현되어 있는 상황으로 주로 유지보수 위주로 진행 예정)
- 이용 프로그래밍 언어 : 자바스크립트
- 서버 관련 사항 : 파이어베이스(주언어 : 타입스크립트)에서 이관 진행 중
  (1.파이어베이스 외 다른 서버 이용 / 2.백엔드 로직 구현 중에 이뤄질 것이며 1.다른 서버 이용 예정일 것)
- 공유 사항 : 개인블로그/노션 혹은 지라에 공유 가능

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
  - peeps.sxodeproj : 설정 파일
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
