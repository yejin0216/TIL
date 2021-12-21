# react

## Ref

Ref는 render 메서드에서 생성된 DOM 노드나 React 엘리먼트에 접근하는 방법을 제공한다.

- useRef

  - .current의 값을 변경시켜도 리랜더링되지 않는다. (컴포넌트 생애주기에는 포함됨)

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
