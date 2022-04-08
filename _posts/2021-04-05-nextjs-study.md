---
layout: post
title:  "Nextjs Study"
date:   2021-04-08 13:40:30 +0530
categories: Javascript NodeJS
---
<br>

# Next.js
## 개념

## 구성 요소
* router.tsx
* _app.tsx
* _document.tsx

## API 설명
* next.config.js

## ServerSide 렌더링
* 렌더링 사이클
 1. Next Server가 GET 요청을 받는다.
 2. 요청에 맞는 Page를 찾는다.
 3. _app.tsx의 getInitialProps가 있다면 실행한다.
 4. Page Component의 getInitialProps가 있다면 실행한다. pageProps들을 받아온다.
 5. document.tsx의 getInitialProps가 있다면 실행한다. pageProps들을 받아온다.
 6. 모든 props들을 구성하고, _app.js > page Component 순서로 rendering.
 7. 모든 Content를 구성하고 _document.js를 실행하여 html 형태로 출력한다.