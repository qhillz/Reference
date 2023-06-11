JavaScript에서 "on"으로 시작하는 메소드는 이벤트 핸들러(`event handler`)를 등록하거나 제거하는 데 사용됩니다. 이벤트 핸들러는 특정 이벤트가 발생할 때 실행되는 함수입니다.

모든 "on" 메소드를 설명하면 다음과 같습니다.

1. `onload`: 문서나 이미지 등이 로드될 때 실행됩니다.
2. `onunload`: 문서가 언로드될 때 실행됩니다.
3. `onfocus`: 요소가 포커스를 받을 때 실행됩니다.
4. `onblur`: 요소가 포커스를 잃을 때 실행됩니다.
5. `onsubmit`: 폼이 제출될 때 실행됩니다.
6. `onreset`: 폼이 리셋될 때 실행됩니다.
7. `onselect`: 텍스트 선택이 변경될 때 실행됩니다.
8. `onchange`: 요소의 값이 변경될 때 실행됩니다.
9. `onclick`: 요소가 클릭될 때 실행됩니다.
10. `ondblclick`: 요소가 더블클릭될 때 실행됩니다.
11. `onmouseover`: 마우스 포인터가 요소 위로 올라갈 때 실행됩니다.
12. `onmouseout`: 마우스 포인터가 요소에서 벗어날 때 실행됩니다.
13. `onmousedown`: 마우스 버튼이 눌러질 때 실행됩니다.
14. `onmouseup`: 마우스 버튼이 떼어질 때 실행됩니다.
15. `onmousemove`: 마우스 포인터가 움직일 때 실행됩니다.
16. `onkeydown`: 키가 눌러질 때 실행됩니다.
17. `onkeyup`: 키가 떼어질 때 실행됩니다.
18. `onkeypress`: 키가 입력될 때 실행됩니다.
19. `ontouchstart`: 터치가 시작될 때 실행됩니다.
20. `ontouchend`: 터치가 끝날 때 실행됩니다.
21. `ontouchmove`: 터치가 움직일 때 실행됩니다.
22. `onscroll`: 스크롤할 때 실행됩니다.
23. `onresize`: 윈도우나 프레임의 크기가 변경될 때 실행됩니다.
24. `onerror`: 에러가 발생할 때 실행됩니다.

위와 같은 "on" 메소드는 일반적으로 HTML 요소의 속성으로 지정됩니다. 예를 들어, `onclick` 이벤트 핸들러를 등록하려면 HTML 요소의 `onclick` 속성에 함수 이름을 할당하면 됩니다. 또한, `addEventListener()` 메소드를 사용하여 이벤트 핸들러를 등록할 수도 있습니다.