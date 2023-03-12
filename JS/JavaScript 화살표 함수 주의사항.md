## JavaScript 화살표 함수 주의사항

```javascript
const Button = () => (
    <button>Hello world</button>
)
```

[화살표 함수 - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/애로우_펑션)에 따르면 화살표 함수의 경우 **괄호()로 감싸진 부분**이 return 된다*(return문을 작성하지 않아도 return 됨)*.

**반면에** 중괄호{}로 감싸진 다음과 같은 함수는 return문이 없다면 *return 값을 반환하지 않는다.*

```javascript
const Button = () => {
    <button>Hello world</button>
}

console.log(Button); // undefined
```

따라서 **중괄호{}를 사용**하여 return 값을 반환하고자 하는 함수를 만드려면 다음과 같이 *return 문을 사용*하여 코드를 작성해야한다.

```javascript
const Button = () => {
    return <button>Hello world</button>
}
```



## 기본 구문

```javascript
(param1, param2, …, paramN) => { statements }
(param1, param2, …, paramN) => expression
// 다음과 동일함:  => { return expression; }

// 매개변수가 하나뿐인 경우 괄호는 선택사항:
(singleParam) => { statements }
singleParam => { statements }

// 매개변수가 없는 함수는 괄호가 필요:
() => { statements }
```

## 고급 구문

```javascript
// 객체 리터럴 표현을 반환하기 위해서는 함수 본문(body)을 괄호 속에 넣음:
params => ({foo: bar})

// 나머지 매개변수 및 기본 매개변수를 지원함
(param1, param2, ...rest) => { statements }
(param1 = defaultValue1, param2, …, paramN = defaultValueN) => { statements }

// 매개변수 목록 내 비구조화도 지원됨
var f = ([a, b] = [1, 2], {x: c} = {x: a + b}) => a + b + c;
f();  // 6
```



## The Compare Function

The purpose of the compare function is to define an alternative sort order.

The compare function should return a negative, zero, or positive value, depending on the arguments:

function(a, b){return a - b}

When the `sort()` function compares two values, it sends the values to the compare function, and sorts the values **according to the returned (negative, zero, positive) value.**

If the result is negative `a` is sorted before `b`.

If the result is positive `b` is sorted before `a`.

If the result is 0 no changes are done with the sort order of the two values.



# String.prototype.localeCompare()

The **`localeCompare()`** method returns a number indicating whether a reference string comes before, or after, or is the same as the given string in sort order.

