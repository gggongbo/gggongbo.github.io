# Superjoin 홈페이지 소스 분석

## 프로젝트 구조

1. 프로젝트 전체 구조

- next.js 프로젝트가 리액트 프로젝트를 감싼 구조

2. json config
   1. package.json
   - scipt 및 dependency 설정
   2. tsconfig.json
   - 넥스트 환경에서 타입스크립트 적용시 사용 가능. 프로젝트 루트에 이 파일 만들고, 개발모드로 재시작하면 typescript 관련 npm dependency 설치 가이드 됨
   - 타입스크립트 ts 파일 > js 변환할 때의 세부 설정이 가능
   - complilerOptions
     - target : 어떤 버전의 자바스크립트로 바꿔줄지 세팅
     - module : 자바스크립트 파일간 import 문법 구현시 어떤 문법 쓸지 세팅(commonjs를 값으로 가지면 require, es2015 혹은 esnext를 가지면 import 문법 사용)
   - 참고 내용 : https://codingapple.com/unit/typescript-tsconfig-json/
   - baseUrl : 서버에서 인식할 수 있는 루트 경로 지정
   - path : 절대 경로 지정이 가능
   ```
   "baseUrl": "./",
   "paths": {
     "~/*": ["./*"]
   } // import ./NavBar 구문 이용시 컴파일러가 경로 이해 가능
   ```
   3. next.config.json
   - nextjs 라우팅 설정 작성
   - redirects : 리다이렉트 설정
   - exportPathMap : 라우팅 경로 지정
   4. firebase.json
   - 호스팅 구성을 정의. firebase init 명령어로 생성 가능
   - 배포 경로 지정
   - 호스팅 구성 참고 내용 : https://firebase.google.com/docs/hosting/full-config?hl=ko
   - 기본 구성
   ```
   "hosting": {
       "public": "public",  // the only required attribute for Hosting
       "ignore": [
           "firebase.json",
           "**/.*", // files with a leading period should be hidden from the system
           "**/node_modules/**"
       ]
   }
   ```
   - hosting 프로퍼티
     - public 프로퍼티 : 파이어베이스 호스팅에 배포할 디렉토리 지정
     - ignore 프로퍼티 : 배포 시 무시할 파일 지정
     - cleanUrls 프로퍼티 : URL에 .html 확장자 포함 여부 제어. true 면 업로드된 파일 url에서 자동으로 .html 확장자 삭제. 도메인/~.html로 직접 접근해도 .html 없애줌
     - trailngSlash : 정적 콘텐츠 url에 후행 슬래시 포함 여부 제어(true면 후행 슬래시 추가, false면 삭제)
   - redirects 프로퍼티
     - 리디렉션 규칙 배열 포함(배열의 요소에는 source(호스팅 트리거 url 패턴), destination(브라우저가 새 요청 생성하는 정적 url), type(https 응답코드) 포함)
   - rewrites 프로퍼티
     - 여러 url에서 동일 콘텐츠 표시할때 사용
     - 존재하지 않는 파일/디렉토리에 대한 요청 시
       ```
       // Serves index.html for requests to files or directories that do not exist
       "rewrites": [ {
           "source": "**",
           "destination": "/index.html"
       } ] // 도메인/아무경로 입력 >> index.html 로 연결됨
       ```
     - 함수에 요청 전달, Cloud Run 컨테이너에 요청 전달할때도 사용 가능
     - 커스텀 도메인 동적 링크 만들 수 있음
   - headers 프로퍼티
     - 파일별 커스텀 응답 헤더 지정 가능
   - Glob 패턴
     - '\*\*' : 임의 하위 디렉터리의 모든 파일 또는 폴더와 일치합니다.
     - '\*' : public(배포시 루트로 설정된 디렉토리) 디렉터리 루트의 파일 및 폴더와만 일치합니다.
     - '\*_/._' — 임의 하위 디렉터리에서 .로 시작하는 모든 파일(일반적으로 .git과 같은 폴더에 있는 숨김 파일)과 일치합니다.
     - '**/node_modules/**' — node_modules 폴더의 임의 하위 디렉터리에 있는 모든 파일 또는 폴더와 일치합니다. 'node_modules' 폴더는 public 디렉터리의 임의 하위 디렉터리에 있을 수 있습니다.
     - '\*_/_.@(jpg|jpeg|gif|png)' — 임의 하위 디렉터리에서 정확히 .jpg, .jpeg, .gif 또는 .png 중 하나로 끝나는 모든 파일과 일치합니다.
   5. prettierrc.json
   - prettier 사용시 관련 설정 가능
3. styles
   - global.css : app.tsx의 css 설정 (여기서 매핑되는 html head body 태그는 document.tsx에서 찾을 수 있음. 어떻게 이게 가능한거지..?)
4. pages
   1. \_app.tsx
   - nextjs 커스텀 앱 구조 + 리액트 기본 구조가 jsx 안에 포함 + styled-component에 있는 themeprovider 테그 이용

```
_app.tsx
   <ThemeProvider theme={theme}> {/* them={them} : import한 theme 설정, them/index.ts에 export 해오는 theme을 받아옴 TheamProvider : styled-component의 wrapper component theme 속성값에는 공통적으로 정의한 color, media 객체 포함. 이를 이용해서 하위 컴포넌트에서 theme.media.mobile로 모바일 환경에서 적용해야하는 css 속성등 사용이 가능(하위 컴포넌트 미디어 쿼리에서 활용)*/}
      <Layout>
        <Component {...pageProps} /> {/* Component는 Layout의 하위 컴포넌트. Layout의 children 속성값에 들어가게 됨*/}
      </Layout>
    </ThemeProvider>

Layout.tsx
  <LayoutBlock>
      <Head>
        <title>Superjoin</title>
        <meta name="description" content="Superjoin" />
        <link rel="icon" href="/favicon.ico" />
      </Head>
      <Navbar />
      <MainBlock>{children}</MainBlock>
      <Footer />
    </LayoutBlock>

>> 합치면
<ThemeProvider>
  <LayoutBlock>
    <Head>
      <title>Superjoin</title>
      <meta name="description" content="Superjoin" />
      <link rel="icon" href="/favicon.ico"/>
    </Head>
    <Navbar />
    <MainBlock><Component {...pageProps} /><MainBlock/>
    <Footer />
  </LayoutBlock>
</ThemProvider>

수퍼조인 홈페이지 웹 어플리케이션의 구조
```

## 빌드

- next dev, next build, next start, next export, next deploy 등 명령어를 이용하며 next 프레임워크에서 알아서 빌드해주고 있음
- package.json의 script 선언으로 next -> yarn 명령어로 바꿔서 이용 가능 (왜 yarn으로 바꾸어줄까? 명령어 통일성을 위해서??>>)
- deploy 시 firebase와 연동되며 연동 관련 설정은 firebase.json에서 가능
- next 프로젝트 관련 다른 옵션, 설정 세팅시 next.config.js 이용 가능

## 빌드된 프로젝트 구조

1. 경로

- 프로젝트 root directory/out 으로 설정되어있음(firebase.json에 설정)

2. 404.html : 커스텀 404 not found 페이지

## 관련 개념

- next
- react
- react-dom
- styled-components
- typescript
