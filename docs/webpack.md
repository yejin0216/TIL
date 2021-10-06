# webpack

## Concept 

Webpack은 JavaScript 애플리케이션을 위한 정적 모듈 번들러이다. Webpack은 하나 이상의 진입점
(entry)에서 종속성 그래프를 빌드한 다음 프로젝트에 필요한 모든 모듈을 하나 이상의 번들(ouput)로 결합한다. 
 

- 핵심 개념 

  - Entry : 진입점, 의존하는 다른 모듈과 라이브러리를 찾아낼 수 있다. 
  - Output : 번들이 생성되는 위치와 이름을 가르킨다.  
  - [Loader](###Loader) : 웹팩은 JavaScript, JSON 파일만 이해한다. 로더를 사용하면 웹팩이 다른 유형의 파일을 처리할 수 있도록 종속성 그래프에 추가할 수 있는 [모듈](####모듈)로 **변환**한다. -> ***변환***이 목적
  - [Plugin](###Plugin) : 번들 최적화, 자산 관리, 환경 변수 주입 등 광범위한 작업 수행 
  - Mode 
  - Browser Compatibility 


- 작성 예시 (v.4부터는 옵션)

```javascript
module.exports = {
  entry: 'index.js', 
  output: {
    path: path.resolve(__dirname, 'dist'), //defualt: dist 
    filename: 'main.bundle.js'
  }, 
  modules: {
    rules: [
        {
          test: /\.css$/, //로더를 적용할 파일 유형
          use: ['style-loader', 'css-loader'] //적용할 로더 타입, 적용 순서는 오른쪽부터 왼쪽이다.
        }
    ]
  }
}
```
<br />

### Loader

웹팩이 웹 애플리케이션을 해석할 때, 자바스크립트 파일이 아닌 웹 자원(HTML, CSS, Image, Font 등)을 변환할 수 있도록 도와주는 속성이다.

- 대표적인 로더 유형

  - babel loader
  - css loader : css
  - file loader : image, font

<br />

### Plugin

<br />

### 모듈 
 
- 예시 
  - ES2015의 `import`
  - CommonJS의 `require()`
  - AMD `define`, `require`
  - css/sass/less 파일 내부의 `@import`
  - 스타일시트 `url()`, 또는 HTML `<img src=...>`


<br />

## Configuration

### Resolve

모듈을 해석하는 방식을 변경할 수 있다.
예를들어 `ìmport 'lodash'`를 호출할 때, resolve 옵션은 webpack이 'lodash'를 찾는 위치를 변경할 수 있다.

#### resolve.fallback

webpack5부터는 Node.js의 핵심모듈을 자동으로 폴리필하지 않는다. 브라우저에서 실행되는 코드는 npm에서 호환되는 모듈을 직접 설치하고, 포함시켜야 한다.

```javascript
module.exports = {
  ...
  resolve: {
    fallback: {
      assert: require.resolve('assert/'),
      os: require.resolve('os-browserify/browser'),
      path: require.resolve('path-browserify'),
      fs: false, //폴리필을 포함하지 않는 경우
    },
  },
}
```

- issue
  - 에러명 : Webpack 5 - Uncaught ReferenceError: process is not defined
  - 해결방법 : Provide Plugin을 사용해서 전역에 process 모듈을 자동으로 import한다.

```javascript
module.exports = {
  ...
  plugins: [
    new CleanWebpackPlugin(),
    new webpack.ProvidePlugin({ process: 'process/browser' }),
  ],
}
```