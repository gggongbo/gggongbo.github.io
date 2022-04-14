# Typescirpt

## 타입스크립트 연습 통해 공부 진행

- 관련 링크 : https://react.vlpt.us/using-typescript/01-practice.html

```
yarn global add typescript

tsc //ts 파일 js 파일로 컴파일
```

## tsconfig.js

- target : 컴파일된 코드가 어떤 환경에서 실행될지 정의
- module : 컴파일된 코드가 어떤 모듈 시스템 사용할지 정의. commonjs : export default Sampe -> export.default = helloWorld 로 변환, es2015인 경우 그대로 유지
- strict : 모든 타입 체킹 옵션 활성화
- esModuleInterop : commonjs 모듈 셩태로 이뤄진 파일을 es2015 모듈 형태로 불러올 수 있게 해줌
- outDir : 컴파일된 파일들이 저장되는 경로 지정

## 특징

- class constructor의 파라미터 쪽에 public 또는 private accessor를 사용하면 직접 하나하나 선언하는 작업 생략 가능

```
class Circle implements Shape {
  constructor(public radius: number) {
      //radius 변수 선언 없이 바로 사용 가능.
    this.radius = radius;
  }
```

- 같은 이름,타입의 프로퍼티를 갖는 경우 같은 객체로 인식되는 듯

interface Person {
name: string;
age?: number; // 물음표가 들어갔다는 것은, 설정을 해도 되고 안해도 되는 값이라는 것을 의미합니다.
}

const person: Person = {
name: '김사람',
age: 20
};

type Person2 = {
name: string;
age?: number; // 물음표가 들어갔다는 것은, 설정을 해도 되고 안해도 되는 값이라는 것을 의미합니다.
};

type People = Person2[];

const people: People = [person, person2]; //

## Type alias

- 클래스와 관련된 타입의 경우엔 interface 사용 권장
- 일반 객체 타입의 경우엔 type 사용해도 무방한데.. 일관성만 유지하면 된다고 함..

## Generics

- 제너릭은 타입스크립트에서 함수, 클래스, 인터페이스, type alias 를 사용하게 될때 여러 종류의 타입에 대해 호환 맞춰야 하는 상황에서 사용

```
function wrap<T>(param: T) {
  return {
    param,
  };
}

const wrapped = wrap(10);

//인터페이스 사용 예시
interface Items<T> {
  list: T[];
}

const items: Items<String> = {
  list: ["a", "b", "c"],
};

//타입에서 사용 예시
type Items<T> = {
  list: T[];
};

const items: Items<string> = {
  list: ['a', 'b', 'c']
};
```
