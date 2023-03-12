app.js 기본적으로 랜더링할 최종파일.



여기서 state를 각 component에 넘겨줄 수 있고, component는 state를 수정가능함.

props만이 app.js에서 각 component에 넘겨주는 변수라고 보면 된다.



[e.target.name]



input type="hidden"



원본을 바꾸지 않는 테크닉, shouldComponentUpdate가 필요하다.



create-react-app .



# JSX 소개

JSX 표현식을 반환 할때

```react
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

어트리뷰트에 JavaScript 표현식을 삽입할 때 중괄호 주변에 따옴표를 입력하지 마세요. 따옴표(문자열 값에 사용) 또는 중괄호(표현식에 사용) 중 하나만 사용하고, 동일한 어트리뷰트에 두 가지를 동시에 사용하면 안 됩니다.



JSX는 HTML보다는 JavaScript에 가깝기 때문에, React DOM은 HTML 어트리뷰트 이름 대신 `camelCase` 프로퍼티 명명 규칙을 사용합니다.

예를 들어, JSX에서 `class`는 [`className`](https://developer.mozilla.org/ko/docs/Web/API/Element/className)가 되고 tabindex는 [`tabIndex`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/tabIndex)가 됩니다.



```react
const element = <img src={user.avatarUrl}></img>;
```

이런식으로, javascript는 중괄호를 써준다.



### JSX는 객체를 표현합니다.

Babel은 JSX를 `React.createElement()` 호출로 컴파일합니다.

다음 두 예시는 동일합니다.

```react
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```react
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

```react
// 주의: 다음 구조는 단순화되었습니다
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

위와 같이 객체 또한 만들 수 있음.



# 엘리먼트와 렌더링

엘리먼트는 React 앱의 가장 작은 단위입니다.

엘리먼트는 화면에 표시할 내용을 기술합니다.

```react
const element = <h1>Hello, world</h1>;
```

### DOM에 엘리먼트 렌더링하기

HTML 파일 어딘가에 `<div>`가 있다고 가정해 봅시다.

```
<div id="root"></div>
```

이 안에 들어가는 모든 엘리먼트를 React DOM에서 관리하기 때문에 이것을 “루트(root)” DOM 노드라고 부릅니다.

React로 구현된 애플리케이션은 일반적으로 하나의 루트 DOM 노드가 있습니다. React를 기존 앱에 통합하려는 경우 원하는 만큼 많은 수의 독립된 루트 DOM 노드가 있을 수 있습니다.

React 엘리먼트를 루트 DOM 노드에 렌더링하려면 둘 다 [`ReactDOM.render()`](https://ko.reactjs.org/docs/react-dom.html#render)로 전달하면 됩니다.



```react
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```



## 변경된 부분만 업데이트하기

React DOM은 해당 엘리먼트와 그 자식 엘리먼트를 이전의 엘리먼트와 비교하고 DOM을 원하는 상태로 만드는데 필요한 경우에만 DOM을 업데이트합니다.



## 함수 컴포넌트와 클래스 컴포넌트

컴포넌트를 정의하는 가장 간단한 방법은 JavaScript 함수를 작성하는 것입니다.

```react
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

이 함수는 데이터를 가진 하나의 “props” (props는 속성을 나타내는 데이터입니다) 객체 인자를 받은 후 React 엘리먼트를 반환하므로 유효한 React 컴포넌트입니다. 이러한 컴포넌트는 JavaScript 함수이기 때문에 말 그대로 “함수 컴포넌트”라고 호칭합니다.



또한 [ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes)를 사용하여 컴포넌트를 정의할 수 있습니다.

```
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

React의 관점에서 볼 때 위 두 가지 유형의 컴포넌트는 동일합니다.

class는 몇 가지 추가 기능이 있으며 이에 대해서는 [다음 장](https://ko.reactjs.org/docs/state-and-lifecycle.html)에서 설명합니다. 그때까지는 간결성을 위해 함수 컴포넌트를 사용하겠습니다. 함수 컴포넌트와 클래스 컴포넌트 둘 다 몇 가지 추가 기능이 있으며 이에 대해서는 [다음 장](https://ko.reactjs.org/docs/state-and-lifecycle.html)에서 설명합니다.



```react
function Welcome(props) {  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;ReactDOM.render(
  element,
  document.getElementById('root')
);
```

이 예시에서는 다음과 같은 일들이 일어납니다.

1. `<Welcome name="Sara" />` 엘리먼트로 `ReactDOM.render()`를 호출합니다.
2. React는 `{name: 'Sara'}`를 props로 하여 `Welcome` 컴포넌트를 호출합니다.
3. `Welcome` 컴포넌트는 결과적으로 `<h1>Hello, Sara</h1>` 엘리먼트를 반환합니다.
4. React DOM은 `<h1>Hello, Sara</h1>` 엘리먼트와 일치하도록 DOM을 효율적으로 업데이트합니다.

**주의: 컴포넌트의 이름은 항상 대문자로 시작합니다.**

React는 소문자로 시작하는 컴포넌트를 DOM 태그로 처리합니다. 예를 들어 `<div />`는 HTML div 태그를 나타내지만, `<Welcome />`은 컴포넌트를 나타내며 범위 안에 `Welcome`이 있어야 합니다.



처음에는 컴포넌트를 추출하는 작업이 지루해 보일 수 있습니다. 하지만 재사용 가능한 컴포넌트를 만들어 놓는 것은 더 큰 앱에서 작업할 때 두각을 나타냅니다. UI 일부가 여러 번 사용되거나 (`Button`, `Panel`, `Avatar`), UI 일부가 자체적으로 복잡한 (`App`, `FeedStory`, `Comment`) 경우에는 별도의 컴포넌트로 만드는 게 좋습니다.



React는 매우 유연하지만 한 가지 엄격한 규칙이 있습니다.

**모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수처럼 동작해야 합니다.**

물론 애플리케이션 UI는 동적이며 시간에 따라 변합니다. [다음 장](https://ko.reactjs.org/docs/state-and-lifecycle.html)에서는 “state”라는 새로운 개념을 소개합니다. React 컴포넌트는 state를 통해 위 규칙을 위반하지 않고 사용자 액션, 네트워크 응답 및 다른 요소에 대한 응답으로 시간에 따라 자신의 출력값을 변경할 수 있습니다.



```javascript
function sum(a, b) {
  return a + b;
}
```

이런 함수들은 [순수 함수](https://en.wikipedia.org/wiki/Pure_function)라고 호칭합니다. 입력값을 바꾸려 하지 않고 항상 동일한 입력값에 대해 동일한 결과를 반환하기 때문입니다.



# State와 생명주기

## 함수에서 클래스로 변환하기

다섯 단계로 `Clock`과 같은 함수 컴포넌트를 클래스로 변환할 수 있습니다.

1. `React.Component`를 확장하는 동일한 이름의 [ES6 class](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes)를 생성합니다.
2. `render()`라고 불리는 빈 메서드를 추가합니다.
3. 함수의 내용을 `render()` 메서드 안으로 옮깁니다.
4. `render()` 내용 안에 있는 `props`를 `this.props`로 변경합니다.
5. 남아있는 빈 함수 선언을 삭제합니다.



## 생명주기 메서드를 클래스에 추가하기

많은 컴포넌트가 있는 애플리케이션에서 컴포넌트가 삭제될 때 해당 컴포넌트가 사용 중이던 리소스를 확보하는 것이 중요합니다.

`Clock`이 처음 DOM에 렌더링 될 때마다 [타이머를 설정](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval)하려고 합니다. 이것은 React에서 “마운팅”이라고 합니다.

또한 `Clock`에 의해 생성된 DOM이 삭제될 때마다 [타이머를 해제](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/clearInterval)하려고 합니다. 이것은 React에서 “언마운팅”이라고 합니다.

컴포넌트 클래스에서 특별한 메서드를 선언하여 컴포넌트가 마운트되거나 언마운트 될 때 일부 코드를 작동할 수 있습니다.



주목해야 될점은 DOM에 컴포넌트가 탑재될때 발생하는 **마운팅**, DOM에 컴포넌트가 삭제될때 발생하는 **언마운팅**.



```react
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
  }

  componentWillUnmount() {
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

이러한 메서드들은 **“생명주기 메서드”**라고 불립니다.



`componentDidMount()` 메서드는 컴포넌트 출력물이 DOM에 렌더링 된 후에 실행됩니다. 이 장소가 타이머를 설정하기에 좋은 장소입니다.

```react
  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
```

`this` (`this.timerID`)에서 어떻게 타이머 ID를 제대로 저장하는지 주의해주세요.

`this.props`가 React에 의해 스스로 설정되고 `this.state`가 특수한 의미가 있지만, 타이머 ID와 같이 데이터 흐름 안에 포함되지 않는 어떤 항목을 보관할 필요가 있다면 자유롭게 클래스에 수동으로 부가적인 필드를 추가해도 됩니다.

`componentWillUnmount()` 생명주기 메서드 안에 있는 타이머를 분해해 보겠습니다.

```react
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
```



### clock 전체 코드

```react
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

이제 시계는 매초 째깍거립니다.

현재 어떤 상황이고 메서드가 어떻게 호출되는지 순서대로 빠르게 요약해 보겠습니다.

1. `<Clock />`가 `ReactDOM.render()`로 전달되었을 때 React는 `Clock` 컴포넌트의 constructor를 호출합니다. `Clock`이 현재 시각을 표시해야 하기 때문에 현재 시각이 포함된 객체로 `this.state`를 초기화합니다. 나중에 이 state를 업데이트할 것입니다.
2. React는 `Clock` 컴포넌트의 `render()` 메서드를 호출합니다. 이를 통해 React는 화면에 표시되어야 할 내용을 알게 됩니다. 그 다음 React는 `Clock`의 렌더링 출력값을 일치시키기 위해 DOM을 업데이트합니다.
3. `Clock` 출력값이 DOM에 삽입되면, React는 `componentDidMount()` 생명주기 메서드를 호출합니다. 그 안에서 `Clock` 컴포넌트는 매초 컴포넌트의 `tick()` 메서드를 호출하기 위한 타이머를 설정하도록 브라우저에 요청합니다.
4. 매초 브라우저가 `tick()` 메서드를 호출합니다. 그 안에서 `Clock` 컴포넌트는 `setState()`에 현재 시각을 포함하는 객체를 호출하면서 UI 업데이트를 진행합니다. **`setState()` 호출 덕분에 React는 state가 변경된 것을 인지하고 화면에 표시될 내용을 알아내기 위해 `render()` 메서드를 다시 호출합니다.** 이 때 `render()` 메서드 안의 `this.state.date`가 달라지고 렌더링 출력값은 업데이트된 시각을 포함합니다. React는 이에 따라 DOM을 업데이트합니다.
5. `Clock` 컴포넌트가 DOM으로부터 한 번이라도 삭제된 적이 있다면 React는 타이머를 멈추기 위해 `componentWillUnmount()` 생명주기 메서드를 호출합니다.



## State를 올바르게 사용하기

`setState()`에 대해서 알아야 할 세 가지가 있습니다.

### 직접 State를 수정하지 마세요

예를 들어, 이 코드는 컴포넌트를 다시 렌더링하지 않습니다.

```
// Wrong
this.state.comment = 'Hello';
```

대신에 `setState()`를 사용합니다.

```
// Correct
this.setState({comment: 'Hello'});
```

`this.state`를 지정할 수 있는 유일한 공간은 바로 constructor입니다.



### State 업데이트는 비동기적일 수도 있습니다.

React는 성능을 위해 여러 `setState()` 호출을 단일 업데이트로 한꺼번에 처리할 수 있습니다.

`this.props`와 `this.state`가 비동기적으로 업데이트될 수 있기 때문에 다음 state를 계산할 때 해당 값에 의존해서는 안 됩니다.

예를 들어, 다음 코드는 카운터 업데이트에 실패할 수 있습니다.

```
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

이를 수정하기 위해 객체보다는 함수를 인자로 사용하는 다른 형태의 `setState()`를 사용합니다. 그 함수는 **이전 state를 첫 번째 인자**로 받아들일 것이고, **업데이트가 적용된 시점의 props**를 두 번째 인자로 받아들일 것입니다.

```
// Correct
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

위에서는 [화살표 함수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/애로우_펑션)를 사용했지만, 일반적인 함수에서도 정상적으로 작동합니다.

```
// Correct
this.setState(function(state, props) {
  return {
    counter: state.counter + props.increment
  };
});
```

### 

### State 업데이트는 병합됩니다

`setState()`를 호출할 때 React는 제공한 객체를 현재 state로 병합합니다.

예를 들어, state는 다양한 독립적인 변수를 포함할 수 있습니다.

```
  constructor(props) {
    super(props);
    this.state = {
      posts: [],      comments: []    };
  }
```

별도의 `setState()` 호출로 이러한 변수를 독립적으로 업데이트할 수 있습니다.

```
  componentDidMount() {
    fetchPosts().then(response => {
      this.setState({
        posts: response.posts      });
    });

    fetchComments().then(response => {
      this.setState({
        comments: response.comments      });
    });
  }
```

병합은 얕게 이루어지기 때문에 `this.setState({comments})`는 `this.state.posts`에 영향을 주진 않지만 `this.state.comments`는 완전히 대체됩니다.



## 데이터는 아래로 흐릅니다

부모 컴포넌트나 자식 컴포넌트 모두 특정 컴포넌트가 유상태인지 또는 무상태인지 알 수 없고, 그들이 함수나 클래스로 정의되었는지에 대해서 관심을 가질 필요가 없습니다.

이 때문에 state는 종종 로컬 또는 캡슐화라고 불립니다. state가 소유하고 설정한 컴포넌트 이외에는 어떠한 컴포넌트에도 접근할 수 없습니다.

컴포넌트는 자신의 state를 자식 컴포넌트에 props로 전달할 수 있습니다.

```
<FormattedDate date={this.state.date} />
```

`FormattedDate` 컴포넌트는 `date`를 자신의 props로 받을 것이고 이것이 `Clock`의 state로부터 왔는지, `Clock`의 props에서 왔는지, 수동으로 입력한 것인지 알지 못합니다.

```react
function FormattedDate(props) {
  return <h2>It is {props.date.toLocaleTimeString()}.</h2>;
}
```



# 이벤트 처리하기

React 엘리먼트에서 이벤트를 처리하는 방식은 DOM 엘리먼트에서 이벤트를 처리하는 방식과 매우 유사합니다. 몇 가지 문법 차이는 다음과 같습니다.

- React의 이벤트는 소문자 대신 캐멀 케이스(camelCase)를 사용합니다.
- JSX를 사용하여 문자열이 아닌 함수로 이벤트 핸들러를 전달합니다.

예를 들어, HTML은 다음과 같습니다.

```html
<button onclick="activateLasers()">
  Activate Lasers
</button>
```

React에서는 약간 다릅니다.

```react
<button onClick={activateLasers}>  Activate Lasers
</button>
```

또 다른 차이점으로, React에서는 `false`를 반환해도 기본 동작을 방지할 수 없습니다. 반드시 `preventDefault`를 명시적으로 호출해야 합니다. 예를 들어, 일반 HTML에서 폼을 제출할 때 가지고 있는 기본 동작을 방지하기 위해 다음과 같은 코드를 작성할 수 있습니다.

```html
<form onsubmit="console.log('You clicked submit.'); return false">
  <button type="submit">Submit</button>
</form>
```

React에서는 다음과 같이 작성할 수 있습니다.

```react
function Form() {
  function handleSubmit(e) {
    e.preventDefault();    console.log('You clicked submit.');
  }

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Submit</button>
    </form>
  );
}
```



```react
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // 콜백에서 `this`가 작동하려면 아래와 같이 바인딩 해주어야 합니다.
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```

JSX 콜백 안에서 `this`의 의미에 대해 주의해야 합니다. JavaScript에서 클래스 메서드는 기본적으로 [바인딩](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)되어 있지 않습니다. `this.handleClick`을 바인딩하지 않고 `onClick`에 전달하였다면, 함수가 실제 호출될 때 `this`는 `undefined`가 됩니다.

이는 React만의 특수한 동작이 아니며, [JavaScript에서 함수가 작동하는 방식](https://www.smashingmagazine.com/2014/01/understanding-javascript-function-prototype-bind/)의 일부입니다. 일반적으로 `onClick={this.handleClick}`과 같이 뒤에 `()`를 사용하지 않고 메서드를 참조할 경우, 해당 메서드를 바인딩 해야 합니다.

`bind`를 호출하는 것이 불편하다면, 이를 해결할 수 있는 두 가지 방법이 있습니다. 실험적인 [퍼블릭 클래스 필드 문법](https://babeljs.io/docs/plugins/transform-class-properties/)을 사용하고 있다면, 클래스 필드를 사용하여 콜백을 올바르게 바인딩할 수 있습니다.



### 중요!!

클래스 필드 문법을 사용하고 있지 않다면, 콜백에 [화살표 함수](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)를 사용하는 방법도 있습니다.

```react
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // 이 문법은 `this`가 handleClick 내에서 바인딩되도록 합니다.    return (      <button onClick={() => this.handleClick()}>        Click me
      </button>
    );
  }
}
```

이 문법의 문제점은 `LoggingButton`이 렌더링될 때마다 다른 콜백이 생성된다는 것입니다. 대부분의 경우 문제가 되지 않으나, 콜백이 하위 컴포넌트에 props로서 전달된다면 그 컴포넌트들은 추가로 다시 렌더링을 수행할 수도 있습니다. 이러한 종류의 성능 문제를 피하고자, 생성자 안에서 바인딩하거나 클래스 필드 문법을 사용하는 것을 권장합니다.



# 조건부 렌더링

### Logical AND (&&)

The logical AND (`&&`) operator (logical conjunction) for a set of boolean operands will be `true` if and only if all the operands are `true`. Otherwise it will be `false`.

More generally, the operator returns the value of the first [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) operand encountered when evaluating from left to right, or the value of the last operand if they are all [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy).



### 논리 && 연산자로 If를 인라인으로 표현하기

JSX 안에는 중괄호를 이용해서 [표현식을 포함](https://ko.reactjs.org/docs/introducing-jsx.html#embedding-expressions-in-jsx) 할 수 있습니다. 그 안에 JavaScript의 논리 연산자 `&&`를 사용하면 쉽게 엘리먼트를 조건부로 넣을 수 있습니다.

```react
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 && <h2>You have {unreadMessages.length} unread messages.</h2>}</div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
);
```

JavaScript에서 `true && expression`은 항상 `expression`으로 평가되고 `false && expression`은 항상 `false`로 평가됩니다.

따라서 `&&` 뒤의 엘리먼트는 조건이 `true`일때 출력이 됩니다. **조건이 `false`라면 React는 무시하고 건너뜁니다.**

falsy 표현식을 반환하면 여전히 `&&` 뒤에 있는 표현식은 건너뛰지만 falsy 표현식이 반환된다는 것에 주의해주세요. 아래 예시에서, `<div>0</div>`이 render 메서드에서 반환됩니다.



### 컴포넌트가 렌더링하는 것을 막기

가끔 다른 컴포넌트에 의해 렌더링될 때 컴포넌트 자체를 숨기고 싶을 때가 있을 수 있습니다. 이때는 렌더링 결과를 출력하는 대신 `null`을 반환하면 해결할 수 있습니다.

아래의 예시에서는 `<WarningBanner />`가 `warn` prop의 값에 의해서 렌더링됩니다. prop이 `false`라면 컴포넌트는 렌더링하지 않게 됩니다.

```react
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

  return (
    <div className="warning">
      Warning!
    </div>
  );
}

class Page extends React.Component {
  constructor(props) {
    super(props);
    this.state = {showWarning: true};
    this.handleToggleClick = this.handleToggleClick.bind(this);
  }

  handleToggleClick() {
    this.setState(state => ({
      showWarning: !state.showWarning
    }));
  }

  render() {
    return (
      <div>
        <WarningBanner warn={this.state.showWarning} />
        <button onClick={this.handleToggleClick}>
          {this.state.showWarning ? 'Hide' : 'Show'}
        </button>
      </div>
    );
  }
}

ReactDOM.render(
  <Page />,
  document.getElementById('root')
);
```



# 리스트와 Key

먼저 JavaScript에서 리스트를 어떻게 변환하는지 살펴봅시다.

아래는 [`map()`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)함수를 이용하여 `numbers` 배열의 값을 두배로 만든 후 `map()`에서 반환하는 새 배열을 `doubled` 변수에 할당하고 로그를 확인하는 코드입니다.

```react
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);console.log(doubled);
```

이 코드는 콘솔에 `[2, 4, 6, 8, 10]`을 출력합니다.

React에서 배열을 [엘리먼트](https://ko.reactjs.org/docs/rendering-elements.html) 리스트로 만드는 방식은 이와 거의 동일 합니다.

### 여러개의 컴포넌트 렌더링 하기

엘리먼트 모음을 만들고 중괄호 `{}`를 이용하여 [JSX에 포함](https://ko.reactjs.org/docs/introducing-jsx.html#embedding-expressions-in-jsx) 시킬 수 있습니다.

아래의 JavaScript [`map()`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 함수를 사용하여 `numbers` 배열을 반복 실행합니다. 각 항목에 대해 `<li>` 엘리먼트를 반환하고 엘리먼트 배열의 결과를 `listItems`에 저장합니다.



```react
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>  <li>{number}</li>);
```

`listItems` 배열을 `<ul>`엘리먼트 안에 포함하고 [DOM에 렌더링합니다.](https://ko.reactjs.org/content/docs/rendering-elements.html#rendering-an-element-into-the-dom)

```react
ReactDOM.render(
  <ul>{listItems}</ul>,  document.getElementById('root')
);
```



```react
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>    <li>{number}</li>  );  return (
    <ul>{listItems}</ul>  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,  document.getElementById('root')
);
```

이 코드를 실행하면 리스트의 각 항목에 key를 넣어야 한다는 경고가 표시됩니다. “key”는 엘리먼트 리스트를 만들 때 포함해야 하는 특수한 문자열 어트리뷰트입니다. 다음 섹션에서 key의 중요성에 대해서 더 설명하겠습니다. 이제 `numbers.map()` 안에서 리스트의 각 항목에 `key`를 할당하여 키 누락 문제를 해결하겠습니다.



## Key

Key는 React가 어떤 항목을 변경, 추가 또는 삭제할지 식별하는 것을 돕습니다. key는 엘리먼트에 안정적인 고유성을 부여하기 위해 배열 내부의 엘리먼트에 지정해야 합니다.

```react
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>    {number}
  </li>
);
```

Key를 선택하는 가장 좋은 방법은 리스트의 다른 항목들 사이에서 해당 항목을 고유하게 식별할 수 있는 문자열을 사용하는 것입니다. 대부분의 경우 데이터의 ID를 key로 사용합니다.

```react
const todoItems = todos.map((todo) =>
  <li key={todo.id}>    {todo.text}
  </li>
);
```

렌더링 한 항목에 대한 안정적인 ID가 없다면 최후의 수단으로 항목의 인덱스를 key로 사용할 수 있습니다.

```react
const todoItems = todos.map((todo, index) =>
  // Only do this if items have no stable IDs  <li key={index}>    {todo.text}
  </li>
);
```

항목의 순서가 바뀔 수 있는 경우 key에 인덱스를 사용하는 것은 권장하지 않습니다. 이로 인해 성능이 저하되거나 컴포넌트의 state와 관련된 문제가 발생할 수 있습니다. Robin Pokorny’s가 작성한 글인 [인덱스를 key로 사용할 경우 부정적인 영향에 대한 상세 설명](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318)을 참고하시길 바랍니다. 리스트 항목에 명시적으로 key를 지정하지 않으면 React는 기본적으로 인덱스를 key로 사용합니다.



# Index as a key is an anti-pattern

So many times I have seen developers use the *index* of an item as its *key* when they render a list.

```
todos.map((todo, index) => (
    <Todo {...todo} key={index} />
  ));
}
```

It looks elegant and it does get rid of the warning (which was the ‘real’ issue, right?). What is the danger here?

> It may break your application and display wrong data!

Let me explain, a *key* is the only thing React uses to identify DOM elements. What happens if you push an item to the list or remove something in the middle? If the *key* is same as before React assumes that the DOM element represents the same component as before. But that is no longer true.



![image-20220327165623145](md-images/image-20220327165623145-16483677846181.png)



**예시: 올바른 Key 사용법**

```react
function ListItem(props) {
  // 맞습니다! 여기에는 key를 지정할 필요가 없습니다.  return <li>{props.value}</li>;}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // 맞습니다! 배열 안에 key를 지정해야 합니다.    <ListItem key={number.toString()} value={number} />  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

경험상 `map()` 함수 내부에 있는 엘리먼트에 key를 넣어 주는 게 좋습니다.

### 

React에서 key는 힌트를 제공하지만 컴포넌트로 전달하지는 않습니다. 컴포넌트에서 key와 동일한 값이 필요하면 다른 이름의 prop으로 명시적으로 전달합니다.

```react
const content = posts.map((post) =>
  <Post
    key={post.id}    id={post.id}    title={post.title} />
);
```

위 예시에서 `Post` 컴포넌트는 `props.id`를 읽을 수 있지만 `props.key`는 읽을 수 없습니다.

### 

# 폼

전반적으로 `<input type="text">`, `<textarea>` 및 `<select>` 모두 매우 비슷하게 동작합니다. 모두 제어 컴포넌트를 구현하는데 `value` 어트리뷰트를 허용합니다.

> 주의
>
> `select` 태그에 multiple 옵션을 허용한다면 `value` 어트리뷰트에 배열을 전달할 수 있습니다.
>
> ```react
> <select multiple={true} value={['B', 'C']}>
> ```



## 다중 입력 제어하기

여러 `input` 엘리먼트를 제어해야할 때, 각 엘리먼트에 `name` 어트리뷰트를 추가하고 `event.target.name` 값을 통해 핸들러가 어떤 작업을 할 지 선택할 수 있게 해줍니다.

아래는 예시입니다.

```react
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;
    this.setState({
      [name]: value    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"            
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"            
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}
```



주어진 input 태그의 name에 일치하는 state를 업데이트하기 위해 ES6의 [computed property name](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Object_initializer#속성_계산명) 구문을 사용하고 있습니다.

```react
this.setState({
  [name]: value});
```

ES5 코드는 아래와 같습니다.

```react
var partialState = {};
partialState[name] = value;
this.setState(partialState);
```

또한, `setState()`는 자동적으로 [현재 state에 일부 state를 병합](https://ko.reactjs.org/docs/state-and-lifecycle.html#state-updates-are-merged)하기 때문에 바뀐 부분에 대해서만 호출하면 됩니다.



# State 끌어올리기

먼저 `BoilingVerdict`라는 이름의 컴포넌트부터 만들어봅시다. 이 컴포넌트는 섭씨온도를 의미하는 `celsius` prop를 받아서 이 온도가 물이 끓기에 충분한지 여부를 출력합니다.

```react
function BoilingVerdict(props) {
  if (props.celsius >= 100) {
    return <p>The water would boil.</p>;  }
  return <p>The water would not boil.</p>;}
```

그 다음으로 `Calculator`라는 컴포넌트를 만들어보겠습니다. 이 컴포넌트는 온도를 입력할 수 있는 `<input>`을 렌더링하고 그 값을 `this.state.temperature`에 저장합니다.

또한 현재 입력값에 대한 `BoilingVerdict` 컴포넌트를 렌더링합니다.

```react
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};  }

  handleChange(e) {
    this.setState({temperature: e.target.value});  }

  render() {
    const temperature = this.state.temperature;    return (
      <fieldset>
        <legend>Enter temperature in Celsius:</legend>
        <input value={temperature} onChange={this.handleChange} />        <BoilingVerdict celsius={parseFloat(temperature)} />      
      </fieldset>
    );
  }
}
```

이제 `Calculator`가 분리된 두 개의 온도 입력 필드를 렌더링하도록 변경할 수 있습니다.

```react
class Calculator extends React.Component {
  render() {
    return (
      <div>
        <TemperatureInput scale="c" /><TemperatureInput scale="f" />      
      </div>
    );
  }
}
```

현재는 두 `TemperatureInput` 컴포넌트가 각각의 입력값을 각자의 state에 독립적으로 저장하고 있습니다.

```
class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};  }

  handleChange(e) {
    this.setState({temperature: e.target.value});  }

  render() {
    const temperature = this.state.temperature;    // ...
```

그러나 우리는 두 입력값이 서로의 것과 동기화된 상태로 있길 원합니다. 섭씨온도 입력값을 변경할 경우 화씨온도 입력값 역시 변환된 온도를 반영할 수 있어야 하며, 그 반대의 경우에도 마찬가지여야 합니다.

React에서 state를 공유하는 일은 그 값을 필요로 하는 컴포넌트 간의 가장 가까운 공통 조상으로 state를 끌어올림으로써 이뤄낼 수 있습니다. 이렇게 하는 방법을 “state 끌어올리기”라고 부릅니다. 이제 `TemperatureInput`이 개별적으로 가지고 있던 지역 state를 지우는 대신 `Calculator`로 그 값을 옮겨놓을 것입니다.

`Calculator`가 공유될 state를 소유하고 있으면 이 컴포넌트는 두 입력 필드의 현재 온도에 대한 “진리의 원천(source of truth)“이 됩니다. 이를 통해 두 입력 필드가 서로 간에 일관된 값을 유지하도록 만들 수 있습니다. 두 `TemperatureInput` 컴포넌트의 props가 같은 부모인 `Calculator`로부터 전달되기 때문에, 두 입력 필드는 항상 동기화된 상태를 유지할 수 있게 됩니다.

어떻게 동작하는지 차근차근 살펴봅시다.

우선, `TemperatureInput` 컴포넌트에서 `this.state.temperature`를 `this.props.temperature`로 대체할 것입니다. 지금은 `this.props.temperature`가 이미 존재한다고 가정해봅시다. 나중에는 이 값을 `Calculator`로부터 건네야 할 것입니다.



```react
 render() {
    // Before: const temperature = this.state.temperature;
    const temperature = this.props.temperature;    // ...
```

[props는 읽기 전용](https://ko.reactjs.org/docs/components-and-props.html#props-are-read-only)입니다. `temperature`가 지역 state였을 때는 그 값을 변경하기 위해서 그저 `TemperatureInput`의 `this.setState()`를 호출하는 걸로 충분했습니다. 그러나 이제 `temperature`가 부모로부터 prop로 전달되기 때문에 `TemperatureInput`은 그 값을 제어할 능력이 없습니다.

React에서는 보통 이 문제를 컴포넌트를 “제어” 가능하게 만드는 방식으로 해결합니다. DOM `<input>`이 `value`와 `onChange` prop를 건네받는 것과 비슷한 방식으로, 사용자 정의된 `TemperatureInput` 역시 `temperature`와 `onTemperatureChange` props를 자신의 부모인 `Calculator`로부터 건네받을 수 있습니다.

이제 `TemperatureInput`에서 온도를 갱신하고 싶으면 `this.props.onTemperatureChange`를 호출하면 됩니다.



# 합성 (Composition) vs 상속 (Inheritance)

### 컴포넌트에서 다른 컴포넌트를 담기

어떤 컴포넌트들은 어떤 자식 엘리먼트가 들어올 지 미리 예상할 수 없는 경우가 있습니다. 범용적인 ‘박스’ 역할을 하는 `Sidebar` 혹은 `Dialog`와 같은 컴포넌트에서 특히 자주 볼 수 있습니다.

이러한 컴포넌트에서는 특수한 `children` prop을 사용하여 자식 엘리먼트를 출력에 그대로 전달하는 것이 좋습니다.

```react
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}
```

이러한 방식으로 다른 컴포넌트에서 JSX를 중첩하여 임의의 자식을 전달할 수 있습니다.

```react
function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">Welcome</h1>
      <p className="Dialog-message">Thank you for visiting our spacecraft!</p>           </FancyBorder>
  );
}
```

`<FancyBorder>` JSX 태그 안에 있는 것들이 `FancyBorder` 컴포넌트의 `children` prop으로 전달됩니다. `FancyBorder`는 `{props.children}`을 `<div>` 안에 렌더링하므로 전달된 엘리먼트들이 최종 출력됩니다.

흔하진 않지만 종종 컴포넌트에 여러 개의 “구멍”이 필요할 수도 있습니다. 이런 경우에는 `children` 대신 자신만의 고유한 방식을 적용할 수도 있습니다.

```react
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}      </div>
      <div className="SplitPane-right">
        {props.right}      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={
        <Contacts />      }
      right={
        <Chat />      } />
  );
}
```



## 특수화

때로는 어떤 컴포넌트의 “특수한 경우”인 컴포넌트를 고려해야 하는 경우가 있습니다. 예를 들어, `WelcomeDialog`는 `Dialog`의 특수한 경우라고 할 수 있습니다.

React에서는 이 역시 합성을 통해 해결할 수 있습니다. 더 “구체적인” 컴포넌트가 “일반적인” 컴포넌트를 렌더링하고 props를 통해 내용을 구성합니다.

```react
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
    </FancyBorder>
  );
}

function WelcomeDialog() {
  return (
    <Dialog      title="Welcome"      message="Thank you for visiting our spacecraft!" />  );
}
```



합성은 클래스로 정의된 컴포넌트에서도 동일하게 적용됩니다.

```react
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
      {props.children}    </FancyBorder>
  );
}

class SignUpDialog extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.handleSignUp = this.handleSignUp.bind(this);
    this.state = {login: ''};
  }

  render() {
    return (
      <Dialog title="Mars Exploration Program"
              message="How should we refer to you?">
        <input value={this.state.login} onChange={this.handleChange} />        <button onClick={this.handleSignUp}>Sign Me Up!</button>      
      </Dialog>
    );
  }

  handleChange(e) {
    this.setState({login: e.target.value});
  }

  handleSignUp() {
    alert(`Welcome aboard, ${this.state.login}!`);
  }
}
```

리액트 합성(Composition) => 컴포넌트안에 element를 위치시켜 props.children으로 자식 컴포넌트에 합성 시키는 방식.



# React로 사고하기

React는 JavaScript로 규모가 크고 빠른 웹 애플리케이션을 만드는 가장 좋은 방법입니다. React는 Facebook과 Instagram을 통해 확장성을 입증했습니다.

React의 가장 멋진 점 중 하나는 앱을 설계하는 방식입니다. 이 문서를 통해 React로 상품들을 검색할 수 있는 데이터 테이블을 만드는 과정을 함께 생각해 봅시다.

## 목업으로 시작하기

JSON API와 목업을 디자이너로부터 받았다고 가정해 봅시다. 목업은 다음과 같을 것입니다.

![목업](md-images/thinking-in-react-mock.png)

JSON API는 아래와 같은 데이터를 반환합니다.

```
[
  {category: "Sporting Goods", price: "$49.99", stocked: true, name: "Football"},
  {category: "Sporting Goods", price: "$9.99", stocked: true, name: "Baseball"},
  {category: "Sporting Goods", price: "$29.99", stocked: false, name: "Basketball"},
  {category: "Electronics", price: "$99.99", stocked: true, name: "iPod Touch"},
  {category: "Electronics", price: "$399.99", stocked: false, name: "iPhone 5"},
  {category: "Electronics", price: "$199.99", stocked: true, name: "Nexus 7"}
];
```

## 1단계: UI를 컴포넌트 계층 구조로 나누기

우리가 할 첫 번째 일은 모든 컴포넌트(와 하위 컴포넌트)의 주변에 박스를 그리고 그 각각에 이름을 붙이는 것입니다. 디자이너와 함께 일한다면, 이것들을 이미 정해두었을 수 있으니 한번 대화해보세요! 디자이너의 Photoshop 레이어 이름이 React 컴포넌트의 이름이 될 수 있습니다.

하지만 어떤 것이 컴포넌트가 되어야 할지 어떻게 알 수 있을까요? 우리가 새로운 함수나 객체를 만들 때처럼 만드시면 됩니다. 한 가지 테크닉은 [단일 책임 원칙](https://ko.wikipedia.org/wiki/단일_책임_원칙)입니다. 이는 **하나의 컴포넌트는 한 가지 일을 하는게 이상적**이라는 원칙입니다. 하나의 컴포넌트가 커지게 된다면 이는 보다 작은 하위 컴포넌트로 분리되어야 합니다.

주로 JSON 데이터를 유저에게 보여주기 때문에, 데이터 모델이 적절하게 만들어졌다면, UI(컴포넌트 구조)가 잘 연결될 것입니다. 이는 UI와 데이터 모델이 같은 *인포메이션 아키텍처(information architecture)*를 가지는 경향이 있기 때문입니다. 각 컴포넌트가 데이터 모델의 한 조각을 나타내도록 분리해주세요.

![Diagram showing nesting of components](md-images/thinking-in-react-components.png)

다섯개의 컴포넌트로 이루어진 앱을 한번 봅시다. 각각의 컴포넌트에 들어간 데이터는 이탤릭체로 표기했습니다. 이미지의 숫자는 아래 숫자에 해당됩니다.

1. **`FilterableProductTable`(노란색)**: 예시 전체를 포괄합니다.
2. **`SearchBar`(파란색)**: 모든 *유저의 입력(user input)* 을 받습니다.
3. **`ProductTable`(연두색)**: *유저의 입력(user input)*을 기반으로 *데이터 콜렉션(data collection)*을 필터링 해서 보여줍니다.
4. **`ProductCategoryRow`(하늘색)**: 각 *카테고리(category)*의 헤더를 보여줍니다.
5. **`ProductRow`(빨강색)**: 각각의 *제품(product)*에 해당하는 행을 보여줍니다.

`ProductTable`을 보면 “Name” 과 “Price” 레이블을 포함한 테이블 헤더만을 가진 컴포넌트는 없습니다. 이 같은 경우, 데이터를 위한 독립된 컴포넌트를 생성할지 생성하지 않을지는 선택입니다. 이 예시에서는 `ProductTable`의 책임인 *데이터 컬렉션(data collection)*이 렌더링의 일부이기 때문에 `ProductTable`을 남겨두었습니다. 그러나 이 헤더가 복잡해지면 (즉 정렬을 위한 기능을 추가하는 등) `ProductTableHeader`컴포넌트를 만드는 것이 더 합리적일 것입니다.

이제 목업에서 컴포넌트를 확인하였으므로 이를 계층 구조로 나열해봅시다. 모형의 다른 컴포넌트 내부에 나타나는 컴포넌트는 계층 구조의 자식으로 나타냅니다.

- `FilterableProductTable`
  - `SearchBar`
  - `ProductTable`
    - `ProductCategoryRow`
    - `ProductRow`

## 2단계: React로 정적인 버전 만들기

[CodePen](https://codepen.io/)에서 [Thinking In React: Step 2](https://codepen.io/gaearon/pen/BwWzwm)를 살펴보세요.

이제 컴포넌트 계층구조가 만들어졌으니 앱을 실제로 구현해볼 시간입니다. **가장 쉬운 방법은 데이터 모델을 가지고 UI를 렌더링은 되지만 아무 동작도 없는 버전을 만들어보는 것입니다.** 이처럼 과정을 나누는 것이 좋은데 정적 버전을 만드는 것은 생각은 적게 필요하지만 타이핑은 많이 필요로 하고, 상호작용을 만드는 것은 생각은 많이 해야 하지만 타이핑은 적게 필요로 하기 때문입니다. 나중에 보다 자세히 살펴봅시다.

데이터 모델을 렌더링하는 앱의 정적 버전을 만들기 위해 다른 컴포넌트를 재사용하는 컴포넌트를 만들고 props 를 이용해 데이터를 전달해줍시다. props는 부모가 자식에게 데이터를 넘겨줄 때 사용할 수 있는 방법입니다. 정적 버전을 만들기 위해 **state를 사용하지 마세요**. state는 오직 상호작용을 위해, 즉 시간이 지남에 따라 데이터가 바뀌는 것에 사용합니다. 우리는 앱의 정적 버전을 만들고 있기 때문에 지금은 필요하지 않습니다.

앱을 만들 때 하향식(top-down)이나 상향식(bottom-up)으로 만들 수 있습니다. 다시 말해 계층 구조의 상층부에 있는 컴포넌트 (즉 `FilterableProductTable`부터 시작하는 것)부터 만들거나 하층부에 있는 컴포넌트 (`ProductRow`) 부터 만들 수도 있습니다. 간단한 예시에서는 보통 하향식으로 만드는 게 쉽지만 프로젝트가 커지면 상향식으로 만들고 테스트를 작성하면서 개발하기가 더 쉽습니다.

이 단계가 끝나면 데이터 렌더링을 위해 만들어진 재사용 가능한 컴포넌트들의 라이브러리를 가지게 됩니다. 현재는 앱의 정적 버전이기 때문에 컴포넌트는 `render()` 메서드만 가지고 있을 것입니다. 계층구조의 최상단 컴포넌트 (`FilterableProductTable`)는 prop으로 데이터 모델을 받습니다. 데이터 모델이 변경되면 `ReactDOM.render()`를 다시 호출해서 UI가 업데이트 됩니다. UI가 어떻게 업데이트되고 어디에서 변경해야하는지 알 수 있습니다. React의 **단방향 데이터 흐름(one-way data flow)** (또는 *단방향 바인딩(one-way binding*))는 모든 것을 모듈화 하고 빠르게 만들어줍니다.

이 단계를 실행하는 데 도움이 필요하다면 [공식 React 문서](https://ko.reactjs.org/docs/getting-started.html)를 참고하세요.

### 짧은 소개: Props vs State

React에는 두 가지 데이터 “모델”인 props와 state가 있습니다. 이 둘 사이의 차이점을 이해하는 것이 중요합니다. 차이점이 제대로 기억나지 않는다면 [공식 React 문서](https://ko.reactjs.org/docs/state-and-lifecycle.html)와 [자주 묻는 질문: state와 props의 차이점은 무엇인가요?](https://ko.reactjs.org/docs/faq-state.html#what-is-the-difference-between-state-and-props)까지 살펴보세요.

## 3단계: UI state에 대한 최소한의 (하지만 완전한) 표현 찾아내기

UI를 상호작용하게 만들려면 기반 데이터 모델을 변경할 수 있는 방법이 있어야 합니다. 이를 React는 **state**를 통해 변경합니다.

애플리케이션을 올바르게 만들기 위해서는 애플리케이션에서 필요로 하는 변경 가능한 state의 최소 집합을 생각해보아야 합니다. 여기서 핵심은 [중복배제](https://en.wikipedia.org/wiki/Don't_repeat_yourself)원칙입니다. 애플리케이션이 필요로 하는 가장 최소한의 state를 찾고 이를 통해 나머지 모든 것들이 필요에 따라 그때그때 계산되도록 만드세요. 예를 들어 TODO 리스트를 만든다고 하면, TODO 아이템을 저장하는 배열만 유지하고 TODO 아이템의 개수를 표현하는 state를 별도로 만들지 마세요. TODO 갯수를 렌더링해야한다면 TODO 아이템 배열의 길이를 가져오면 됩니다.

예시 애플리케이션 내 데이터들을 생각해봅시다. 애플리케이션은 다음과 같은 데이터를 가지고 있습니다.

- 제품의 원본 목록
- 유저가 입력한 검색어
- 체크박스의 값
- 필터링 된 제품들의 목록

각각 살펴보고 어떤 게 state가 되어야 하는 지 살펴봅시다. 이는 각 데이터에 대해 아래의 세 가지 질문을 통해 결정할 수 있습니다.

1. 부모로부터 props를 통해 전달됩니까? 그러면 확실히 state가 아닙니다.
2. 시간이 지나도 변하지 않나요? 그러면 확실히 state가 아닙니다.
3. 컴포넌트 안의 다른 state나 props를 가지고 계산 가능한가요? 그렇다면 state가 아닙니다.

제품의 원본 목록은 props를 통해 전달되므로 state가 아닙니다. 검색어와 체크박스는 state로 볼 수 있는데 시간이 지남에 따라 변하기도 하면서 다른 것들로부터 계산될 수 없기 때문입니다. 그리고 마지막으로 필터링된 목록은 state가 아닙니다. 제품의 원본 목록과 검색어, 체크박스의 값을 조합해서 계산해낼 수 있기 때문입니다.

결과적으로 애플리케이션은 다음과 같은 state를 가집니다.

- 유저가 입력한 검색어
- 체크박스의 값

## 4단계: State가 어디에 있어야 할 지 찾기

[CodePen](https://codepen.io/)에서 [Thinking In React: Step 4](https://codepen.io/gaearon/pen/qPrNQZ)를 살펴보세요.

좋습니다. 이제 앱에서 최소한으로 필요한 state가 뭔지 찾아냈습니다. 다음으로는 어떤 컴포넌트가 state를 변경하거나 **소유**할지 찾아야 합니다.

기억하세요: React는 항상 컴포넌트 계층구조를 따라 아래로 내려가는 단방향 데이터 흐름을 따릅니다. 어떤 컴포넌트가 어떤 state를 가져야 하는 지 바로 결정하기 어려울 수 있습니다. **많은 초보자가 이 부분을 가장 어려워합니다.** 아래 과정을 따라 결정해 보세요.

애플리케이션이 가지는 각각의 state에 대해서

- state를 기반으로 렌더링하는 모든 컴포넌트를 찾으세요.
- 공통 소유 컴포넌트 (common owner component)를 찾으세요. (계층 구조 내에서 특정 state가 있어야 하는 모든 컴포넌트들의 상위에 있는 하나의 컴포넌트).
- 공통 혹은 더 상위에 있는 컴포넌트가 state를 가져야 합니다.
- state를 소유할 적절한 컴포넌트를 찾지 못하였다면, state를 소유하는 컴포넌트를 하나 만들어서 공통 오너 컴포넌트의 상위 계층에 추가하세요.

이 전략을 애플리케이션에 적용해봅시다.

- `ProductTable`은 state에 의존한 상품 리스트의 필터링해야 하고 `SearchBar`는 검색어와 체크박스의 상태를 표시해주어야 합니다.
- 공통 소유 컴포넌트는 `FilterableProductTable`입니다.
- 의미상으로도 `FilterableProductTable`이 검색어와 체크박스의 체크 여부를 가지는 것이 타당합니다.

좋습니다. state를 `FilterableProductTable`에 두기로 했습니다. 먼저 인스턴스 속성인 `this.state = {filterText: '', inStockOnly: false}` 를 `FilterableProductTable`의 `constructor`에 추가하여 애플리케이션의 초기 상태를 반영합니다. 그리고 나서 `filterText`와 `inStockOnly`를 `ProductTable`와 `SearchBar`에 prop으로 전달합니다. 마지막으로 이 props를 사용하여 `ProductTable`의 행을 정렬하고 `SearchBar`의 폼 필드 값을 설정하세요.

이제 애플리케이션의 동작을 볼 수 있습니다. `filterText`를 `"ball"`로 설정하고 앱을 새로고침 해보세요. 데이터 테이블이 올바르게 업데이트 된 것을 볼 수 있습니다.

## 5단계: 역방향 데이터 흐름 추가하기

[CodePen](https://codepen.io/)에서 [Thinking In React: Step 5](https://codepen.io/gaearon/pen/LzWZvb)를 살펴보세요.

지금까지 우리는 계층 구조 아래로 흐르는 props와 state의 함수로써 앱을 만들었습니다. 이제 다른 방향의 데이터 흐름을 만들어볼 시간입니다. 계층 구조의 하단에 있는 폼 컴포넌트에서 `FilterableProductTable`의 state를 업데이트할 수 있어야 합니다.

React는 전통적인 양방향 데이터 바인딩(two-way data binding)과 비교하면 더 많은 타이핑을 필요로 하지만 데이터 흐름을 명시적으로 보이게 만들어서 프로그램이 어떻게 동작하는지 파악할 수 있게 도와줍니다.

4단계의 예시에서 체크하거나 키보드를 타이핑할 경우 React가 입력을 무시하는 것을 확인할 수 있습니다. 이는 `input` 태그의 `value` 속성이 항상 `FilterableProductTable`에서 전달된 state와 동일하도록 설정했기 때문입니다.

우리가 원하는 것이 무엇인지를 한번 생각해봅시다. 우리는 사용자가 폼을 변경할 때마다 사용자의 입력을 반영할 수 있도록 state를 업데이트하기를 원합니다. 컴포넌트는 그 자신의 state만 변경할 수 있기 때문에 `FilterableProductTable`는 `SearchBar`에 콜백을 넘겨서 state가 업데이트되어야 할 때마다 호출되도록 할 것입니다. 우리는 input에 onChange 이벤트를 사용해서 알림을 받을 수 있습니다. `FilterableProductTable`에서 전달된 콜백은 `setState()`를 호출하고 앱이 업데이트될 것입니다.
