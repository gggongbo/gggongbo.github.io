# 리액트 네이티브는 무엇일까요

- 리액트 네이티브는 javascriptcore 내에서 동작
- 웹용으로 사용되는 동일한 리액트 라이브러리 사용 가능
- 메시지는 네이티브 플랫폼 api에 비동기적으로 보내짐. 성능 위해 배치로 수행
- html 요소인 컴포넌트 대신 모바일 플랫폼을 위해 구현된 컴포넌트를 제공

## 웹용 리액트와 차이점

- 렌더 타겟이 DOM이 아님
- 비동기 API 호출이 있음

## 모바일 브라우저 경험

- 사용자가 손가락으로 상호작용하기 시작>모바일 플랫폼에서는 제스처 시스템 탑재
- 리액트 네이티브는 제스처를 다루기에 더 적합
- 리액트 네이티브는 실제 플랫폼의 컴포넌트 사용>개발한 앱의 컴포넌트 업데이트 해야하는 문제가 해결됨

## creat react native app

- CRA처럼 react native에 대한 개발 환경 구축해주는 명령어

## 관련 명령어

- start : 목표 플랫폼 위한 네이티브 빌드 xxx. 개발을 위한 다양한 시뮬레이터용으로 앱을 효율적으로 빌드
- run ios
- run android
- test
- run eject

## Expo

- 리액트 네이티브 개발을 도와줄 도구
- 개발 시 실제 모바일 장치에서 앱을 보고 상호작용할 수 있도록 해줌
- 코드 변경시 실시간 재로딩도 지원

## 플렉스 박스

- 반응형 레이아웃 구현시 이용
- 컨테이너들은 방향을 갖고 있음

## 스타일 적용

- 리액트 네이티브 스타일 적용시 StyleSheet 객체 사용

```
const styled = StyleSheet.create({
    container : {
        flex : 1,
        justifyContent : 'center',
        backgroundColor : 'ghostwhite',
    },
    box : {
        width : 100
    }
})

```

## 화면 전환

- react-navigation 패키지 사용

```
//App.js
import {createStackNavigator} from 'react-navigation';
import Home from './Home';
import Settings from './Settings';

export default createStackNavigator(
    {Home,
    Settings},
    { initialRouteName : 'Home'}
);

//Home.js
import React from 'react';
import {View, Text, Button} from 'react-native';
import styles from './styles';

export default({navigation}) => (
    <View style]{styles.container}>
        <Text>Home Screen</Text>
        <Button
        title="Settings"
        onPress={()=> navigation.navigate('Settings')}> //Settings 화면으로 이동
    </View>
)

//Settings.js
import React from 'react';
import {View, Text, Button} from 'react-native';
import styles from './styles';

export default({navigateion}) => (
    <View style={styles.container}>
        <Text>Settings Screeb</Text>
        <Button title="Home"
        onPress={()=> navigation.navigate('Home')}>
)
```

- createStackNavigator(param1, param2, param3)
- 첫번째 인자는 탐색(라우트)될 수 있는 컴포넌트, 두 번째 인자는 제네릭 탐색 옵션을 위한 인자,
- 홈이 렌더링되는 기본 컴포넌트라고 지정

  ```
  naviagtion.navigate('Detail', {
  title: 'Thrid Item'.
  content: 'Thire Item Content',
  stock: 200}) //navigate 함수의 첫번째 인자는 이동하고 싶은 컴포넌트, 두번째는 라우트 인자로 객체의 속성값을 이동하는 화면에 전달해줄수 있음

  Detail 컴포넌트에서
  navigate.getParan('title') 로 전달해준 값 받아올 수 있음
  ```

354
382 385

프로그레스바 (progressviewios, progressbarandroid)

geolocation
MapView
TextInput : 텍스트 입력
Switch : 토글
DatePicker, TimePicker : 날짜/시간 입력 받기
Modal : 모달
Notification(안드로이드-토스트)
...

NetInfo : 네트워크 상태 변화 감지
AsyncStoreage API : 동기화할 데이터 저장. 513
