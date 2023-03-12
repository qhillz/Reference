https://ko.javascript.info/css-animations (아주 좋은 정보들.)

# css-transition

.transition-property



`transition-property` 프로퍼티엔 `left`, `margin-left`, `height`, `color` 같이 애니메이션 효과를 적용할 프로퍼티 목록을 정의합니다.

이때 주의할 점은 모든 프로퍼티에 애니메이션 효과를 적용할 수 없다는 사실입니다. 참고로 [흔히 사용되는 프로퍼티 대다수엔](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties) 애니메이션 효과를 적용할 수 있습니다.



## transition-duration

`transition-duration` 프로퍼티엔 애니메이션 효과를 얼마 동안 줄지를 설정합니다. 시간은 [CSS 시간 형식(CSS time format)](http://www.w3.org/TR/css3-values/#time)을 따라야 하는데, 초 단위(`s`)나 밀리초 단위(`ms`)를 사용할 수 있습니다.



## transition-delay

`transition-delay` 프로퍼티엔 애니메이션 효과가 *시작되기 전*에 얼마만큼의 지연 시간을 줄지 설정합니다. `transition-delay` 값을 `1s`로 설정하면 애니메이션 효과가 1초 후에 나타납니다.

`transition-delay`엔 음수 값도 넣을 수 있습니다. 값이 음수일 땐 애니메이션 효과가 중간부터 나타납니다. `transition-duration`을 `2s`, 지연 시간을 `-1s`로 설정하면 애니메이션 효과는 1초가 지난 후 1초 동안 지속됩니다.

CSS `translate` 프로퍼티와 지금까지 배운 내용을 사용해 `0`부터 `9`까지가 화면에 자연스럽게 나타나도록 해봅시다.



# translate()

The **`translate()`** [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) [function](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions) repositions an element in the horizontal and/or vertical directions. Its result is a [``](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function) data type.

![img](md-images/translate.png)

This transformation is characterized by a two-dimensional vector. Its coordinates define how much the element moves in each direction.

## [Syntax](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/translate#syntax)

```css
/* Single <length-percentage> values */
transform: translate(200px);
transform: translate(50%);

/* Double <length-percentage> values */
transform: translate(100px, 200px);
transform: translate(100px, 50%);
transform: translate(30%, 200px);
transform: translate(30%, 50%);
```



## transition-timing-function

`transition-timing-function` 프로퍼티를 사용해 timing 함수를 만들면 시간에 따라 애니메이션 효과를 어떻게 분배할지를 설정할 수 있습니다. 애니메이션 효과가 초반엔 천천히 나타나다가 나중엔 빠르게 나타나게 할 수 있고, 물론 이 반대도 가능합니다.

처음 이 프로퍼티를 접하면 애니메이션 프로퍼티 중 가장 복잡한 프로퍼티 같다고 느낄 수 있습니다. 그렇지만 시간을 조금 투자해 학습하면 매우 간단한 프로퍼티라는 생각이 들 겁니다.

`transition-timing-function` 프로퍼티 값엔 베지어 곡선(bezier curve)이나 단계(step)가 올 수 있습니다. 먼저 사용 빈도가 높은 베지어 곡선부터 알아봅시다.





# 베지어 곡선의 포인트

```css
transition: width 3s cubic-bezier(0, 0, .5, 2), height 3s cubic-bezier(0, 0, .5, 2);
```

cubic-bezier(0, 0, .5, 2) // x2,y2  x3,y3 
기본적으로 0,0 1,1 끝포인트는 정해져있고 (0번째 4번째 점)
내가 설정 할 수 있는 것은 (2번째 3번째 점이다.)

0초에서는 크기는 0, 0.5초에서는 크기가 2로 일반 크기 설정인 420px에서 벗어나게 되는 것이다.