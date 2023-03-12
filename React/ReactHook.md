Class스타일의 component에서는 this.state = ... 와 같이 state를 정의할 수 있었지만, function에서는 그러지 못하였다.
고로 function에 state를 추가시키는 스펙을 도입했는데 이것이 StateHook이다.

var [_date, Setdate]  = useState(초기값);

var _date = 초기값, Setdate는 function으로 var_date를 control한다.



Note

You might be wondering: why is `useState` not named `createState` instead?

“Create” wouldn’t be quite accurate because the state is only created the first time our component renders. During the next renders, `useState` gives us the current state. Otherwise it wouldn’t be “state” at all! There’s also a reason why Hook names *always* start with `use`. We’ll learn why later in the [Rules of Hooks](https://reactjs.org/docs/hooks-rules.html).

Setstate가 일어나게 되면 컴포넌트가 re-render됨.