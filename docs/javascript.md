# javascript

## Native

### var의 문제점 

1. 함수 스코프 
    ```javascript
      function example {
        var i = 1;
      }
      console.log(i); //함수스코프를 벗어나서 참조에러 발생
    ```

    ```javascript
      for (var i=0; i<10; i++) {
        console.log(i); 
      }
      console.log(i); //10 출력, for문을 벗어나도 변수가 사라지지 않음 
    ```

    - var 변수의 스코프를 제한하기 위해 IIFE를 사용해서 스코프를 제한하기도 한다. 

2. 호이스팅 
    ```javascript
      console.log(myVar); //undefined 출력, 선언부가 끌어올려졌기 때문에 에러가 발생하지 않음
      var myVar = 1; 
    ```
  
3. 기타 
    ```javascript
      var myVar = 1; 
      var myVar = 2; //var 변수의 재정의가 가능하다. 
    ```

### const, let 
 
  1. 블록 스코프 
  ```javascript 
    if (true) {
      const i = 0; 
    }
    console.log(i); //참조 에러 발생, 블록을 벗어나면 변수를 사용할 수 없다. 
  ``` 

  ```javascript 
    let foo = "bar1"; 
    console.log(foo); //bar1
    if (true) {
      let foo = "bar2"; 
      console.log(foo); //bar2 
    }
    console.log(foo); //bar1
  ``` 
  
  2. 호이스팅 

  변수가 정의된 위치와 호이스팅된 위치 사이에서 사용하려면 에러가 발생한다. 이 구간을 임시적 사각지대(Temporal Dead Zone)라고 부른다. 
  ```javascript 
    console.log(foo); //참조 에러
    const foo = 1; 
  ```

  3. 기타 
    
     - const로 정의된 변수는 재할당 불가능하다. 단, const로 정의된 변수의 내부 속성값은 수정 가능하다. 
     - `immer`, `immutable.js`를 사용하면 객체의 내부 속성값을 수정할 수 없다.(변수 값 자체의 변경은 불가능함) 자바스크립트 내장함수를 이용하면 생성은 가능하고 수정은 차단할 수 있다. 
     ```javascript
      Object.preventExtenstions
      Object.seal
      Object.freeze
     ```

### IIFE (즉시실행함수)

- 정의되는 즉시 호출, 실행되는 함수이다.
- 함수 내부의 변수는 외부에서 접근할 수 없기 때문에 전역 스코프의 오염을 막을 수 있다.

  ```javascript
    ((a, b)=> {
      return a+b;
    }, (10, 20))
  ```

## Host

### document.activeElement

DOM에서 현재 포커스 받은 Element 객체를 반환한다.

```html
<body>
  <textarea id="textarea1">반갑습니다.</textarea>
  <input type="text" id="text1" />
</body>
<script>
  function getActiveElement() {
    document.getElementById('text1').value = document.activeElement.id;
  }
  document.addEventListener('mouseup', getActiveElement, false);
</script>
```
