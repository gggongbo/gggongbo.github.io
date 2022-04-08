---
layout: post
title:  "Nextjs Study"
date:   2021-04-08 13:40:30 +0530
categories: Javascript NodeJS
---
<br>

# Next.js
## 관련 개념
1. CSR (Client Side Rendering)
- 첫 렌더시 그냥 페이지 로드, 다시 렌더링 하면서 데이터 불러옴. 그래서 검색엔진에 안걸림. 한 번에 데이터 다 불러오기 때문에 초기 로딩 속도는 느린데 페이지 이동 빠름 (반응성 좋음)
2. SSR (Server Side Rendering)
- 첫 렌더시 데이터도 서버측에서 함께 로드. 렌더 한 번만 하므로 초기 로딩 속도 빠르고 검색엔진에 데이터 걸림. 페이지 불러올때마다(매 request 마다) 중복 데이터 불러와야 해서 페이지 이동시 느림 

## 동작 방식
* SSR을 기반으로 하지만, 페이지가 로드된 이후에는 React에서 CSR을 이용하는 방식을 차용

## Nextjs 프로젝트 구조
 * next.config.js
   - webpack plugin들과 nextjs 라우팅 설정 작성
   - redirects 
   - exportpathmap 으로 라우팅 경로 지정
 * styles
   - globals.css : _app.tsx에서만 사용 가능
   - home.module.css : 다른 컴포넌트 css 설정 가능
 * pages
    - index.tsx : 기본 홈페이지 (global.css와 연동)
    - _app.tsx
      - 모든 페이지 컴포넌트를 감싸고 있는 공통레이아웃
      - 원하는 컴포넌트 import하면 모든 페이지 적용
      - 최초로 실행됨
      - 페이지 업데이트 전에 원하는 방식으로 페이지 업데이트하는 통로
      - 내부의 컴포넌트 전부 실행하고 html body로 구성
      - 실행 이후 _document.tsx 실행
      - 기본 구성(react 프로젝트의 App.tsx  )
        ```
        import '../styles/globals.css'
        import type { AppProps } from 'next/app'

        function MyApp({ Component, pageProps }: AppProps) {
            return <Component {...pageProps} />
        }

        export default MyApp

        cf) Typescript 기반 리엑트 플젝 app.tsx

        function App() {
            return <div></div>; //JSX 방식
        }
        ```
    - _document.tsx
      - html > head 하위에 meta 태그 정의 가능
      - 전체 페이지에 관여하는 컴포넌트
      - 설정 안하면 디폴트 적용
      - 이곳 콘솔은 서버에서만 보임(클라이언트에서는 안보임)
      - 훅(react lifecycle api 같은거) 실행 x. static한 상황만 부여됨
    - Layout.tsx
      - 일반적으로 Layout.tsx 만들고 _app.tsx를 layout으로 감싸서 사용
      - 원하는 전역 페이지 요소 제어
      - Navbar, Footer 등 component 화면에 만들고 layout.tsx에 import해서 사용

## 프로젝트 초기 세팅
- CRA와는 달리 자동으로 적용이 안돼서 eslint, prettier 직접 설정 필요
  
## API 설명
* next/head
    - import하고 이 태그에 값을 넣으면 seo(검색엔진 옵티마이저) 잘 찾는형태로 구현
    - <Head>태그로 사용
* next/link
    - react-router-dom 기능을 함
    - <Link>태그로 사용
* next/router
    - react-router-dom 기능을 함

## ServerSide 렌더링
* 렌더링 사이클
 1. Next Server가 GET 요청을 받는다.
 2. 요청에 맞는 Page를 찾는다.
 3. _app.tsx의 getInitialProps가 있다면 실행한다.
 4. Page Component의 getInitialProps가 있다면 실행한다. pageProps들을 받아온다.
 5. document.tsx의 getInitialProps가 있다면 실행한다. pageProps들을 받아온다.
 6. 모든 props들을 구성하고, _app.js > page Component 순서로 rendering.
 7. 모든 Content를 구성하고 _document.js를 실행하여 html 형태로 출력한다.

# Serverless Architecture

## 개념
- 특정 작업을 수행하기 위해 컴퓨터/가상머신에 서버 설정하고 이를 통해 처리하는 것이 아닌 것
- 처리는 BaaS(Backend as a Service) 혹은 Faas(Function as a Service)에 의존하여 작업 처리
- BaaS : Firebase, Parse, Kinvey
- FaaS : AWS Lambda, Azure, Functions, Google Cloud Functions
  
## 기존 기술과의 차이
1. 기존 기술 특징
   - 공간, 하드웨어, 네티워크, 운영체제 모두 직접 관리

## IaaS, PaaS, Baas, FaaS
2. IaaS(Infrastructure as a Service) : AWS, Azure 서비스로 서버자원, 네트워크, 전력 등의 인프라 직접 구축할 필요 사라짐
3. PaaS(Platform as a Service) : IaaS에서 한번 더 추상화된 모델. 네트워크, 런타임까지 제공해서 애플리케이션 배포하면 바로 구동이 가능. AWS Elastic Beanstalk, Azure App Service (auto scaling, load balancing 적용 가능)
4. BaaS, FaaS
   - 서버가 있어도 서버의 존재에 대해 신경쓰지 않아도 됨. 서버 사양, 갯수, 네트위커 설정할 필요가 없음
   - BaaS : 데이터 저장 다른 기기에서도 접근/공유시 가능하게 하려면 백엔드 서버 필요. 데이터베이스, 소셜서비스 연동, 파일시스템을 api로 제공. 서버 이용자가 늘어나도 서버 알아서 확장됨

5. BaaS 사용의 이점
   - 개발 시간 단축, 서버 확장 작업 불필요.
   - Firebase는 실시간 데이터베이스 사용해서 소켓을 써서 클라이언트에 바로 반영해주는 기능 있음. (백엔드 서버 필요하지만 실시간 기능 최소 공수로 구현하고 싶으면 feather.js 사용하는 방법도 있음)
   - 일정 사용량까지는 무료 사용 가능.
   - 토이/소규모 플젝에 유용
6. BaaS 사용의 단점
   - 클라이언트 위주의 코드
     - 백엔드 로직이 클라에 구현될 수 있음. Firebase SDK로 일부 로직 서버측에 구현 가능(메일 발송, 결제 처리 등)
     - 데이터 단 로직 변경되면 클라이언트 코드 수정 필요 > 웹어플은 상관 없는데 앱은 업뎃해야함... 구버전 사용자도 강제 업뎃 시켜야하는 경우가 발생할 수 잇슴..
   - 가격 : 실시간 데이터베이스에 10G 가 쌓이고, 한달 전송되는 데이터의 양이 20G 정도면 데이터베이스 비용으로만 $70 가 발생
   - 복잡한 쿼리가 불가능 : Firebase는 데이터베이스가 하나의 json 객체로 구조화됨. 최대한 DB 모델 비정규화해서 사용하는게 좋음
7. FaaS
   - 플젝을 하나의 함수, 여러개의 함수로 쪼개서 거대하고 분산된 컴퓨팅 자워네 함수 등록, 함수 실행 횟수 및 시간 만큼 비용 내는 방식
   - AWS Rambda 등 포함
   - 배치 기능 구현 가능
   - 웹 요청 처리 가능 (특정 url로 들어온 경우 작업 하도록해서 백엔드 api 구성 가능)
   - 콘솔 통한 직접 호출 가능
   - 백엔드,크롤러,파일 업/다운로드 등의 처리, 로그 분석/자원사용 모니터링, 자동화 작업, 백업 등 가능
   - 애플리케이션이 안니 함수를 배포. 계속 실행되는게 아니라, 특정 이벤트 발생시 실행.  작업 마치거나 timeout 지나면 종료
   - 장점 : 비용 절약, 인프라 관리 공수 감소, 인프라 보안 신경 쓸 필요 없음. 확장성이 뛰어남(auto scaling처럼 특정 조건에서 자동 확장이라기 보다는.. 함수 호출 횟수에 따라 호출개수가 확장되니까 확장성이 뛰어나다고 하는 듯)
   - 단점 : 자원 사용 제약(웹소켓 같은건 못씀..), 제공사에 대한 의존성 높아짐. 함수는 stateless하므로 로컬 스토리지에서 데이터 read/write 불가
   - 비교적 최근에 나와서... 자료가 마니 엄슴