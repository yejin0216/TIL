# react

## CRA에서 bundle-analyzer 설정하기 

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
    
## Ref 

Ref는 render 메서드에서 생성된 DOM 노드나 React 엘리먼트에 접근하는 방법을 제공한다. 

- useRef
    - .current의 값을 변경시켜도 리랜더링되지 않는다. (컴포넌트 생애주기에는 포함됨)
