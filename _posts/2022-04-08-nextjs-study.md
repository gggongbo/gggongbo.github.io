---
layout: post
title: "Nextjs Study"
date: 2022-04-08 13:40:30 +0530
categories: Javascript NodeJS
---

<br>

# Next.js

## 관련 개념

1. CSR (Client Side Rendering)

- 첫 렌더시 그냥 페이지 로드, 다시 렌더링 하면서 데이터 불러옴. 그래서 검색엔진에 안걸림. 한 번에 데이터 다 불러오기 때문에 초기 로딩 속도는 느린데 페이지 이동 빠름 (반응성 좋음)
- 클라이언트에서 초기화면을 로드하기 위해 서버에 요청 보냄 > 서버는 화면에 표시하는데 필요한 완전한 리소스를 응답
- 동작 방식

  1. 브라우저 요청 > 프론트 엔드로부터 화면 그리는 코드 다운로드(모든 js 파일 다운로드, 데이터는 없음)
  2. 브라우저 > 백엔드 > DB > 백엔드 > 브라우저로 서버에서 데이터까지 모두 포함하여 페이지 구성

  - 일부 요소만 바뀌는 경우 2번 과정만 진행. 서버는 변경된 부분과 관련된 리소스만 응답

  1. 장점

  - 요청시 새로고침 없이 수정된 데이터 표시가 가능하고 사용자 친화적
  - 변경된 부분과 관련된 데이터만 가져오므로 SSR보다 빠른 반응 속도, 서버 부하 감소

  2. 단점

  - 초기에 모든 js 파일을 다운받아와야해서 초기 로딩이 오래 걸림
  - 자바스크립트를 사용하여 Interaction 후에 페이지 내용을 로드. 웹 크롤러가 페이지 색인화 하려하면 빈 페이지처럼 보이게 됨.

1. SSR (Server Side Rendering)

- 첫 렌더시 데이터도 서버측에서 함께 로드. 렌더 한 번만 하므로 초기 로딩 속도 빠르고 검색엔진에 데이터 걸림. 페이지 불러올때마다(매 request 마다) 중복 데이터 불러와야 해서 페이지 이동시 느림
- 기존에 사용하는 렌더링 방식이라고 생각하면 될 듯
- 서버로부터 완전하게 만들어진 html 파일을 받아와 페이지 전체를 렌더링
- 새로고침 현상 발생
- 동작 방식 : 브라우저 요청 > 프론트엔드 > 백엔드(서버에서 데이터까지 모두 포함하여 페이지를 구성) > DB > 백엔드 > 프론트엔드 > 브라우저 응답 전달

  1. 장점

  - 모든 데이터가 이미 html에 담겨진 채로 브라우저에 전달되어 검색엔진 최적화에 유리
  - 서버로부터 화면을 렌더하기 위한 필수적인 요소를 먼저 가져와 빠른 초기 로딩을 지님

  2. 단점

  - TTV(Time to View)와 TTI(Time to Interact) 간에 시간 간격이 존재 (버튼 클릭해도 아무 반응 없)
  - 페이지 요청 시 마다 새로 고침
  - 서버에서 페이지 구성하는 모든 리소스를 준비해서 응답. 서버측 부하가 증가

## 동작 방식

- SSR을 기반으로 하지만, 페이지가 로드된 이후에는 React에서 CSR을 이용하는 방식을 차용
- 리액트의 SSR을 쉽게 구현해주는 프레임워크
- Next.js를 사용하여 첫 페이지는 백엔드 서버에서 렌더링하여 빈 html이 아닌 데이터가 채워진 html을 받아 검색 최적화 문제를 해결. 그 다음 페이지 부턴 CSR 방식을 적용해서 필요한 데이터 부분만 갱신해 서버 부하 줄임

## Nextjs 특징

- 웹펙을 기본 번들러로 사용
- 넥스트 사용하지 않는 리액트 개발환경에서는 webpack.config.js 생산해서 플러그인, output 설정 필요(CRA 환경이면 자동으로 해주나 봄...)

## Nextjs 프로젝트 구조

- next.config.js
  - webpack plugin들과 nextjs 라우팅 설정 작성
  - redirects
  - exportpathmap 으로 라우팅 경로 지정
- styles
  - globals.css : \_app.tsx에서만 사용 가능
  - home.module.css : 다른 컴포넌트 css 설정 가능
- pages

  - index.tsx : 기본 홈페이지 (global.css와 연동)
  - \_app.tsx

    - 모든 페이지 컴포넌트를 감싸고 있는 공통레이아웃
    - 원하는 컴포넌트 import하면 모든 페이지 적용
    - 최초로 실행됨
    - Server only file(클라이언트에서 사용하는 로직인 window/dom 로직 사용이 어려움)
    - 페이지 업데이트 전에 원하는 방식으로 페이지 업데이트하는 통로
    - 내부의 컴포넌트 전부 실행하고 html body로 구성
    - 실행 이후 \_document.tsx 실행
    - 아래 기본 구성에서 props로 받은 component는 요청한 페이지. pageProps는 페이지 getInitialProps를 통해 내려 받은 props
    - 기본 구성(react 프로젝트의 App.tsx )

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

      ```
      //<Component {...pageProps} /> 의미
      //Spread 문법 이용한 것으로 보면 됨
      <Component pageProp1={pageProps.pageProp1} pageProp2={pageProps.pagePrp2} /> 과 동일
      }

      ```

  - \_document.tsx
    - html > head 하위에 meta 태그 정의 가능
    - static html을 구성하기 위한 app.js에서 구성한 html 바디가 어떤 형태로 들어갈지 구성하는 곳
    - content들을 브라우저가 html로 이해하도록 주조화시켜주는 곳
    - 전체 페이지에 관여하는 컴포넌트
    - 설정 안하면 디폴트 적용
    - 이곳 콘솔은 서버에서만 보임(클라이언트에서는 안보임)
    - 훅(react lifecycle api 같은거) 실행 x. static한 상황만 부여됨
    - Server only file (클라이언트에서 사용하는 로직 window/dom 로직 사용이 어려움)
  - Layout.tsx
    - 일반적으로 Layout.tsx 만들고 \_app.tsx를 layout으로 감싸서 사용
    - 원하는 전역 페이지 요소 제어
    - Navbar, Footer 등 component 화면에 만들고 layout.tsx에 import해서 사용
    - \_app.js, \_app.tsx 실행되며 갖춰진 content 들은 <Main> 아래에 생성된다

## 프로젝트 초기 세팅

- CRA와는 달리 자동으로 적용이 안돼서 eslint, prettier 직접 설정 필요

## API 설명

- next/head
  - import하고 이 태그에 값을 넣으면 seo(검색엔진 옵티마이저) 잘 찾는형태로 구현
  - <Head>태그로 사용
- next/link
  - react-router-dom 기능을 함
  - <Link>태그로 사용
- next/router
  - react-router-dom 기능을 함

## ServerSide 렌더링

- 렌더링 사이클

1.  Next Server가 GET 요청을 받는다.
2.  요청에 맞는 Page를 찾는다.
3.  \_app.tsx의 getInitialProps가 있다면 실행한다.
4.  Page Component의 getInitialProps가 있다면 실행한다. pageProps들을 받아온다.
5.  document.tsx의 getInitialProps가 있다면 실행한다. pageProps들을 받아온다.
6.  모든 props들을 구성하고, \_app.js > page Component 순서로 rendering.
7.  모든 Content를 구성하고 \_document.js를 실행하여 html 형태로 출력한다.

- getInitialProps
  - 웹페이지는 각 페이지마다 사전에 불러와야할 데이터들이 있음(데이터 패칭)
  - 데이터 패칭은 CSR에서는 리액트 로직에 따라 componentDidMout / useEffect 로 컴포넌트가 마운트 되고 나서 하는 경우가 많은데, 이 과정을 서버에서 미리 처리하도록 도와주는게 getInitialProps
  - Nextjs 9.3버전에서는 대신에 getStaticProps, getStaticPaths, getServerSideProps 사용하게 된다고 함
  - 데이터 패칭을 서버에서 하게되면 속도가 빨라진다. (연산을 서버와 함께하고 미리 데이터 받아와 브라우저는 렌더링만 할 수 있음)
  - 브라우저가 데이터를 가져올때까지 화면 렌더링을 null 처리하는 경우가 있는데, 이 과정이 없어지고 initial한 데이터가 들어오는 과정을 전제로 코드를 작성할 수 있다
  - 공통된 데이터 패칭이 필요 : \_app.js에 getInitialProps를 붙임
  - 페이지마다 다른 데이터 패칭 필요 : 페이지마다 getInitialProps를 붙임
  - 내부 로직은 서버에서 실행(클라이언트에서 사용하는 로직 window/dom 로직 사용이 어려움)
  - 한 페이지를 로드할 때 하나의 getInitialProps 로직만 실행
  - \_app.js에 getinitalprops를 달면 그 하부 페이지의 getinitalprops는 실행되지 않는데 아래처럼 하면 하부 페이지의 getinitialprops 달고 pageprops 받아올 수 있음
  - getInitialProps (appContext) >> 기본적으로 받아오는 인수 : context(ctx) 객체
- ctx object
  - pathname : 현재 pathname /user?type=normal page 접속 시에는 /user
  - query : 현재 query를 object형태로 출력 /user?type=normal page 접속 시에는 {type: 'normal'}
  - asPath : 전체 path /user?type=normal page 접속 시에는 /user?type=normal
  - req : HTTP request object (server only)
  - res : HTTP response object (server only)
  - err : Error object if any error is encountered during the rendering

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

   - 서버가 있어도 서버의 존재에 대해 신경쓰지 않아도 됨. 서버 사양, 갯수, 네트워크 설정할 필요가 없음
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
   - 플젝을 하나의 함수, 여러개의 함수로 쪼개서 거대하고 분산된 컴퓨팅 자원 함수 등록, 함수 실행 횟수 및 시간 만큼 비용 내는 방식
   - AWS Rambda 등 포함
   - 배치 기능 구현 가능
   - 웹 요청 처리 가능 (특정 url로 들어온 경우 작업 하도록해서 백엔드 api 구성 가능)
   - 콘솔 통한 직접 호출 가능
   - 백엔드,크롤러,파일 업/다운로드 등의 처리, 로그 분석/자원사용 모니터링, 자동화 작업, 백업 등 가능
   - 애플리케이션이 안니 함수를 배포. 계속 실행되는게 아니라, 특정 이벤트 발생시 실행. 작업 마치거나 timeout 지나면 종료
   - 장점 : 비용 절약, 인프라 관리 공수 감소, 인프라 보안 신경 쓸 필요 없음. 확장성이 뛰어남(auto scaling처럼 특정 조건에서 자동 확장이라기 보다는.. 함수 호출 횟수에 따라 호출개수가 확장되니까 확장성이 뛰어나다고 하는 듯)
   - 단점 : 자원 사용 제약(웹소켓 같은건 못씀..), 제공사에 대한 의존성 높아짐. 함수는 stateless하므로 로컬 스토리지에서 데이터 read/write 불가
   - 비교적 최근에 나와서... 자료가 마니 엄슴

## CSS in JS

## Template Literal

- 탬플릿 문자열. 백틱(`)을 써서 표현식을 넣을 수 있음
- `test is ${test}` 이런 애들
- Tagged Template

  - 함수`` 형태로 함수 호출 가능
  - 타입에 상관없이 function, numver, array, object 전달 및 실행 가능

  ```
     const userName = 'test';
        const age = 10;
        function transform(staticData, ...dynamicData){
            console.log(staticData); //['Hi, ', ' and I am ', '']
            console.log(dynamicData); //['test', 10]
        }

        transform`Hi, ${userName} and I am ${age}`;

    //${}을 통해 함수를 넣어줬다면 함수 사용 가능
    function sample(texts, ...fns) {
      const mockProps = {
          title : '안녕하세요',
          body :  '내용입니다.'
      };

      retrun texts.reduce((result, text, i) =>
      `${result}${text}${fns[i]? fns[i](mockProps) : ''}`
      , '');
    }

    sample `
      제목 : ${props => props.title}
      내용 : ${props => props.body}
    `

    실행시 function(props){
      return props.title
    } 함수가 전달 >> function(mockProps){
      return mockProps.title;
    } 실행
  ```

  - styled-component에서 이를 사용하여 컴포넌트의 props 일거옴

  ```
  const StyledDiv = styled`
    background: ${props => props.color};
  `; 와 같은 형태로 사용 가능
  ```
