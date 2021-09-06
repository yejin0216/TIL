# webpack

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
  ```
  module.exports = {
    ...
    plugins: [
      new CleanWebpackPlugin(),
      new webpack.ProvidePlugin({ process: 'process/browser' }),
    ],
  }
  ```

## Loader

웹팩이 웹 애플리케이션을 해석할 때, 자바스크립트 파일이 아닌 웹 자원(HTML, CSS, Image, Font 등)을 변환할 수 있도록 도와주는 속성이다.

- 대표적인 로더 유형

  - babel loader
  - css loader : css
  - file loader : image, font

- 코드

```javascript
  module.export = {
    ...
    modules: {
      rules: [
        {
          test: /\.css$/, //로더를 적용할 파일 유형
          use: ['style-loader', 'css-loader'] //해당 파일에 적용할 로더 타입, 적용 순서는 오른쪽부터 왼쪽이다.
        }
      ]
    }
  }
```

- [Webpack 핸드북](https://joshua1988.github.io/webpack-guide/concepts/loader.html#%EC%9E%90%EC%A3%BC-%EC%82%AC%EC%9A%A9%EB%90%98%EB%8A%94-%EB%A1%9C%EB%8D%94-%EC%A2%85%EB%A5%98)

## Module Resolution
