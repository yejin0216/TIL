# git

## href

### `#`, `#none` 차이

- `#` : 아무 것도 하지 않고 페이지 최상단으로 이동한다.
- `#none` : 아무 것도 실행하지 않고 페이지 최상단으로도 이동하지 않는다.

```html
<a href="#">링크</a> <a href="#none">링크</a>
```

- `{here}` : 클릭할 경우, name이 {here}인 곳으로 이동한다.

```
<a name="here" />
<br />
<a href="#here">위로 이동 </a>
```

## meta 태그 

### viewport-fit 

단순한 사각형 모양의 디스플레이가 아닌 디스플레이를 위한 속성으로 기본값은 `auto`이다. 

- `auto` : 콘텐츠를 모두 보여주도록 콘텐츠 축소 
- `cover` : viewport를 스크린 전체로 확대, `safe-area-inset-*`을 사용해서 padding을 조정할 수 있다.
