# javascript

## General

### 얕은 비교

- 원시값을 비교할 때, 값을 비교한다.
  ```javascript
  const a1 = 'a';
  const a2 = 'a';
  console.log(a === b); // true, 원시 값 비교
  ```
- Object를 비교할 때, 속성이 아닌 reference를 비교한다.
  ```javascript
  const a1 = { a: 'a' };
  const a2 = { a: 'a' };
  console.log(a === b); // false, 주소 값 비교
  ```

### 얕은 복사

- 객체를 복사하면, 복사된 객체는 원본 객체와 같은 메모리 주소를 참조한다.

### 깊은 복사

- 객체를 복사할 때, 해당 객체와 인스턴스 변수까지 복해서 새 주소에 담는다.

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
   for (var i = 0; i < 10; i++) {
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
let foo = 'bar1';
console.log(foo); //bar1
if (true) {
  let foo = 'bar2';
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
   Object.preventExtenstions;
   Object.seal;
   Object.freeze;
   ```

### IIFE (즉시실행함수)

- 정의되는 즉시 호출, 실행되는 함수이다.
- 함수 내부의 변수는 외부에서 접근할 수 없기 때문에 전역 스코프의 오염을 막을 수 있다.

  ```javascript
  (a, b) => {
    return a + b;
  },
    (10, 20);
  ```

### 전개연산자

iterable 프로토콜을 따른다.

```javascript
console.log([...map.values(), ...map.entries()]);
```

### 제너레이터

iterator를 반환하는 함수이다.

```javascript
function* gen() {
  yield 1;
  yield 2;
  yield 3;
  return 100; //for 순회시에는 나오지 않는다. 마지막 done할 때 나오는 값이다.
}
let iter = gen();
console.log(iter[Symbol.iterator()] == iter); //welformed iterator
console.log(iter.next());
console.log(iter.next());
console.log(iter.next());
console.log(iter.next());

for (const a of gen()) console.log(a); //done:false만 취급
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

## Web API

### Element.getBoundingClientRect()

getBoundingClientRect 메서드는 엘리먼트 크기와 viewport에 상대적인 위치 정보를 제공하는 DOMRect 객체를 반환한다.

- 특이사항
  - padding, border를 포함한다.
  - viewport 왼쪽-상단(top-left)을 기준으로 위치, 사이즈 제공 (left, top, right, bottom, x, y, width, height)
  -

### Window.getComputedStyle()

getComputedStyle()는 인자로 받은 Element의 모든 CSS 속성값을 담은 객체를 반환한다.

### Intersection Observer API (교차 관찰자 API)

타겟 Element와 상위 Element 또는 최상위 document와 viewport 사이의 intersection 내의 변화를 비동기적으로 관찰하는 방법이다.

- 페이지가 스크롤 되는 도중에 발생하는 이미지나 다른 컨텐츠의 **지연 로딩**
- 스크롤 시에 더 많은 컨텐츠가 로드 및 렌더링되는 **infinite scroll 구현**
- 사용자에게 결과가 표시되는 여부에 따라 작업이나 애니메이션을 수행할지 여부를 결정
- 광고 수익을 계산하기 위한 용도로 광고의 가시성 보고

Intersection Observer API는 감시하려는 Element가 viewport에 들어가거나 나갈 때, 또는 요청한 부분만큼 두 Element의 교차 부분이 변경될 때마다 콜백 함수를 등록할 수 있게 한다. 즉, **사이트는 요소이 교차를 지켜보기 위해 메인 스레드를 사용할 필요가 없고 브라우저는 원하는 대로 교차 영역을 최적화할 수 있다.**

```javascript
const callback = (entries, observer) => {
  entries.forEach(entry => {
    ...
  });
}
const options = {
  root: document.querySelector('#scrollArea'),
  rootMargin: '0px',
  threshold: 1.0, //root에 지정요소가 100% 보여질 때 콜백이 호출된다.
};
const observer = new IntersectionObserver(callback, options);

const target = document.querySelector('#listItem');
observer.observe(target);
```

[참고자료 MDN 문서](https://developer.mozilla.org/ko/docs/Web/API/Intersection_Observer_API)
