# flex

```html
<!doctype>
<html>
<head>
    <style>
        .container{
            background-color: powderblue;
            height:200px;
            display:flex;
            flex-direction:row;
        }
        .item{
            background-color: tomato;
            color:white;
            border:1px solid white;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
        <div class="item">4</div>
        <div class="item">5</div>
    </div>
</body>
</html>
```

flex를 적용하기 위해서는 container와 그 안의 item이 필요하다.
기본적으로 활용 가능한 property는 **container**에서 **flex-direction**.

block elem의 특징을 활용하여 row일때는, height 100%
column일때는 width 100% 상황을 볼 수 있다.

```css
/* The direction text is laid out in a line */
flex-direction: row;

/* Like <row>, but reversed */
flex-direction: row-reverse;

/* The direction in which lines of text are stacked */
flex-direction: column;

/* Like <column>, but reversed */
flex-direction: column-reverse;
```



```html
<!doctype>
<html>
<head>
    <style>
        .container{
            background-color: powderblue;
            height:200px;
            display:flex;
            flex-direction:row;
        }
        .item{
            background-color: tomato;
            color:white;
            border:1px solid white;         
        }
        .item:nth-child(1){
            flex-basis: 150px;
            flex-shrink: 1;
        }
        .item:nth-child(2){
            flex-basis: 150px;
            flex-shrink: 2;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
        <div class="item">4</div>
        <div class="item">5</div>
    </div>
</body>
</html>
```



**flex-basis 정의**(Item용)

The flex-basis CSS property **sets the initial main size of a flex item**. It sets the size of the content box unless otherwise set with box-sizing (컨텐츠 박스의 사이즈를 결정한다.)

flex-direction은 row이면 width를 기본적으로 설정해주고.

​							column이면 height를 기본적으로 설정해준다.



**flex-grow 정의**(Item용)

item이 얼마나 container의 여백을 몇 등분해서 가져갈 것이냐를 정함.

### Description

This property specifies how much of the remaining space in the flex container should be assigned to the item (the flex grow factor).

The [main size](https://www.w3.org/TR/css-flexbox/#main-size) is either width or height of the item which is dependent on the [`flex-direction`](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-direction) value.

The remaining space is the size of the flex container minus the size of all flex items' sizes together. If all sibling items have the same flex grow factor, then all items will receive the same share of remaining space, otherwise it is distributed according to the ratio defined by the different flex grow factors.



**flex-shrink 정의**(Item용)

The **`flex-shrink`** [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) property sets the flex shrink factor of a flex item. If the size of all flex items is larger than the flex container, items shrink to fit according to `flex-shrink`.

flex-shrink: 0; 

container가 item이 차지하는 공간보다 작아질때 해당 프로퍼티가 설정된 item은 content영역이 줄어들지 않는다.



전체 shrink 정의 된 값을 더해서, 예시로 1, 2가 있으면

컨테이너가 item이 가진 총 크기보다 작아진다면 (1/3) (2/3) 만큼 줄어들게 하겠다는 것이다.



**flex-wrap 정의**(Container용)

The **`flex-wrap`** [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) property sets whether flex items are forced onto one line or can wrap onto multiple lines. If wrapping is allowed, it sets the direction that lines are stacked.



**Align-items 정의**(Container용)

The [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) **`align-items`** property sets the [`align-self`](https://developer.mozilla.org/en-US/docs/Web/CSS/align-self) value on all direct children as a group. In Flexbox, it controls the alignment of items on the [Cross Axis](https://developer.mozilla.org/en-US/docs/Glossary/Cross_Axis). In Grid Layout, it controls the alignment of items on the Block Axis within their [grid area](https://developer.mozilla.org/en-US/docs/Glossary/Grid_Areas).

기본값은 Stretch임(이때 Item들은 Container에 packed됨.)
Container 내부의 Item들의 정렬을 의미함. (row면 열을, column이면 행을 기준.)

```css
/* Positional alignment */
/* align-items does not take left and right values */
align-items: center; /* Pack items around the center */
align-items: start; /* Pack items from the start */
align-items: end; /* Pack items from the end */
align-items: flex-start; /* Pack flex items from the start */
align-items: flex-end; /* Pack flex items from the end */
```

**align-self**(Item용)

Align-items로 지정되어 있는 상태에서 특정한 아이템만 예외적으로 다르게 align 시킬 수 있음.

```css
align-self: center; /* Put the item around the center */
align-self: start; /* Put the item at the start */
align-self: end; /* Put the item at the end */
align-self: self-start; /* Align the item flush at the start */
align-self: self-end; /* Align the item flush at the end */
align-self: flex-start; /* Put the flex item at the start */
align-self: flex-end; /* Put the flex item at the end */
```



**Justify-content 정의**(Container용)

The [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) **`justify-content`** property defines how the browser distributes space between and around content items along the [main-axis](https://developer.mozilla.org/en-US/docs/Glossary/Main_Axis) of a flex container, and the inline axis of a grid container.

**Container flex-direction을 기준으로 정렬 한다.**

```css
/* Positional alignment */
justify-content: center;     /* Pack items around the center */
justify-content: start;      /* Pack items from the start */
justify-content: end;        /* Pack items from the end */
justify-content: flex-start; /* Pack flex items from the start */
justify-content: flex-end;   /* Pack flex items from the end */
justify-content: left;       /* Pack items from the left */
justify-content: right;      /* Pack items from the right */
```



**Align-content 정의**(Container용)

space-between => 같은 행에 존재하는 item들을 그룹으로 묶어서 일정한 공간을 주어 배치시킨다. 



```
space-between
```

The items are evenly distributed within the alignment container along the cross axis. The spacing between each pair of adjacent items is the same. The first item is flush with the start edge of the alignment container in the cross axis, and the last item is flush with the end edge of the alignment container in the cross axis. 

**(첫번째 element의 시작 그리고 마지막 element 끝에 공백 없음)**

```
space-around
```

The items are evenly distributed within the alignment container along the cross axis. The spacing between each pair of adjacent items is the same. The empty space before the first and after the last item equals half of the space between each pair of adjacent items. 

**(첫번쨰 element 시작 공백과 마지막 element 후 공백이 일반 공백의 절반임)**

```
space-evenly
```

The items are evenly distributed within the alignment container along the cross axis. The spacing between each pair of adjacent items, the start edge and the first item, and the end edge and the last item, are all exactly the same. 

**(모든 공백이 다 같은 넓이를 가짐)**



**order 프로퍼티**(Item용)

Item의 순서를 적용시킬 수 있음.

order:1, order:2 이런식으로 적용시킴.



기본적으로 css에서 flex와 %는 window resize와 연동되게 된다.