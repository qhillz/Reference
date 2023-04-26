# Sass

Syntactically Awesome Style Sheets

CSS 전처리기이며 CSS의 문법을 인간이 쉽게 이해할 수 있는 구조로 변환하여 코딩에 가독성과 생산성을 높인 CSS문법 체계



```javascript
# NPM 을 통하여 node-sass 글로벌 설치
$ sudo npm install -g node-sass

# 컴파일하여 현재 디렉토리에 저장
$ node-sass style.scss -o .

# style.scss 파일에 변화가 있을 떄 마다 자동으로 리컴파일
$ node-sass style.scss -w -o .
```



## 문법예시

**Sass**

```css
$primary-color: #333;

body {
  background-color: $primary-color;
}
```

**CSS**

```css
body {
  background-color: #333;
}
```



### 1. Variable Scope (변수 범위)

Sass 의 변수엔 변수 범위가 있습니다.  변수를 특정 selector (선택자) 에서 선언하면 해당 selector 에서만 접근이 가능합니다.

**Sass**

```css
$primary-color: #333;

body {
  $primary-color: #eee;
  background-color: $primary-color;
}

p {
  color: $primary-color;
}
```

==> 변수 범위에 주의



**CSS**

```css
body {
  background-color: #eee;
}

p {
  color: #333;
}
```



위의 지역 변수범위에서 글로벌 변수 범위로의 확장을 이뤄내기 위해 아래와 같이 사용될 수 있다.

**Sass**

```css
$primary-color: #333;

body {
  $primary-color: #eee !global;;
  background-color: $primary-color;
}

p {
  color: $primary-color;
}
```

**CSS**

```css
body {
  background-color: #eee;
}

p {
  color: #eee;
}
```



## 2. Math Operators (수학 연산자)

Sass 에서는 수학 연산자들을 사용 할 수 있습니다. 지원되는 연산자들은 다음과 같다.



| Operator | Description    |
| :------- | :------------- |
| +        | addition       |
| -        | subtraction    |
| /        | division       |
| *        | multiplication |
| %        | modulo         |
| ==       | equality       |
| !=       | inequality     |



주의할 점은, `+`, `-` operator 를 사용 할 떄는 단위를 언제나 통일시켜야한다.

예를들어, 다음과 같은 코드는 오류가 발생한다 : `$box-width: 100% - 20px`

이런 작업을 해야한다면 css 의 [`calc()`](http://www.w3schools.com/cssref/func_calc.asp) 함수를 사용해야한다.

다음과 같은 식은 오류 없이 작동한다. `$box-width: 300px / 960px * 100%`



**Sass**

```css
.container { width: 100%; }


article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}
```

**CSS**

```css
.container {
  width: 100%;
}

article[role="main"] {
  float: left;
  width: 62.5%;
}

aside[role="complementary"] {
  float: right;
  width: 31.25%;
}
```



## 3. 색과 관련된 Built-in 함수



http://jackiebalzer.com/color ==> 여기서 참고 함수를 얻을 수 있음



```css
// ----
// Sass (v3.4.4)
// Compass (v1.0.1)
// ----

$buttonColor: #2ecc71;
$buttonDark: darken($buttonColor, 10%);
$buttonDarker: darken($buttonDark, 10%);

button {
  background: $buttonColor;
  border-radius: 3px;
  box-shadow: 0px 5px 0px $buttonDark;
  border: 0;
  color: white;
  font-size: 17px;
  padding: 10px 30px;
  display: inline-block;
  outline: 0;
  &:hover {
    background: $buttonDark;
    box-shadow: 0px 5px 0px $buttonDarker;
  }
  &:active {
    box-shadow: none;
    margin-top: 5px;
  }
}

body {
  text-align: center;
  padding-top: 100px;
}
```



## 4. Nesting (중첩)

CSS의 문법

```css
/* CSS */
.container {
    width: 100%;
}

.container h1 {
    color: red;
}
```



Sass 에선 이런식으로 작성하면 위와 같은 결과물을 얻을 수 있다.

```css
/* Sass */
.container {
    width: 100%;
    h1 {
        color: red;
    }
}
```



부모 선택자를 리퍼런스 할떄는 `&` 문자를 사용한다.

**Sass**

```css
a {
  color: black;
  &:hover {
    text-decoration: underline;
    color: gray;
  }
  &:visited {
    color: purple;
  }
}
```

**CSS**

```css
a {
  color: black;
}
a:hover {
  text-decoration: underline;
  color: gray;
}
a:visited {
  color: purple;
}
```



## 5. Extend (상속) 

Sass 에서 특정 선택자를 상속 할 때, `@extend` directive를 사용합니다.

**Sass**

```css
.box {
  border: 1px solid gray;
  padding: 10px;
  display: inline-block;
}

.success-box {
  @extend .box;
  border: 1px solid green;
}
```



**CSS**

```css
.box, .success-box {
  border: 1px solid gray;
  padding: 10px;
  display: inline-block;
}

.success-box {
  border: 1px solid green;
}
```



## 6. Mixin (믹스인)

Mixin 을 선언 할 떄는`@mixin` directive 를 사용하며, 이를 사용 할 때는 `@include` directive 를 사용합니다.

**Sass**

```css
@mixin headline ($color, $size) {
  color: $color;
  font-size: $size;
}

h1 {
  @include headline(green, 12px);
}
```

**CSS**

```css
h1 {
  color: green;
  font-size: 12px;
}
```

Mixin 을 응용하면 이런식으로도 사용 가능합니다:

**Sass**

```css
@mixin media($queryString){
    @media #{$queryString} {
      @content;
    }
}

.container {
    width: 900px;
    @include media("(max-width: 767px)"){
        width: 100%;
    }
}
```

**CSS**

```css
.container {
  width: 900px;
}
@media (max-width: 767px) {
  .container {
    width: 100%;
  }
}
```

워우워우… 갑자기 처음보는 표현들이 좀 나왔죠? 당황하지 마세요, 설명해드리겠습니다.

`#{ }` 표현은 특정 문자열을 따로 처리하지않고 **그대로 출력** 할 때 사용됩니다.

`@content` directive 를 사용하면 나중에 `@include` 하였을 때, 그 선택자 내부의 내용들이 `@conent` 부분에 나타나게됩니다.





-----

#### components/Button.js

```javascript
import React from 'react';
import classNames from 'classnames';
import './Button.scss';

function Button({ children, size, color, outline, fullWidth, ...rest }) {
  return (
    <button
      className={classNames('Button', size, color, { outline, fullWidth })}
      {...rest}
    >
      {children}
    </button>
  );
}

Button.defaultProps = {
  size: 'medium',
  color: 'blue'
};

export default Button;
```

이렇게 `...rest`를 사용해서 우리가 지정한 props 를 제외한 값들을 `rest` 라는 객체에 모아주고, `<button>` 태그에 `{...rest}` 를 해주면, `rest` 안에 있는 객체안에 있는 값들을 모두 `<button>` 태그에 설정을 해준답니다.

그래서, 만약에 App.js 에서 사용한 가장 첫번째 버튼에 `onClick` 을 설정해준다면,



#### App.js

```javascript
import React from 'react';
import './App.scss';
import Button from './components/Button';

function App() {
  return (
    <div className="App">
      <div className="buttons">
        <Button size="large" onClick={() => console.log('클릭됐다!')}>
          BUTTON
        </Button>
        <Button>BUTTON</Button>
        <Button size="small">BUTTON</Button>
      </div>
      <div className="buttons">
        <Button size="large" color="gray">
          BUTTON
        </Button>
        <Button color="gray">BUTTON</Button>
        <Button size="small" color="gray">
          BUTTON
        </Button>
      </div>
      <div className="buttons">
        <Button size="large" color="pink">
          BUTTON
        </Button>
        <Button color="pink">BUTTON</Button>
        <Button size="small" color="pink">
          BUTTON
        </Button>
      </div>
      <div className="buttons">
        <Button size="large" color="blue" outline>
          BUTTON
        </Button>
        <Button color="gray" outline>
          BUTTON
        </Button>
        <Button size="small" color="pink" outline>
          BUTTON
        </Button>
      </div>
      <div className="buttons">
        <Button size="large" fullWidth>
          BUTTON
        </Button>
        <Button size="large" color="gray" fullWidth>
          BUTTON
        </Button>
        <Button size="large" color="pink" fullWidth>
          BUTTON
        </Button>
      </div>
    </div>
  );
}

export default App;
```



#### components/Button.scss

```scss
$blue: #228be6;
$gray: #495057;
$pink: #f06595;

@mixin button-color($color) {
  background: $color;
  &:hover {
    background: lighten($color, 10%);
  }
  &:active {
    background: darken($color, 10%);
  }
  &.outline {
    color: $color;
    background: none;
    border: 1px solid $color;
    &:hover {
      background: $color;
      color: white;
    }
  }
}

.Button {
  display: inline-flex;
  color: white;
  font-weight: bold;
  outline: none;
  border-radius: 4px;
  border: none;
  cursor: pointer;

  // 사이즈 관리
  &.large {
    height: 3rem;
    padding-left: 1rem;
    padding-right: 1rem;
    font-size: 1.25rem;
  }

  &.medium {
    height: 2.25rem;
    padding-left: 1rem;
    padding-right: 1rem;
    font-size: 1rem;
  }

  &.small {
    height: 1.75rem;
    font-size: 0.875rem;
    padding-left: 1rem;
    padding-right: 1rem;
  }

  // 색상 관리
  &.blue {
    @include button-color($blue);
  }

  &.gray {
    @include button-color($gray);
  }

  &.pink {
    @include button-color($pink);
  }

  & + & {
    margin-left: 1rem;
  }

  &.fullWidth {
    width: 100%;
    justify-content: center;
    & + & {
      margin-left: 0;
      margin-top: 1rem;
    }
  }
}
```