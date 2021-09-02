# Document 

## document.activeElement 
DOM에서 현재 포커스 받은 Element 객체를 반환한다. 
```html
<body>
    <textarea id="textarea1">반갑습니다.</textarea>
    <input type="text" id="text1" />
</body>
<script>
    function getActiveElement() {
      document.getElementById("text1").value = document.activeElement.id; 
    }
    document.addEventListener("mouseup", getActiveElement, false); 
</script>
```