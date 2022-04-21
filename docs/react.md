# react

## Ref

Ref는 render 메서드에서 생성된 DOM 노드나 React 엘리먼트에 접근하는 방법을 제공한다.

- useRef

  - .current의 값을 변경시켜도 리랜더링되지 않는다. (컴포넌트 생애주기에는 포함됨)

## Hooks

### useSelector

## CRA

### bundle-analyzer 설정하기

[cra-bundle-analyzer](https://www.npmjs.com/package/cra-bundle-analyzer) 를 설치한 뒤 npx로 실행한다.

- 설치
  ```bash
  # NPM
  npm install --save-dev cra-bundle-analyzer
  # Yarn
  yarn add -D cra-bundle-analyzer
  ```
- 실행
  ```bash
  npx cra-bundle-analyzer
  ```

### IE 적용하기

- [브라우저 점유율](https://www.koreahtml5.kr/front/stats/browser/browserUseStats.do)

- IE 적용방법
  - [react-app-polyfill](https://github.com/facebook/create-react-app/blob/main/packages/react-app-polyfill/README.md)을 사용
    - 스크립트 삽입
    ```javascript
    // These must be the first lines in src/index.js
    import 'react-app-polyfill/ie11';
    import 'react-app-polyfill/stable';
    import React from 'react';
    ```
    - react-script 버전 다운그레이드
    - package.json 수정
    ```json
    "browserslist": {
        "production": [
        "ie 11", // 추가
        ">0.2%",
        "not dead",
        "not op_mini all"
        ],
        "development": [
        "ie 11", // 추가
        "last 1 chrome version",
        "last 1 firefox version",
        "last 1 safari version"
        ]
    }
    ```
    - node_modules/.cache 삭제
  - babel 수준에서 마이크로 세팅
  - [기타] [Babel7과 corejs3 설정으로 전역 오염 없는 폴리필 사용하기](https://tech.kakao.com/2020/12/01/frontend-growth-02)

## Redux

### 용어

#### Action

`type` 필드를 가지고 있는 자바스크립트 객체이다. `type` 필드는 액션에 대한 설명이고, 추가적인 정보는 `payload`에 담는다.

```javascript
const addTodoAction = { type: 'todos/todoAdded', payload: 'Buy Milk' };
```

#### Action Creator

액션 객체를 생성하거나 반환하는 함수이다. 보통 Action Creator를 사용해서 작업하기 때문에 매번 반복해서 Action 객체를 작성할 필요가 없다.

```javascript
const addTodo = text => {
  return {
    type: 'todos/todoAdded',
    payload: text,
  };
};
```

#### Reducer

`current state`와 `action` 객체를 받아서 새로운 `new state`를 반환한다. `(state, action) => newState`

- 특이사항
  - `current state`와 `action`에 의해서만 `new state`를 생성한다.
  - `current state`는 불변객체이다. `new state`는 `current state`를 복제해서 만든다.
  - side effect(예. 비동기, 랜덤 값 계산) 등은 절대 해서 안된다.

#### Store

Redux 앱의 state가 모여있는 저장소이다.

#### Dispatch

Redux Store 안의 state는 오직 `Store.dispatch()`로만 수정할 수 있다.

```javascript
const addTodo = text => {
  return {
    type: 'todos/todoAdded',
    payload: text,
  };
};

store.dispatch(addTodo('Buy Milk'));
```

#### Selector

store에서 state를 추출하는 함수이다.
