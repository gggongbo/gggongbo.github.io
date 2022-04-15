# 1장

## 리액트는 무엇일까요

- 페북에서 개발하고 관리하는 UI 라이브러리
- UI 기능만 제공(전역 상태 관리, 라우팅, 빌드 시스템은 개발자가 직접 구축 필요)
- create-react-app(cra) 를 이용하면 리액트를 처음 사용하는 사람도 하나의 명령어로 리액트 개발환경 구축 가능
- API 통신, 사용자 이벤트를 통해 프로그램 상태값 변경 > 리액트가 변경된 상태값 기반으로 UI 자동 업데이트
- 리액트를 쓰지 않으면 브라우저의 돔을 직접 업데이트해야함(순수 자바스크립트나 자체 라이브러리로 처리할 수 있음)

## 리액트 장점

- 가상 돔을 통해 UI 빠르게 업데이트 가능
- 가상 돔은 이전 UI 상태를 메모리에 유지. 변경될 UI의 최소 집합을 계산하는 돔 기술
- 가상 돔은 데이터가 변경됐을때 ui에서 변경될 부분을 빨리 찾기 위해 사용되는 범용적인 자료구조
-

## 리액트 특징

- 함수형 프로그래밍을 적극 활용
- render 함수는 순수 함수로 작성 (순수함수 : 동일한 입력에 대해 항상 동일한 출력 반환. 외부의 상태와 독립된 함수)
- 인수 state가 변하지 않으면 render 함수는 항상 같은 값을 반환
- 컴포넌트 상태값 수정시 기존값 변경보다는 새로운 객체 생성 필요
- 이렇게 하면 복잡도 낮아짐. 렌더링 성능 향상 가능

```
//순수하지 않은 함수
let c = 1;
function(a,b) {
    return a+b+c;
}

console.log(func(2,2));

c = 2;

console.log(func(2,2)); //외부 값에 영향 받음

let c = 1;
function fuc(a,b){
    c +=1;
    return a+ b;
}

func(2,2); //함수가 실행되면 외부값 c 변화. 부수효과 발생
console.log(c);
```

- state는 불변 변수로 관리

## cra 없이 리액트 개발 환경 구축

- react 패키지 > 웹, 앱 둘다 사용 / react-dom 패키지 > 웹에서만 사용

## 리액트 네이티브

- 리액트로 안드로이드, ios 네이티브 앱 개발 가능
- 웹 애플리케이션 개발시 사용하는 리액트 패키지가 리액트 네이티브에서도 그대로 사용
- 웹에서의 react-dom 역할 하는 리액트 네이티브 코드가 별도로 존재함
- 하나의 소스코드로 안드로이드, ios 동작 앱 개발 가능
- 인앱 구매, 추시 알람과 같이 플랫폼에 종속적인 기능 사용 위해서는 플랫폼별 코드 작성 필요
- 모바일에서 자바스크립트를 실행하기 위해 javascriptcore를 사용
- javascriptcore는 웹킷에 내장된 자바스크립트 엔진
- 대부분의 모바일 운영체제는 앱에서 c++코드를 실행할 방법을 제공해준다
- 리액트 네이티브는 c++로 작성된 javascriptcore를 앱 빌드시 포함해서 자바스크립트 실행 환경을 제공
- 리액트의 가상돔은 리액트 네이티브에서도 동작

## 바벨

- 바벨은 자바스크립트 코드를 변환해주는 컴파일러
- 최신 자바스크립트 문법 지원하지 않는 환경에서도 최신 문법 사용 가능
- 코드에서 주석을 제거하거나 코드 압축하는 용도 사용
- 리액트에서는 jsx 문법 사용 위해 바벨을 사용
- 바벨이 jsx 문법으로 작성된 코드를 createElement 함수를 호출하는 코드로 변환

## 웹팩

- 자바스크립트로 만든 프로그램을 배포하기 좋은 형태로 묶어줌
- SPA로 웹페이지 제작 방식 전환 > 한 페이지에 필요한 자바스크립트 파일이 수십 수백개로 증가
  ```
  <html>
    <head>
        <script type="text/javascript" src="javascript_file_1.js"></script>
        <script type="text/javascript" src="javascript_file_2.js"></script>
        <script type="text/javascript" src="javascript_file_3.js"></script>
    </head>
  </html>
  ```
- 파일 간 의존성으로 선언 순서 신경써야 함
- 뒤에 선언된 파일이 앞에 선언된 파일에서 생성한 전역 변수를 덮어쓰는 위험있음
- 웹팩은 ESM(ES6의 모듈 시스템) commonjs(es6 나오기 전 등장한 모듈 시스템. node.js가 이 표준을 따름) 모두 지원
- 이 모듈 시스템 이용해서 코드 작성하고 웹팩을 실행하면 예전 버전의 브라우저에서도 동작하는 코드 만들 수 있음
- 실행하면 하나의 자바스크립트 파일이 만들어짐(여러 개 파일로 분리가 가능)
- 자바스크립트 파일 압축, css 전처리등의 기능이 있음

## 클래스형 컴포넌트와 함수형 컴포넌트

- 리액트 16.8 이전 버전의 함수형 컴포넌트는 상태값 가질 수 없고, 리액트 컴포넌트의 생명 주기 함수를 작성할 수 없음
- 리액트 버전 16.7부터 훅이라는 기능 추가되며 함수형 컴포넌트에서도 상태값, 생명 주기 함수 코드 작성이 가능
- 레거시 프로젝트 관련 클래스 컴포넌트의 생명 주기 메소드 이해 필요

## CRA

- 바벨, 웹팩, 테스트 시스템, hmr(hot-module-replacement), es6+문법, css 후처리 등의 개발 환경 구축해줌
- 기존 기능 개선, 새 기능 추가 시 패키지 버전만 올리면 됨

## ESM 문법

- ES6의 모듈 시스템
- 모듈을 내보내고 가져오는 코드 가져올 수 있음
- 내보내기 : export 키워드 이용
- 가져오기 : import 키워드 이용
- default는 한 파일에서 한 번만 사용 가능
- default 키워드로 내보내진 코든느 괄호없이 가져올 수 있고, 이름은 원하는대로 정할 수 있다

# package.json 주요 명령어

- yarn start(react-script start) : 개발 모드로 프로그램 실행. hmr이 동작해서 코드 수정하면 화면에 즉시 반영. 새로고침 할 필요 없음
- HTTPS=true yarn start : 자체 서명된 인증서와 함께 https 사이트로 접속
- yarn build : 배포 환경에서 사용할 파일 만들어줌. 정적 파일 생성
  - build/static 폴더 밑에 생성된 파일 이름에는 해시값 포함
  - 파일 내용 변경되지 않으면 해시값은 항상 동일. 새로 빌드해도 변경되지 않은 파일은 브라우저에 캐싱되어있는 파일 사용 가능
  - js에서 import 로 가져온 css는 build/static/css/main.{해시값}.chunk.css에 저장
  - 여러 개의 css 파일을 임포트해도 모두 앞의 파일에 저장도미
  - js에서 import로 가녀온 폰트, 이미지 등의 리소스 파일은 build/static/medi 폴더 밑에 저장. 이미지 파일 크기가 10kb 미만이면 파일 생성 x, data url 형식으로 자바스크립트 파일에 포함
- yarn test : jest라는 테스트 프레임워크 기반으로 테스트 시스템이 구축
  - 테스트 파일 : '**test**' 폴더 밑에 있는 모든 자바스크립트 파일, .test.js, .spec.js 로 끝나는 파일은 테스트 파일로 인식

# 설정 파일 추출

1. yarn eject 명령어로 내부 설정 파일 추출
2. react-scripts 프로젝트를 포크해서 나만의 스크립트 만들거나 react-app-rewired 패키지 사용

# 지원 기능

- 지수 연산자
- async, await 함수
- rest, spread operator
- dynamic import
- class field
- jsx
- typescript, flow type system

# 폴리필

- 실행시점에 기능(새로운 객체, 함수)이 존재하는지 검사하고, 그 기능이 없을때만 주입하는 것 의미

# 코드 스플리팅

- 사용자에게 필요한 양의 코드만 내려줄 수 있음
- 사용하지 않으면 전체 코드를 한 번에 내려줌 > 첫 페이지 뜨는 시간이 오래 걸림
- 방법
  1. 동적 임포트 이용
  - spa 만들기 위해 react-router-dom 패키지를 이용하는 경우에는 react-router-dom에서 지원하는 기능 이용해 페이지 단위 코드 분할 가능

## 환경 변수 사용

- 빌드 시점에 환경 변수를 코드로 전달 가능
- 개발, 테스트, 배포 환경별로 다른 값 적용 가능
- 전달된 환경변수는 코드에서 process.env.{환경변수 이름}으로 접근할 수 있음
- NODE_ENV 환경 변수 기본으로 제공
  - 환경 변수 값
    - npm start : development
    - npm test : test
    - npm run build : production
- 기타 환경 변수는 process.env.REACT_APP\_ 형태로 접근
- 셸에서 입력 or .env 파일 이용해 입력 가능
  - REACT_APP_API_URL=api.myapp.com yarn start
  - .env 파일 안에 작성
  - 로컬 머신에 저장된 환경변수 이용 가능(REACT_APP_NODE_VERSION=$npm_version 이런 식으로)
  - index.html에서 환경 변수 사용이 가능 (<title>%REACT_APP_NODE_VERSION%</title>)

## CSS

- autofixer
  - cra autofixer 패키지로 벤더 접두사 자동으로 붙음
- 일반적인 css 파일에는 클래스명 충돌될 수 있는데 css-module 사용하면 충돌 극복 가능
- {이름}.module.css로 작성
- sass
  - 공통으로 사용하는 클래스명 @infoColor: #aaaaaa; 로 선언 가능
- css-in-js
  - css 코드를 자바스크립트 파일 안에서 작성
  - 가장 유명한 패키지 : styled-components
  - styled-component로 동적 스타일 적용할때 값 px 이렇게 중간에 띄어쓰기 들어가면 안 먹음.. tagged template literal 특징인듯
  - styled.div`` 안에서 표현식(${}) 사용하면 컴포넌트 속성값을 매개변수로 갖는 함수를 작성할 수 있음

## SPA

- 초기 요청시 서버에서 첫 페이지를 처리하고 이후의 라우팅은 클라이언트에서 처리하는 웹 어플리케이션
- 페이지 전환에 의한 렌더링을 클라이언트에서 처리
- SPA 구현이 가능하려면 필요한 기능
  - 자바스크립트에서 브라우저로 페이지 전환 요청 보낼 수 있고, 브라우저는 서버로 요청을 보내지 않아야 함
  - 브라우저의 뒤로 가기 같은 사용자 페이지 전환 요청을 자바스크립트에서 처리 가능해야함(브라우저는 서버로 요청 보내면 안됨
- 이 조건 만족 하는 브라우저 API : pushState, replaceState 함수, popState 이벤트 (브라우저는 히스토리에 state를 저장하는 스택이 존재함)
- pushState : 스택에 state 쌓임
- replaceState : 스택에 state 쌓지 않고 가장 최신의 state를 대체

- react-router-dom
  - 페이지 라우팅 처리에 사용
  - 사용하려면 전체를 BrowserRouter 컴포넌트로 감싸야 한다
  - 버튼을 통한 페이지 전환시 Link 컴포넌트 사용, to 속성값은 이동할 주소 의미
  - Route 컴포넌트로 각 페이지 정의
    - path 속성 : 요청오는 주소
    - (deprecated) component : path 속성값과 매핑되는 컴포넌트 명
    - element: path 속성값과 매핑되는 컴포넌트 명 element={<Home/>} 같은 형태로 사용
    - exact 속성 값 입력하지 않으면 root(/) path와 매핑되는 컴포넌트가 계속 렌더링될 것임 > router v6에서 이 이슈 해결됨
    - 같은 path 속성을 갖는 route 컴포넌트 여러 번 작성 가능
    ```
    // 예시
    element={
              <div>
                <Photo /> <Photo2 />
              </div>
            }
    ```
    - v6에서 달라진점 > 예제와 다름
    - router 태그 여러 개 사용시 routes나 switch로 감싸야함
    - match property 사용 불가 > match.id, match.params.:customId 사용 불가해짐
    - 부모 라우트 밑에 /\* 달아줘야 자식 컴포넌트의 라우트가 제대로 작동함
    - <Link to="path"> 지정해주면 현재 라우트/path로 자동으로 인식됨 자식 컴포넌트에서 (${match.url}/path) 지정할 피요 없음
    - useParams 메소드 가져와서 let params = useParams(); > params.:customId 로 사용할 수 있음

# 8장 서버 사이드 렌더링 & 넥스트

## CRA와 넥스트의 차이

- CRA는 클라이언트 렌더링만. 넥스트는 서버사이드 렌더링에 특화되어 있음
- 넥스트는 CRA와 다르게 웹팩 설정 변경 가능(next.config.js에서 웹팩 설정 변경 가능)

## 페이지 컴포넌트 위치

- pages 폴더 밑에 만들어야 한다

## 넥스트 특징

- 넥스트는 리액트 모듈을 자동으로 포함시켜 준다(파일 상단에 import REACT from 'react'; 작성하지 않아도 됨

## 넥스트 빌드 후 프로젝트 구조

- 브라우저 상 전달된 파일 구조
  - 페이지명.js : 작성한 페이지 코드가 들어있음(서버 사이드 렌더)
  - \_app.js : 모든 페이지의 최상단에서 실행되는 리액트 컴포넌트
  - framework-해시값.js : 넥스트에서 사용하는 주요 패키지(리액트 등) 코드 들어 있음
  - 해시값.js : 여러 페이지에서 공통으로 사용하는 코드
  - main-해시값.js : 웹팩 런타임 코드
  - \_nex/static 폴더
    - 해시값/pages : 각 페이지의 번들 파일
    - chuncks : 여러 페이지에서 공통으로 사용하느 번들 파일
    - runtime : 웹팩과 넥스트의 런타임과 관련된 번들 파일
- ./next 폴더에 생성된 파일 구조
  - ./next/server/static
    - 서버에서 사용되는 파일 들어감
    - node_modules의 외부 모듈코드가 파일에 포함돼있지 않음. 서버에서 실행되어 포함 X
    - page.html 처럼 페이지 파일이 html 파일로 확인 가능
    - 넥스트는 정적인 페이지를 자동으로 미리 렌더링해서 최적화함(변수를 사용하지 않아 렌더링 결과가 항상 같은 페이지의 경우)
    - 동적인 페이지는 미리 렌더링하지 않고 자바스크립트 파일로 만듦
    - \_document.js : 서버 측에서 html 요소를 추가하는 용도로 사용
  - ./next/server/chunks
    - 서버 쪽에 생성된 웹팩 번들 파일 확인 가능 (넥스트는 기본적으로 페이지 별 번들 파일 생성, 동적 임포트 시에도 생성됨)

## 넥스트 활용

- Head 컴포넌트 : head 태그 하위에 원하는 돔 요소 추가 가능, <head>태그 여러번 사용 가능(나중에 하나로 합쳐짐)
- styled-jsx 패키지 : css-in-js 방식 지원. 선언된 스타일은 컴포넌트 내부에만 적용
- 넥스트가 생성한 html : script 태그로 여러 가지 자바스크립트 파일을 가져옴(\_\_NEXT_DATA\_\_ 라는 json 형태의 환경 변수도 가져오고 있음(pageProps 객체))
- 프로젝트루트/static : 이미지 파일과 같은 정적 파일 서비스 가능.
- 웹팩 file-loader : 파일의 내용이 변경되면 파일 경로도 변경되는 기능 구현 가능. 이미지 경로 뒤에 해시값 붙음.(브라우저 캐싱 기능 사용 가능) 사용시 next.config.js에서 설정 필요.(해당 설정안에 images:{disableStaticImages:true}) 설정 필요

## 서버에서 생성된 데이터 전달하기

- getInitialProps : 페이지 진입 직전에 호출.
- 첫 페이지를 요청하면 서버에서 호출.
- 이후 클라이언트에서 페이지 전환을 하면 클라이언트에서 함수 호출
- 반환하는 값은 페이지 컴포넌트의 속성값으로 입력됨
- getInitialProps 함수는 서버에서 호출되며 이 함수를 통한 데이터의 전달은 넥스트의 큰 장점
  ```
  myComponent.getInitialProps = async({req}) => {
    const userAgent = req ? req.headers['user-agent'] : navigator.userAgent;
  }
  //http 요청 객체도 매개변수로 전달됨. http 요청과 응답 객체는 getInitialProps 함수가 서버에소 호출되는 경우에만 전달
  //헤더에서 user-agent 정보를 추출, getInitialProps가 호출되지 않아 req가 빈 상태(클라이언트에서 호출)라면 브라우저의 navigator 전역 변수 이용
  ```

## 페이지 이동

- Link 컴포넌트, Router 객체 제공하여 페이지 이동
- 페이지 이동시 Link, Router 컴포넌트 기능ㅈ거 차이는 없지만 Router 객체가 동적인 코드에 적합

## 에러 페이지 구현

- 넥스트에서 에러페이지 기본으로 제공
- 커스텀하고 싶으면 \_error.js 파일 작성하면 됨
- next dev로 테스트 시 서버에서 발생한 오류 > error.js가 받아오지 못함. 빌드하고 프로덕션 환경에서 start 해야 제대로 반영됨
- next dev 실행시 : 서버에 response 에러 코드 500으로 찍힘. buildManifest.js 확인 시 경로 / 유니코드로 표시
- next build && next start 실행시 : 서버에 response 에러 코드 200 으로 찍힘. 빌드 후 실행했을 때 크롬 개발자 모드에서 \_error.js 확인 가능

## 페이지 공통 기능 구현

- \_app.js의 MyApp 컴포넌트
  - 페이지가 전환되어도 언마운트되지 않음. 항상 유지되어야 하는 컴포넌트들 여기에 선언되어있음
  - MyApp 컴포넌트에서 전역 상태값 관리 가능

## 코드 분할

- 넥스트는 기본적으로 페이지 별 번들 파일 생성
- 동적 임포트 사용 시에는 해당 모듈의 코드는 별도 파일로 분할
  - 테스트시 916.js 라는 형식으로 별도 번들 파일 생성, 클라이언트 뿐만 아니라 서버를 위한 파일도 생성됨
- 여러 페이지에 공통 사용 모듈도 별도 파일로 분리됨

## 여러 페이지에 공통으로 사용되는 코드 분할

- 넥스트는 여러 페이지에서 공통으로 사용되는 모듈을 별도의 번들 파일로 분할
- 웹팩의 splitChunks 설정을 통해 코드 분할. 코드 변경에 따른 캐시 무효화 최소화 하는 방향으로 설계
- 책 예제에 나온대로 여러 모듈에 공통으로 js 모듈 사용했으나, 빌드된 번들 파일 분리가 안되었음 > 재확인 필요

## 웹서버 직접 띄우기

- express 등의 웹서버를 사용하지 않으면, 넥스트 내장 웹 서버 사용할 수 있음
- 직접 웹 서버를 띄워 서버사이드 렌더링 결과 캐시 가능 (url로 직접 접근시에도 캐싱이 가능, 많은 트래픽의 처리가 가능)

## 페이지 미리 렌더링하기

- 페이지를 미리 렌더링하면 서버 cpu 리소스 절약 가능
- 넥스트에서 빌드시 getInitialProps 함수가 없는 페이지는 자동으로 미리 렌더링됨(getInitial 함수는 꼭 필요한 경우에만 작성하는게 좋음 >> next 12 환경은 조금 다른 것 같음
- \_app.js 파일에서 getInitialProps 함수를 정의하면 모든 페이지가 미리 렌더링되지 않음
- next export : 전체 페이지 미리 렌더링. 빌드 후에 실행해야함
  - 실행하면 루트 경로에 out 폴더 생성
  - 404.html : 에러 페이지 미리 렌더링
  - page.html : /page 요청에 대해 미리 렌더링
  - 404.html.html
  - \_next : next 빌드 후 생성되는 폴더인 .next 폴더에 있는 번들 파일과 같음
  - static : 이미지와 같은 정적 파일 모아 놓음
    - icon.png
- export 명령어 실행후 생성된 out 폴더만 있으면 서버에서 넥스트를 실행하지 않아도 정적 페이지 서비스 가능
  - 이때 서버주소/페이지.html로 접근해야 접근 가능
  - 서버 클린 url 설정하면 제어 가능
- node.config.js > exportPathMap 쿼리 파라미터를 활용해서 정적 페이지를 만들 수 있음
- next export 시 exportPathMap 옵션 사용
- 'page':{page:'page'} 로 설정하면 서버주소/page.html로 접속해야만 페이지 보여짐

## 동적 페이지 정적 페이지 동시에 서비스 하기

- 예제 따라하는 경우 프로덕션 환경에서 에러 발생하고 있음
- export NODE_ENV=dev 로 핵셜 가능

## styled components 사용

- css-in-js 방식을 사용하려면 서버사이드 렌더링 스타일 코드를 추출해서 html 코드에 삽입 필요
- styled-jsx 문법으로 작성한 코드 추출은 넥스트 내부의 \_document.js 파일에 있음
- \_document.js에서 스타일 코드를 추출해서 전달하는 로직 작성 필요
- 이때 서버, 클라이언트에서 생성하는 styled-component 해시값이 달라져 문제 발생
- styled-components babel-plugin-styled-components 로 해결 가능
- babelrc presets, plugin 설정 하여 해결 가능
