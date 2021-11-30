# javascript

## Native

### IIFE (즉시실행함수)

- 정의되는 즉시 호출, 실행되는 함수이다.
- 함수 내부의 변수는 외부에서 접근할 수 없기 때문에 전역 스코프의 오염을 막을 수 있다.

```
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
