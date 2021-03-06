---
layout: post
title: "React Study"
date: 2022-04-08 13:40:30 +0530
categories: Javascript NodeJS
---

<br>

# React

## 리액트 개념

- 리액트가 등장하게 된 배경 / 동작 방식
  - 모델 <-> 뷰 간 양뱡한 바인딩을 통한 변화 대신 데이터가 바뀌면 뷰를 날리고 새로 만든다는 개념에서 출발
  - 이때 virtudal dom 사용
    - 자바스크립트로 이뤄진 가상 dom에 한번 렌더링하고 기존의 dom과 비교 후 변화가 필요한 곳에만 업데이트(브라우저 dom 반영)
    - 바뀐 데이터로 일단 화면 그리고 바뀐 부분만 찾아서 변화시켜줌
  - virtudal dom은 dom 변화를 최소화 시켜줌
- 리액트 컴포넌트
  - 리액트를 사용하면 웹 애플리케이션에서 사용하는 유저 인터페이스를 재사용 가능한 컴포넌트로 분리하여 작성하며 프로젝트 유지보수성을 우수하게 해줌
  - 컴포넌트 : 데이터를 넣으면 우리가 지정한 유저 인터페이스를 조립해서 보여주는 것
  - 만드는 방법 : 클래스 / 함수(stste, LifeCycle 이용 어려움) 를 이용하여 생성
  - 렌더링 : render() 함수가 호출된다는 의미임 (virtudal dom에 한번 그려줌)

## 리액트 프로젝트 구조

- node_modules : creat-react-app 구성하는 모든 패킷지 소스 코드가 존재
  package.json : creat-react-app 기본 패키지 외 추가로 설치된 \*라이브러리/패키지 정보 기록 (모든 패키지마다 존재)
- package-lock.json : 프로그래머가 관리할 필요가 없고 npm 이나 yarn이 알아서 관리해주는 파일들(lock파일은 해당 프로젝트에 설치한 패키지 , 그패키지와 관련된 모든 패키지의 버전정보를 포함)
- public
  - 가상 DOM을 위한 html파일 (빈 껍데기 파일) / CRA를 배포했을 때 실제 서버에 배포되는 디렉토리(<div id="root"><div>/index.html 포함)
  - mock date 관리하는 data 폴더 위치
- src
  - index.js : React 플젝의 시작점
  ```
  ReactDOM.render(<App />, document.getElementById('root'))
  ```
  - ReactDOM.render 함수의 인자는 두개이다. 첫 번째 인자는 화면에 보여주고 싶은 컴포넌트, 두 번째 인자는 화면에 보여주고 싶은 컴포넌트의 위치
  - assets : 미디어 파일
  - components : 공통 컴포넌트 관리(header, footer, nav)
  - pages : 페이지 단위의 컴포넌트 폴더로 구성(각 라우트들이 위치)
  - styles : css 파일 (GlobalStyle.js => css 초기화, theme.js => 공통으로 사용하는 css 속성 정의)
  - services : 자바스크립트 모듈 (로컬스토리지 모듈 등이 들어감)
  - utils : 상수/공통함수/유틸리티
  - context : context API로 프로젝트를 작업하는 경우 관련 API 저장
  - hoc : 함수형 컴포넌트를 사용하면서 커스텀 훅을 모듈화하여 담아놓는 폴더
  - store : 리덕스 사용시 관련 데이터 저장
- App.js
  - 현재 화면에 보여지는 초기 컴포넌트

## 리액트 문법

    - ES6 에서는, var 을 쓸 일이 없음. 값을 선언 후 바꿔야 할 땐 let, 그리고 바꾸지 않을 땐 const 를 사용
    * props
    - 부모 컴포넌트가 자식 컴포넌트에게 주는 값
    * state
    - 컴포넌트 내부에서 선언하며 내부에서 값 변경 가능

## jsx 문법

    - 태그는 꼭 닫아줘야함
    - Fragment 태그 : 감싸기 위해 새로운 div 생성이 맘에들지 않을 때 이용
    - const : 한 번 선언하고 바뀌지 않는 값 설정(es6부터 도입)
    - let : 바뀔 수 있는 값
    - var scope : 함수 / const,let scope : 블록 단위
    - JSX 내부에서 조건부 렌더링을 할 때는 보통 삼항 연산자를 사용하거나, AND 연산자를 사용 if문은 사용할 수 없음
    - 주석 태그 밖에는 {/**/} 태그 사이는 //
    - 이벤트 설정 시 이벤트명은 camelCase로 설정, 이벤트에 전달해주는 값은 함수명 (함수() 와 같이 전달하면 무한 함수 호출 발생)

## 리액트 주요 api

- LifeCycle API

* constructor
* componentWillMount : deprected, componentDidMount에서 처리 가능, 컴포넌트가 화면에 나타나기 직전에 호출
* componentDidMount : 컴포넌트가 화면에 나타나게 됐을 때 호출(외부 라이브러리 연동, 컴포넌트에서 필요로하는 데이터 요청, DOM 속성 읽기/변경)
* componentWillReceiveProps : deprecate, getDerivedStateFromProps로 대체. 컴포넌트가 새로운 props 를 받게됐을 때 호출(state 가 props 에 따라 변해야 하는 로직을 작성)
* static getDerivedStateFromProps() : props 로 받아온 값을 state 로 동기화 하는 작업을 해줘야 하는 경우에 사용
* shouldComponentUpdate : 불필요한 Virtual DOM 리렌더링 제어 가능. 기본적으로 true 를 반환. 조건에 따라 false를 반환하게 하여 render 함수를 호출하지 않도록 할 수 있음
* componentWillUpdate : deperecated, getSnapshotBeforeUpdate 로 대체. shouldComponentUpdate 에서 true 를 반환했을때만 호출, 애니메이션 효과 초기화/이벤트 리스너를 없애는 작업
* getSnapshotBeforeUpdate()
  : render(), getSnapshotBeforeUpdate(), getSnapshotBeforeUpdate(), componentDidUpdate 시점에 발생. DOM 변화가 일어나기 직전의 DOM 상태를 가져오고, 여기서 리턴하는 값은 componentDidUpdate 에서 3번째 파라미터로 받아올 수 있음
* componentDidUpdate : 컴포넌트에서 render() 를 호출하고난 다음에 발생
* componentWillUnmount : 컴포넌트 제거시 호출. 등록했던 이벤트, setTimeout, 외부 라이브러리 인스턴스 제거
* componentDidCatch : 에러 발생시 실행하도록 할 수 있는 api. 컴포넌트 자신의 render 함수에서 에러가 발생해버리는것은 잡아낼 수는 없지만, 그 대신에 컴포넌트의 자식 컴포넌트 내부에서 발생하는 에러들을 잡아낼 수 있음

## 간단 정리 사항

- 리액트를 통해 재사용 가능한 컴포넌트 생성/관리 가능
- props는 부모에게서 전달받는 데이터, state 는 자기 자신이 지니고 있는 데이터
- props 나 state 가 바뀌면 컴포넌트는 리렌더링함
- LifeCycle API 를 통해서 컴포넌트 마운트, 업데이트, 언마운트 전후로 처리 할 로직을 설정하거나 리렌더링을 막아줄 수 있음
- 라우팅 : 주소에 따라 다른 뷰를 보여줄 라이브러리도 필요물론 직접 구현할수도 있겠지만, 오픈소스를 사용하는것이 더 안정적이고 효율적입니다. 지금 리액트 생태계에서 주요 라우터는 두 종류가 있는데요, 하나는 react-router 입니다. 또 다른 라우터는 Next.js 인데요, 이건 서버사이드 렌더링까지 매우 편하게 해주는 프레임워크 입니다. 리액트 라우터, 코드 스플리팅, 그리고 서버사이드 렌더링 에서는 리액트 라우터 기초부터 리액트 프로젝트 코드 스플리팅까지 배워보실 수 있으니 참고하세요.

## Hook

1. 개념
   - 함수 컴포넌트에 Hook이 도입되면서 클래스 컴포넌트는 componentDidCatch를 사용할 때를 제외하고 모두 함수 컴폰넌트를 사용하여 구현 간으

## 관련 개념

1. SPA

   1. 개념

   - 단일 페이지 애플리케이션. 배포가 간단하며 네이티브 앱과 유사한 사용자 경험 제공이 가능
   - 웹 애플리케이션에 필요한 모든 정적 리소스를 최초 접근시 단 한 번만 다운로드.
   - 새로운 페이지 요청시 페이지 갱신에 필요한 데이터만을 JSON으로 전달받아 페이지 갱신.
   - 특정 부분만 Ajax를 통해 데이터 바인딩
   - 트래픽 감소 및 전체 페이지 다시 렌더링하지 않고 변경되는 부분만 갱신, 새로고침 발생 X

   2. 단점

   - 초기 구동 속도가 느림 : 웹 애플리케이션에 필요한 모든 정적 리소스를 최초 접근시 단 한 번 다운로드 함
   - SEO 이슈 : SPA는 일반적으로 서버 사이드 렌더링 방식이 아닌 자바스크립트 기반 비동기 모델의 클라이언트 사이드 렌더링(CSR) 방식으로 동작. CSR시 주소창 url 변경되지 않아 사용자 방문 히스토리 관리가 어려움. Angula, React 등의 SPA 프레임워크는 SSR 지원하는 기능이 존재. 크롬 등의 모던 브라우저는 SPA의 SEO 문제를 해결하고 있음

2. MPA
3. 개념

- multi page application. 여러 페이지로 구성. 사용자 클릭과 같은 인터렉션 발생 시 서버로부터 새로운 html을 받아와서 해당 링크로 이동하여 페이지 전체를 새로 렌더링

# bug fix

## 1. 슈퍼조인 홈페이지 헤더 그림자 효과

색상 -> opacity 변경 / 색상값 0(black -> 투명도만 변경)

## 2. homepage05 애니메이션 이슈 확인

고해상도인경우 이슈 발생

이미지가 2221 이상 커지지 않음

다른 애니메이션 적용 이미지에 비해 sizes 적용했더니 해상도별 적용 이미지가 없고 0\*0 px 로 노출
home_category 처럼 png 파일 넣어보면 될까?

## 3. 저해상도인경우 아이콘 짤리는 현상

화면 확대되는 경우 헤더 메인 화면 리액티브하게 만들어야함 >타블렛 해상도인경우 모바일처럼 세로 크기 키우도록 변경

## 4. tobe 수정사항

home02 두번재 icon block(일정-함깨할 일정 공유) 이거 수정 필요함.....!\_! 아마 함께..? 이거겠쥐?

<hr/><br>
1. 자바스크립트
2. Next.js
- 리액트에서 라우터 관리할 때 사용하는 라이브러리
