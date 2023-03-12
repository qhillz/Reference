# input type="radio"

**`radio`** 유형의 [``](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input) 요소는 보통 서로 관련된 옵션을 나타내는 라디오 버튼 콜렉션, **라디오 그룹**에 사용합니다. 임의의 그룹 내에서는 동시에 하나의 라디오 버튼만 선택할 수 있습니다. 라디오 버튼은 흔히 원형으로 그려지며, 선택한 경우 속을 채우거나 강조 표시를 합니다.



## [값](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input/radio#값)

The `value` attribute is a [`DOMString`](https://developer.mozilla.org/ko/docs/Web/API/DOMString) containing the radio button's value. The value is never shown to the user by their [user agent](https://developer.mozilla.org/ko/docs/Glossary/User_agent). Instead, it's used to identify which radio button in a group is selected.



### [라디오 그룹 정의하기](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input/radio#라디오_그룹_정의하기)

A radio group is defined by giving each of radio buttons in the group **the same [`name`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#attr-name)**. Once a radio group is established, selecting any radio button in that group automatically deselects any currently-selected radio button in the same group.

You can have as many radio groups on a page as you like, as long as each has its own unique `name`.

For example, if your form needs to ask the user for their preferred contact method, you might create three radio buttons, each with the `name` property set to `contact` but one with the [`value`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#attr-value) `email`, one with the value `phone`, and one with the value `mail`. The user never sees the `value` or the `name` (unless you expressly add code to display it).

