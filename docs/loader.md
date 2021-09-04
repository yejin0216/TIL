# 로더(loader)

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
          use: ['style-loader', 'css-loader'] // 해당 파일에 적용할 로더 타입, 적용 순서는 오른쪽부터 왼쪽이다.
        }
      ]
    }
  }
```

- [Webpack 핸드북](https://joshua1988.github.io/webpack-guide/concepts/loader.html#%EC%9E%90%EC%A3%BC-%EC%82%AC%EC%9A%A9%EB%90%98%EB%8A%94-%EB%A1%9C%EB%8D%94-%EC%A2%85%EB%A5%98)
