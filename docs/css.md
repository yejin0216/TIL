# css

### object-fit

`<img>`나 `<video>` 요소와 같은 대체 콘텐츠의 크기를 요소에 어떤 방식으로 조절해 맞출 것인지 지정한다.

#### fill

요소의 크기에 맞춰서 대체 콘텐츠의 크기를 조절한다. 가로세로비가 일치하지 않으면 콘텐츠가 늘어난다.

#### contain

가로세로비를 유지하면서, 요소의 콘텐츠 박스 내부에 들어가도록 크기를 맞춤 조절한다. 콘텐츠 박스 크기에 맞도록 하면서 가로세로비를 유지한다.

#### cover

가로세로비를 유지하면서, 요소의 콘텐츠 박스를 가득 채운다. 가로세로비가 일치하지 않으면 객체 일부가 잘려나간다.

#### none

크기를 조절하지 않는다.

#### scale-down

contain과 none 중에 크기가 더 작아지는 값을 택한다.