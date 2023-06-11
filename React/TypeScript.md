# TypeScript



### `noImplicitAny`

몇몇 경우에서 TypeScript는 값의 타입을 추론하지 않고 가장 관대한 타입인 `any`로 간주한다는 사실을 기억하시기 바랍니다. 이는 최악의 경우는 아닙니다. 어쨌든, 타입을 `any`로 간주하는 것은 일반적인 JavaScript에서는 당연한 일이기도 합니다.

하지만, `any`를 사용하면 애초에 TypeScript를 사용하는 이유가 무색해지는 경우가 많습니다. 프로그램에서 타입을 더 구체적으로 사용할수록, 더 많은 유효성 검사와 도구 기능을 사용할 수 있으며, 이는 곧 코드 상에서 보다 적은 버그를 만나게 된다는 의미입니다. `noImplicitAny` 플래그를 활성화하면 타입이 `any`로 암묵적으로 추론되는 변수에 대하여 오류를 발생시킵니다.

### `strictNullChecks`

`null`과 `undefined`와 같은 값은 다른 타입의 값에 할당할 수 있는 것이 기본 동작입니다. 이는 코드 작성을 쉽게 만들어주지만, `null`과 `undefined`의 처리를 잊는 것은 세상의 셀 수 없이 많은 버그들의 원인입니다. 혹자는 이를 [백만 불 짜리 실수](https://www.youtube.com/watch?v=ybrQvs4x0Ps)라고 일컫기도 합니다! `strictNullChecks` 플래그는 `null`과 `undefined`를 보다 명시적으로 처리하며, `null` 및 `undefined` 처리를 *잊었는지* 여부를 걱정하는 데에서 우리를 *해방시켜* 줍니다.



## 변수에 대한 타입 표기

`const`, `var`, 또는 `let` 등을 사용하여 변수를 선언할 때, 변수의 타입을 명시적으로 지정하기 위하여 타입 표기를 추가할 수 있으며 이는 선택 사항입니다.

```react
let myName: string = "Alice";Try
```

> TypeScript는 `int x = 0;`과 같이 “타입을 왼쪽에 쓰는” 식의 표기법을 사용하지 않습니다. 타입 표기는 항상 타입의 대상 *뒤쪽에* 위치합니다.

하지만 대부분의 경우, 타입 표기는 필요하지 않습니다. 가능하다면 TypeScript는 자동으로 코드 내의 있는 타입들을 *추론*하고자 시도합니다. 예를 들어, 변수의 타입은 해당 변수의 초깃값의 타입을 바탕으로 추론됩니다.

```react
// 타입 표기가 필요하지 않습니다. 'myName'은 'string' 타입으로 추론됩니다.
let myName = "Alice";Try
```

대부분의 경우 추론 규칙을 명시적으로 학습하지 않아도 됩니다. 이제 막 TypeScript를 시작하는 단계라면, 가능한 타입 표기를 적게 사용하도록 해보세요. 코드 흐름을 완전히 파악하는 데에 타입이 그다지 많이 필요하지 않다는 사실에 놀라실 겁니다.



## 함수

함수는 JavaScript에서 데이터를 주고 받는 주요 수단입니다. TypeScript에서는 함수의 입력 및 출력 타입을 지정할 수 있습니다.

### 매개변수 타입 표기

함수를 선언할 때, 함수가 허용할 매개변수 타입을 선언하기 위하여 각 매개변수 뒤에 타입을 표기할 수 있습니다. 매개변수 타입은 매개변수 이름 뒤에 표기합니다.

```react
// 매개변수 타입 표기
function greet(name: string) {
  console.log("Hello, " + name.toUpperCase() + "!!");
}Try
```

매개변수에 타입이 표기되었다면, 해당 함수에 대한 인자는 검사가 이루어집니다.

```react
// 만약 실행되면 런타임 오류가 발생하게 됩니다!
greet(42);Argument of type 'number' is not assignable to parameter of type 'string'.Argument of type 'number' is not assignable to parameter of type 'string'.Try
```

> 매개변수에 타입을 표기하지 않았더라도, 여전히 TypeScript는 올바른 개수의 인자가 전달되었는지 여부를 검사합니다.

### 반환 타입 표기

반환 타입 또한 표기할 수 있습니다. 반환 타입은 매개변수 목록 뒤에 표기합니다.

```react
function getFavoriteNumber(): number {
  return 26;
}Try
```

변수의 타입 표기와 마찬가지로, 반환 타입은 표기하지 않아도 되는 것이 일반적입니다. 왜냐하면 TypeScript가 해당 함수에 들어있는 `return` 문을 바탕으로 반환 타입을 추론할 것이기 때문입니다. 위 예시에서 사용된 타입 표기는 큰 의미를 갖지 않습니다. 때에 따라 문서화를 목적으로, 또는 코드의 잘못된 수정을 미연에 방지하고자, 혹은 지극히 개인적인 선호에 의하여 명시적인 타입 표기를 수행하는 코드도 존재합니다.





### 익명 함수

익명 함수는 함수 선언과는 조금 다릅니다. 함수가 코드상에서 위치한 곳을 보고 해당 함수가 어떻게 호출될지 알아낼 수 있다면, TypeScript는 해당 함수의 매개 변수에 자동으로 타입을 부여합니다.

아래는 그 예시입니다.

```react
// 아래 코드에는 타입 표기가 전혀 없지만, TypeScript는 버그를 감지할 수 있습니다.
const names = ["Alice", "Bob", "Eve"];
 
// 함수에 대한 문맥적 타입 부여
names.forEach(function (s) {
  console.log(s.toUppercase());Property 'toUppercase' does not exist on type 'string'. Did you mean 'toUpperCase'?Property 'toUppercase' does not exist on type 'string'. Did you mean 'toUpperCase'?
});
 
// 화살표 함수에도 문맥적 타입 부여는 적용됩니다
names.forEach((s) => {
  console.log(s.toUppercase());Property 'toUppercase' does not exist on type 'string'. Did you mean 'toUpperCase'?Property 'toUppercase' does not exist on type 'string'. Did you mean 'toUpperCase'?
});Try
```

매개 변수 `s`에는 타입이 표기되지 않았음에도 불구하고, TypeScript는 `s`의 타입을 알아내기 위하여 배열의 추론된 타입과 더불어 `forEach` 함수의 타입을 활용하였습니다.

이 과정은 *문맥적 타입 부여*라고 불리는데, 왜냐하면 함수가 실행되는 *문맥*을 통하여 해당 함수가 가져야 하는 타입을 알 수 있기 때문입니다. 추론 규칙과 비슷하게, 이 과정이 어떻게 일어나는지를 명시적으로 배울 필요는 없지만, 이것이 *실제로 일어나는 과정*이라는 것을 이해하면 타입 표기가 불필요한 경우를 구분하는 데에 도움이 됩니다. 값이 발생하는 문맥이 해당 값의 타입에 영향을 끼치는 예시들은 이후에 살펴보도록 하겠습니다.



## 객체 타입

원시 타입을 제외하고 가장 많이 마주치는 타입은 *객체 타입*입니다. 객체는 프로퍼티를 가지는 JavaScript 값을 말하는데, 대부분의 경우가 이에 해당하죠! 객체 타입을 정의하려면, 해당 객체의 프로퍼티들과 각 프로퍼티의 타입들을 나열하기만 하면 됩니다.

예를 들어, 아래 함수는 좌표로 보이는 객체를 인자로 받고 있습니다.

```react
// 매개 변수의 타입은 객체로 표기되고 있습니다.
function printCoord(pt: { x: number; y: number }) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
printCoord({ x: 3, y: 7 });Try
```

위에서 매개변수는 `x`와 `y`라는 두 개의 프로퍼티로 이루어진 타입으로 표기되고 있는데, 두 값은 모두 `number` 타입입니다. 각 프로퍼티를 구분할 때 `,` 또는 `;`를 사용할 수 있고, 가장 마지막에 위치한 구분자의 표기는 선택 사항입니다.

각 프로퍼티의 타입 표기 또한 선택 사항입니다. 만약 타입을 지정하지 않는다면, 해당 프로퍼티는 `any` 타입으로 간주합니다.





### 옵셔널 프로퍼티

객체 타입은 일부 또는 모든 프로퍼티의 타입을 선택적인 타입, 즉 *옵셔널*로 지정할 수 있습니다. 프로퍼티 이름 뒤에 `?`를 붙이면 됩니다.

```react
function printName(obj: { first: string; last?: string }) {
  // ...
}
// 둘 다 OK
printName({ first: "Bob" });
printName({ first: "Alice", last: "Alisson" });Try
```

JavaScript에서는 존재하지 않는 프로퍼티에 접근하였을 때, 런타임 오류가 발생하지 않고 `undefined` 값을 얻게 됩니다. 이 때문에 옵셔널 프로퍼티를 *읽었을* 때, 해당 값을 사용하기에 앞서 `undefined`인지 여부를 확인해야 합니다.

```react
function printName(obj: { first: string; last?: string }) {
  // 오류 - `obj.last`의 값이 제공되지 않는다면 프로그램이 멈추게 됩니다!
  console.log(obj.last.toUpperCase());'obj.last' is possibly 'undefined'.'obj.last' is possibly 'undefined'.
  if (obj.last !== undefined) {
    // OK
    console.log(obj.last.toUpperCase());
  }
 
  // 최신 JavaScript 문법을 사용하였을 때 또 다른 안전한 코드
  console.log(obj.last?.toUpperCase());
}
```





## 유니언 타입

TypeScript의 타입 시스템에서는 기존의 타입을 기반으로 다양한 연산자를 사용하여 새로운 타입을 만들 수 있습니다. 몇몇 타입들을 사용하는 법을 알았으니, 이제 이 타입들을 *조합하여* 흥미로운 방식으로 사용해볼 시간입니다.

### 유니언 타입 정의하기

타입을 조합하는 첫 번째 방법은 *유니언* 타입을 사용하는 것입니다. 유니언 타입은 서로 다른 두 개 이상의 타입들을 사용하여 만드는 것으로, 유니언 타입의 값은 타입 조합에 사용된 타입 중 *무엇이든 하나*를 타입으로 가질 수 있습니다. 조합에 사용된 각 타입을 유니언 타입의 *멤버*라고 부릅니다.

문자열 또는 숫자를 받을 수 있는 함수를 작성해보겠습니다.

```react
function printId(id: number | string) {
  console.log("Your ID is: " + id);
}
// OK
printId(101);
// OK
printId("202");
// 오류
printId({ myID: 22342 });Argument of type '{ myID: number; }' is not assignable to parameter of type 'string | number'.
```



### 유니언 타입 사용하기

유니언 타입에 맞는 값을 *제공하는* 것은 간단합니다. 유니언 타입의 멤버 중 하나에 해당하는 타입을 제공하면 됩니다. 유니언 타입인 값이 코드상에 *존재할 때*, 이를 어떻게 사용해야 할까요?

TypeScript에서 유니언을 다룰 때는 해당 유니언 타입의 *모든* 멤버에 대하여 유효한 작업일 때에만 허용됩니다. 예를 들어 `string | number`라는 유니언 타입의 경우, `string` 타입에만 유효한 메서드는 사용할 수 없습니다.

```react
function printId(id: number | string) {  console.log(id.toUpperCase());Property 'toUpperCase' does not exist on type 'string | number'.
  Property 'toUpperCase' does not exist on type 'number'.Property 'toUpperCase' does not exist on type 'string | number'.
  Property 'toUpperCase' does not exist on type 'number'.}Try
```

이를 해결하려면 코드상에서 유니언을 *좁혀야* 하는데, 이는 타입 표기가 없는 JavaScript에서 벌어지는 일과 동일합니다. *좁히기*란 TypeScript가 코드 구조를 바탕으로 어떤 값을 보다 구체적인 타입으로 추론할 수 있을 때 발생합니다.

예를 들어, TypeScript는 오직 `string` 값만이 `typeof` 연산의 결괏값으로 `"string"`을 가질 수 있다는 것을 알고 있습니다.

```react
function printId(id: number | string) {
  if (typeof id === "string") {
    // 이 분기에서 id는 'string' 타입을 가집니다
 
    console.log(id.toUpperCase());
  } else {
    // 여기에서 id는 'number' 타입을 가집니다
    console.log(id);
  }
}Try
```

또 다른 예시는 `Array.isArray`와 같은 함수를 사용하는 것입니다.

```react
function welcomePeople(x: string[] | string) {
  if (Array.isArray(x)) {
    // 여기에서 'x'는 'string[]' 타입입니다
    console.log("Hello, " + x.join(" and "));
  } else {
    // 여기에서 'x'는 'string' 타입입니다
    console.log("Welcome lone traveler " + x);
  }
}Try
```

`else` 분기 문에서는 별도 처리를 하지 않아도 된다는 점에 유의하시기 바랍니다. `x`의 타입이 `string[]`가 아니라면, `x`의 타입은 반드시 `string`일 것입니다.

때로는 유니언의 모든 멤버가 무언가 공통점을 가질 수도 있습니다. 에를 들어, 배열과 문자열은 둘 다 `slice` 메서드를 내장합니다. 유니언의 모든 멤버가 어떤 프로퍼티를 공통으로 가진다면, 좁히기 없이도 해당 프로퍼티를 사용할 수 있게 됩니다.

```react
// 반환 타입은 'number[] | string'으로 추론됩니다
function getFirstThree(x: number[] | string) {
  return x.slice(0, 3);
}
```



## 타입 별칭

지금까지는 객체 타입과 유니언 타입을 사용할 때 직접 해당 타입을 표기하였습니다. 이는 편리하지만, 똑같은 타입을 한 번 이상 재사용하거나 또 다른 이름으로 부르고 싶은 경우도 존재합니다.

*타입 별칭*은 바로 이런 경우를 위하여 존재하며, *타입*을 위한 *이름*을 제공합니다. 타입 별칭의 구문은 아래와 같습니다.

```react
type Point = {
  x: number;
  y: number;
};
 
// 앞서 사용한 예제와 동일한 코드입니다
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
 
printCoord({ x: 100, y: 100 });
```



타입 별칭을 사용하면 단지 객체 타입뿐이 아닌 모든 타입에 대하여 새로운 이름을 부여할 수 있습니다. 예를 들어, 아래와 같이 유니언 타입에 대하여 타입 별칭을 부여할 수도 있습니다.

```react
type ID = number | string;Try
```

타입 별칭은 *단지* 별칭에 지나지 않는다는 점에 유의하시기 바랍니다. 즉, 타입 별칭을 사용하여도 동일 타입에 대하여 각기 구별되는 “여러 버전”을 만드는 것은 아닙니다. 별칭을 사용하는 것은, 별도로 이름 붙인 타입을 새로 작성하는 것입니다. 다시 말해, 아래 코드는 틀린 것처럼 *보일 수* 있지만, TypeScript에서는 이것이 정상인데 그 이유는 각각의 타입들이 동일 타입에 대한 별칭들이기 때문입니다.

```react
type UserInputSanitizedString = string;
 
function sanitizeInput(str: string): UserInputSanitizedString {
  return sanitize(str);
}
 
// 보안 처리를 마친 입력을 생성
let userInput = sanitizeInput(getInput());
 
// 물론 새로운 문자열을 다시 대입할 수도 있습니다
userInput = "new input";
```



## 인터페이스

*인터페이스 선언*은 객체 타입을 만드는 또 다른 방법입니다.

```react
interface Point {
  x: number;
  y: number;
}
 
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
 
printCoord({ x: 100, y: 100 });
```

타입 별칭을 사용한 경우와 마찬가지로, 위 예시 코드는 마치 타입이 없는 임의의 익명 객체를 사용하는 것처럼 동작합니다. TypeScript는 오직 `printCoord`에 전달된 값의 *구조*에만 관심을 가집니다. 즉, 예측된 프로퍼티를 가졌는지 여부만을 따집니다. 이처럼, 타입이 가지는 구조와 능력에만 관심을 가진다는 점은 TypeScript가 *구조적* 타입 시스템이라고 불리는 이유입니다.



### 타입 별칭과 인터페이스의 차이점

타입 별칭과 인터페이스는 매우 유사하며, 대부분의 경우 둘 중 하나를 자유롭게 선택하여 사용할 수 있습니다. `interface`가 가지는 대부분의 기능은 `type`에서도 동일하게 사용 가능합니다. 이 둘의 가장 핵심적인 차이는, 타입은 새 프로퍼티를 추가하도록 개방될 수 없는 반면, 인터페이스의 경우 항상 확장될 수 있다는 점입니다.



인터페이스 확장하기

```react
interface Animal {  
name: string 
} 

interface Bear extends Animal {  
honey: boolean 
} 

const bear = getBear() 
bear.name 
bear.honey
```



교집합을 통하여 타입 확장하기

```react
type Animal = { 
name: string 
} 

type Bear = Animal & {  
honey: Boolean 
} 

const bear = getBear();
bear.name;
bear.honey;
```



기존의 인터페이스에 새 필드를 추가하기

```react
interface Window {
  title: string
}
interface Window {
  ts: TypeScriptAPI
}
const src = 'const a = "Hello World"';
window.ts.transpileModule(src, {});
```



타입은 생성된 뒤에는 달라질 수 없다

```react
type Window = {
  title: string
}
type Window = {
  ts: TypeScriptAPI
}
 // Error: Duplicate identifier 'Window'.
```



## 타입 단언

때로는 TypeScript보다 당신이 어떤 값의 타입에 대한 정보를 더 잘 아는 경우도 존재합니다.

예를 들어 코드상에서 `document.getElementById`가 사용되는 경우, TypeScript는 이때 `HTMLElement` 중에 *무언가*가 반환된다는 것만을 알 수 있는 반면에, 당신은 페이지 상에서 사용되는 ID로는 언제나 `HTMLCanvasElement`가 반환된다는 사실을 이미 알고 있을 수도 있습니다.

이런 경우, *타입 단언*을 사용하면 타입을 좀 더 구체적으로 명시할 수 있습니다.

```react
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;Try
```

타입 표기와 마찬가지로, 타입 단언은 컴파일러에 의하여 제거되며 코드의 런타임 동작에는 영향을 주지 않습니다.

꺾쇠괄호를 사용하는 것 또한 (코드가 `.tsx` 파일이 아닌 경우) 가능하며, 이는 동일한 의미를 가집니다.

```react
const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas");
```





단 하나의 값만을 가질 수 있는 변수는 그다지 쓸모가 없죠!

하지만 리터럴을 유니언과 *함께 사용하면*, 보다 유용한 개념들을 표현할 수 있게 됩니다. 예를 들어, 특정 종류의 값들만을 인자로 받을 수 있는 함수를 정의하는 경우가 있습니다.

```react
function printText(s: string, alignment: "left" | "right" | "center") {
  // ...
}
printText("Hello, world", "left");
printText("G'day, mate", "centre");Argument of type '"centre"' is not assignable to parameter of type '"left" | "right" | "center"'.Argument of type '"centre"' is not assignable to parameter of type '"left" | "right" | "center"'.Try
```

숫자 리터럴 타입 또한 같은 방식으로 사용할 수 있습니다.

```react
function compare(a: string, b: string): -1 | 0 | 1 {
  return a === b ? 0 : a > b ? 1 : -1;
}Try
```

물론, 리터럴이 아닌 타입과도 함께 사용할 수 있습니다.

```react
interface Options {
  width: number;
}
function configure(x: Options | "auto") {
  // ...
}
configure({ width: 100 });
configure("auto");
configure("automatic");Argument of type '"automatic"' is not assignable to parameter of type 'Options | "auto"'.Argument of type '"automatic"' is not assignable to parameter of type 'Options | "auto"'.Try
```

또 하나의 리터럴 타입이 있습니다. 바로 불 리터럴 타입입니다. 불 리터럴에는 오직 두 개의 타입만이 존재하며, 이는 익히 예상하셨듯이 `true`와 `false`입니다. `boolean` 타입 자체는 사실 단지 `true | false` 유니언 타입의 별칭입니다.



### 리터럴 추론

객체를 사용하여 변수를 초기화하면, TypeScript는 해당 객체의 프로퍼티는 이후에 그 값이 변화할 수 있다고 가정합니다. 예를 들어, 아래와 같은 코드를 작성하는 경우를 보겠습니다.

```react
const obj = { counter: 0 };
if (someCondition) {
  obj.counter = 1;
}Try
```

기존에 값이 `0`이었던 필드에 `1`을 대입하였을 때 TypeScript는 이를 오류로 간주하지 않습니다. 이를 달리 말하면 `obj.counter`는 반드시 `number` 타입을 가져야 하며, `0` 리터럴 타입을 가질 수 없다는 의미입니다. 왜냐하면 타입은 *읽기* 및 *쓰기* 두 동작을 결정하는 데에 사용되기 때문입니다.

동일한 사항이 문자열에도 적용됩니다.

```react
const req = { url: "https://example.com", method: "GET" };
handleRequest(req.url, req.method);Argument of type 'string' is not assignable to parameter of type '"GET" | "POST"'.Argument of type 'string' is not assignable to parameter of type '"GET" | "POST"'.Try
```

위 예시에서 `req.method`는 `string`으로 추론되지, `"GET"`으로 추론되지 않습니다. `req`의 생성 시점과 `handleRequest`의 호출 시점 사이에도 얼마든지 코드 평가가 발생할 수 있고, 이때 `req.method`에 `"GUESS"`와 같은 새로운 문자열이 대입될 수도 있으므로, TypeScript는 위 코드에 오류가 있다고 판단합니다.

이러한 경우를 해결하는 데에는 두 가지 방법이 있습니다.

1. 둘 중에 한 위치에 타입 단언을 추가하여 추론 방식을 변경할 수 있습니다.

   ```react
   // 수정 1:
   const req = { url: "https://example.com", method: "GET" as "GET" };
   // 수정 2
   handleRequest(req.url, req.method as "GET");
   ```

   수정 1은 `req.method`가 항상 *리터럴 타입* `"GET"`이기를 의도하며, 이에 따라 해당 필드에 `"GUESS"`와 같은 값이 대입되는 경우를 미연에 방지하겠다”는 것을 의미합니다. 수정 2는 “무슨 이유인지, `req.method`가 `"GET"`을 값으로 가진다는 사실을 알고 있다”는 것을 의미합니다.

2. `as const`를 사용하여 객체 전체를 리터럴 타입으로 변환할 수 있습니다.

   ```react
   const req = { url: "https://example.com", method: "GET" } as const;
   handleRequest(req.url, req.method);
   ```

`as const` 접미사는 일반적인 `const`와 유사하게 작동하는데, 해당 객체의 모든 프로퍼티에 `string` 또는 `number`와 같은 보다 일반적인 타입이 아닌 리터럴 타입의 값이 대입되도록 보장합니다.





## `null`과`undefined`

JavaScript에는 빈 값 또는 초기화되지 않은 값을 가리키는 두 가지 원시값이 존재합니다. 바로 `null`과 `undefined`입니다.

TypeScript에는 각 값에 대응하는 동일한 이름의 두 가지 *타입*이 존재합니다. 각 타입의 동작 방식은 `strictNullChecks` 옵션의 설정 여부에 따라 달라집니다.

### `strictNullChecks`가 설정되지 않았을 때

`strictNullChecks`가 *설정되지 않았다면*, 어떤 값이 `null` 또는 `undefined`일 수 있더라도 해당 값에 평소와 같이 접근할 수 있으며, `null`과 `undefined`는 모든 타입의 변수에 대입될 수 있습니다. 이는 Null 검사를 하지 않는 언어(C#, Java 등)의 동작 방식과 유사합니다. Null 검사의 부재는 버그의 주요 원인이 되기도 합니다. 별다른 이유가 없다면, 코드 전반에 걸쳐 `strictNullChecks` 옵션을 설정하는 것을 항상 권장합니다.

### `strictNullChecks`설정되었을 때

`strictNullChecks`가 *설정되었다면*, 어떤 값이 `null` 또는 `undefined`일 때, 해당 값과 함께 메서드 또는 프로퍼티를 사용하기에 앞서 해당 값을 테스트해야 합니다. 옵셔널 프로퍼티를 사용하기에 앞서 `undefined` 여부를 검사하는 것과 마찬가지로, *좁히기*를 통하여 `null`일 수 있는 값에 대한 검사를 수행할 수 있습니다.

```
function doSomething(x: string | undefined) {
  if (x === undefined) {
    // 아무 것도 하지 않는다
  } else {
    console.log("Hello, " + x.toUpperCase());
  }
}Try
```

### Null 아님 단언 연산자 (접미사`!`)

TypeScript에서는 명시적인 검사를 하지 않고도 타입에서 `null`과 `undefined`를 제거할 수 있는 특별한 구문을 제공합니다. 표현식 뒤에 `!`를 작성하면 해당 값이 `null` 또는 `undefined`가 아니라고 타입 단언하는 것입니다.

```
function liveDangerously(x?: number | undefined) {
  // 오류 없음
  console.log(x!.toFixed());
}Try
```

다른 타입 단언과 마찬가지로 이 구문은 코드의 런타임 동작을 변화시키지 않으므로, `!` 연산자는 반드시 해당 값이 `null` 또는 `undefined`가 *아닌* 경우에만 사용해야 합니다.



Imagine we have a function called `padLeft`.

```react
function padLeft(padding: number | string, input: string): string {
  throw new Error("Not implemented yet!");
}
```

If `padding` is a `number`, it will treat that as the number of spaces we want to prepend to `input`. If `padding` is a `string`, it should just prepend `padding` to `input`. Let’s try to implement the logic for when `padLeft` is passed a `number` for `padding`.

```react
function padLeft(padding: number | string, input: string) {  
    return " ".repeat(padding) + input;
    
    Argument of type 'string | number' is not assignable to parameter of type 'number'.
  Type 'string' is not assignable to type 'number'.Argument of type 'string | number' is not assignable to parameter of type 'number'.
  Type 'string' is not assignable to type 'number'.}Try
```

Uh-oh, we’re getting an error on `padding`. TypeScript is warning us that we’re passing a value with type `number | string` to the `repeat` function, which only accepts a `number`, and it’s right. In other words, we haven’t explicitly checked if `padding` is a `number` first, nor are we handling the case where it’s a `string`, so let’s do exactly that.

```react
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    return " ".repeat(padding) + input;
  }
  return padding + input;
}
```

이것이 대체로 흥미롭지 않은 JavaScript 코드처럼 보인다면 그게 요점입니다. 우리가 배치한 주석을 제외하면 이 TypeScript 코드는 JavaScript처럼 보입니다. 아이디어는 TypeScript의 유형 시스템이 유형 안전성을 얻기 위해 뒤로 구부리지 않고 일반적인 JavaScript 코드를 가능한 한 쉽게 작성하는 것을 목표로 한다는 것입니다.

별거 아닌 것 같지만 사실 여기에는 많은 것들이 숨겨져 있습니다. `if/else`TypeScript가 정적 유형을 사용하여 런타임 값을 분석하는 방법과 매우 유사하게, 유형 분석 은 이러한 유형에 모두 영향을 미칠 수 있는 , 조건부 삼항, 루프, 진실성 검사 등과 같은 JavaScript의 런타임 제어 흐름 구조에 유형 분석을 오버레이합니다 .

우리의 `if`검사 내에서 TypeScript는 이를 *유형 보호*`typeof padding === "number"` 라고 하는 특별한 형태의 코드로 보고 이해합니다 . TypeScript는 프로그램이 주어진 위치에서 가능한 가장 구체적인 유형의 값을 분석하기 위해 취할 수 있는 가능한 실행 경로를 따릅니다. *이러한 특수 검사( 유형 보호* 라고 함 ) 및 할당을 살펴보고 유형을 선언된 것보다 더 구체적인 유형으로 정제하는 프로세스를 *축소* 라고 합니다 . 많은 편집기에서 이러한 유형이 변경되는 것을 관찰할 수 있으며 예제에서도 그렇게 할 것입니다.

```react
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    return " ".repeat(padding) + input;
                        
(parameter) padding: number
  }
  return padding + input;
           
(parameter) padding: string
}
```



## `typeof`타입 가드

우리가 본 것처럼 JavaScript는 `typeof`런타임에 우리가 가지고 있는 값의 유형에 대한 매우 기본적인 정보를 제공할 수 있는 연산자를 지원합니다. TypeScript는 이것이 특정 문자열 집합을 반환할 것으로 예상합니다.

- `"string"`
- `"number"`
- `"bigint"`
- `"boolean"`
- `"symbol"`
- `"undefined"`
- `"object"`
- `"function"`

에서 본 것처럼 `padLeft`이 연산자는 여러 JavaScript 라이브러리에서 꽤 자주 등장하며 TypeScript는 이를 이해하여 다양한 분기의 유형을 좁힐 수 있습니다.

TypeScript에서 반환된 값에 대한 확인은 `typeof`유형 보호입니다. TypeScript는 다양한 값에서 작동하는 방식을 인코딩하기 때문에 `typeof`JavaScript의 몇 가지 단점을 알고 있습니다. 예를 들어 위 목록에서 는 `typeof`문자열을 반환하지 않습니다 `null`. 다음 예를 확인하십시오.

```react
function printAll(strs: string | string[] | null) {
  if (typeof strs === "object") {
    for (const s of strs) {'strs' is possibly 'null'.'strs' is possibly 'null'.
      console.log(s);
    }
  } else if (typeof strs === "string") {
    console.log(strs);
  } else {
    // do nothing
  }
}노력하다
```

함수 에서 배열 유형인지 확인하기 위해 객체인지 `printAll`확인하려고 합니다 (지금은 JavaScript에서 배열이 객체 유형임을 강조할 좋은 시기일 수 있습니다). `strs`그러나 JavaScript에서는 `typeof null`실제로 `"object"`! 이것은 역사의 불행한 사고 중 하나입니다.

충분한 경험을 가진 사용자는 놀라지 않을 수 있지만 모든 사람이 JavaScript에서 이 문제를 겪은 것은 아닙니다. 운 좋게도 TypeScript는 `strs`단지 .`string[] | null``string[]`

이것은 우리가 "진실성" 검사라고 부르는 것에 대한 좋은 세그웨이가 될 수 있습니다.



# Truthiness narrowing

Truthiness might not be a word you’ll find in the dictionary, but it’s very much something you’ll hear about in JavaScript.

In JavaScript, we can use any expression in conditionals, `&&`s, `||`s, `if` statements, Boolean negations (`!`), and more. As an example, `if` statements don’t expect their condition to always have the type `boolean`.

```react
function getUsersOnlineMessage(numUsersOnline: number) {
  if (numUsersOnline) {
    return `There are ${numUsersOnline} online now!`;
  }
  return "Nobody's here. :(";
}Try
```

In JavaScript, constructs like `if` first “coerce” their conditions to `boolean`s to make sense of them, and then choose their branches depending on whether the result is `true` or `false`. Values like

- `0`
- `NaN`
- `""` (the empty string)
- `0n` (the `bigint` version of zero)
- `null`
- `undefined`

all coerce to `false`, and other values get coerced `true`. You can always coerce values to `boolean`s by running them through the `Boolean` function, or by using the shorter double-Boolean negation. (The latter has the advantage that TypeScript infers a narrow literal boolean type `true`, while inferring the first as type `boolean`.)

```react
// both of these result in 'true'
Boolean("hello"); // type: boolean, value: true
!!"world"; // type: true,    value: true
```



It’s fairly popular to leverage this behavior, especially for guarding against values like `null` or `undefined`. As an example, let’s try using it for our `printAll` function.

```react
function printAll(strs: string | string[] | null) {
  if (strs && typeof strs === "object") {
    for (const s of strs) {
      console.log(s);
    }
  } else if (typeof strs === "string") {
    console.log(strs);
  }
}Try
```

You’ll notice that we’ve gotten rid of the error above by checking if `strs` is truthy. This at least prevents us from dreaded errors when we run our code like:

```
TypeError: null is not iterable
```

Keep in mind though that truthiness checking on primitives can often be error prone. As an example, consider a different attempt at writing `printAll`

```react
function printAll(strs: string | string[] | null) {
  // !!!!!!!!!!!!!!!!
  //  DON'T DO THIS!
  //   KEEP READING
  // !!!!!!!!!!!!!!!!
  if (strs) {
    if (typeof strs === "object") {
      for (const s of strs) {
        console.log(s);
      }
    } else if (typeof strs === "string") {
      console.log(strs);
    }
  }
}Try
```

We wrapped the entire body of the function in a truthy check, but this has a subtle downside: we may no longer be handling the empty string case correctly.

TypeScript doesn’t hurt us here at all, but this is behavior worth noting if you’re less familiar with JavaScript. TypeScript can often help you catch bugs early on, but if you choose to do *nothing* with a value, there’s only so much that it can do without being overly prescriptive. If you want, you can make sure you handle situations like these with a linter.

One last word on narrowing by truthiness is that Boolean negations with `!` filter out from negated branches.

```react
function multiplyAll(
  values: number[] | undefined,
  factor: number
): number[] | undefined {
  if (!values) {
    return values;
  } else {
    return values.map((x) => x * factor);
  }
}
```



Checking against specific literal values (as opposed to variables) works also. In our section about truthiness narrowing, we wrote a `printAll` function which was error-prone because it accidentally didn’t handle empty strings properly. Instead we could have done a specific check to block out `null`s, and TypeScript still correctly removes `null` from the type of `strs`.

```react
function printAll(strs: string | string[] | null) {
  if (strs !== null) {
    if (typeof strs === "object") {
      for (const s of strs) {
                       
(parameter) strs: string[]
        console.log(s);
      }
    } else if (typeof strs === "string") {
      console.log(strs);
                   
(parameter) strs: string
    }
  }
}
```



JavaScript’s looser equality checks with `==` and `!=` also get narrowed correctly. If you’re unfamiliar, checking whether something `== null` actually not only checks whether it is specifically the value `null` - it also checks whether it’s potentially `undefined`. The same applies to `== undefined`: it checks whether a value is either `null` or `undefined`.

```react
interface Container {
  value: number | null | undefined;
}
 
function multiplyValue(container: Container, factor: number) {
  // Remove both 'null' and 'undefined' from the type.
  if (container.value != null) {
    console.log(container.value);
                           
(property) Container.value: number
 
    // Now we can safely multiply 'container.value'.
    container.value *= factor;
  }
}
```



## The`in`operator narrowing

JavaScript has an operator for determining if an object has a property with a name: the `in` operator. TypeScript takes this into account as a way to narrow down potential types.

For example, with the code: `"value" in x`. where `"value"` is a string literal and `x` is a union type. The “true” branch narrows `x`’s types which have either an optional or required property `value`, and the “false” branch narrows to types which have an optional or missing property `value`.

```react
type Fish = { swim: () => void };
type Bird = { fly: () => void };
 
function move(animal: Fish | Bird) {
  if ("swim" in animal) {
    return animal.swim();
  }
 
  return animal.fly();
}Try
```

To reiterate optional properties will exist in both sides for narrowing, for example a human could both swim and fly (with the right equipment) and thus should show up in both sides of the `in` check:

```react
type Fish = { swim: () => void };
type Bird = { fly: () => void };
type Human = { swim?: () => void; fly?: () => void };
 
function move(animal: Fish | Bird | Human) {
  if ("swim" in animal) {
    animal;
      
(parameter) animal: Fish | Human
  } else {
    animal;
      
(parameter) animal: Bird | Human
  }
}
```

To reiterate optional properties will exist in both sides for narrowing, for example a human could both swim and fly (with the right equipment) and thus should show up in both sides of the `in` check:

```react
type Fish = { swim: () => void };
type Bird = { fly: () => void };
type Human = { swim?: () => void; fly?: () => void };
 
function move(animal: Fish | Bird | Human) {
  if ("swim" in animal) {
    animal;
      
(parameter) animal: Fish | Human
  } else {
    animal;
      
(parameter) animal: Bird | Human
  }
}
```



## `instanceof`narrowing

JavaScript has an operator for checking whether or not a value is an “instance” of another value. More specifically, in JavaScript `x instanceof Foo` checks whether the *prototype chain* of `x` contains `Foo.prototype`. While we won’t dive deep here, and you’ll see more of this when we get into classes, they can still be useful for most values that can be constructed with `new`. As you might have guessed, `instanceof` is also a type guard, and TypeScript narrows in branches guarded by `instanceof`s.

```react
function logValue(x: Date | string) {
  if (x instanceof Date) {
    console.log(x.toUTCString());
               
(parameter) x: Date
  } else {
    console.log(x.toUpperCase());
               
(parameter) x: string
  }
}
```



## Assignments

As we mentioned earlier, when we assign to any variable, TypeScript looks at the right side of the assignment and narrows the left side appropriately.

```react
let x = Math.random() < 0.5 ? 10 : "hello world!";
   
let x: string | number
x = 1;
 
console.log(x);
           
let x: number
x = "goodbye!";
 
console.log(x);
           
let x: stringTry
```

Notice that each of these assignments is valid. Even though the observed type of `x` changed to `number` after our first assignment, we were still able to assign a `string` to `x`. This is because the *declared type* of `x` - the type that `x` started with - is `string | number`, and assignability is always checked against the declared type.

If we’d assigned a `boolean` to `x`, we’d have seen an error since that wasn’t part of the declared type.

```react
let x = Math.random() < 0.5 ? 10 : "hello world!";
   
let x: string | number
x = 1;
 
console.log(x);
           
let x: number
x = true;Type 'boolean' is not assignable to type 'string | number'.Type 'boolean' is not assignable to type 'string | number'.
 
console.log(x);
           
let x: string | number
```



## Control flow analysis

Up until this point, we’ve gone through some basic examples of how TypeScript narrows within specific branches. But there’s a bit more going on than just walking up from every variable and looking for type guards in `if`s, `while`s, conditionals, etc. For example

```react
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    return " ".repeat(padding) + input;
  }
  return padding + input;
}Try
```

`padLeft` returns from within its first `if` block. TypeScript was able to analyze this code and see that the rest of the body (`return padding + input;`) is *unreachable* in the case where `padding` is a `number`. As a result, it was able to remove `number` from the type of `padding` (narrowing from `string | number` to `string`) for the rest of the function.

This analysis of code based on reachability is called *control flow analysis*, and TypeScript uses this flow analysis to narrow types as it encounters type guards and assignments. When a variable is analyzed, control flow can split off and re-merge over and over again, and that variable can be observed to have a different type at each point.



```react
function example() {
  let x: string | number | boolean;
 
  x = Math.random() < 0.5;
 
  console.log(x);
             
let x: boolean
 
  if (Math.random() < 0.5) {
    x = "hello";
    console.log(x);
               
let x: string
  } else {
    x = 100;
    console.log(x);
               
let x: number
  }
 
  return x;
        
let x: string | number
}
```



## Using type predicates

We’ve worked with existing JavaScript constructs to handle narrowing so far, however sometimes you want more direct control over how types change throughout your code.

To define a user-defined type guard, we simply need to define a function whose return type is a *type predicate*:

```react
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}Try
```

`pet is Fish` is our type predicate in this example. A predicate takes the form `parameterName is Type`, where `parameterName` must be the name of a parameter from the current function signature.

Any time `isFish` is called with some variable, TypeScript will *narrow* that variable to that specific type if the original type is compatible.

```react
// Both calls to 'swim' and 'fly' are now okay.
let pet = getSmallPet();
 
if (isFish(pet)) {
  pet.swim();
} else {
  pet.fly();
}Try
```

Notice that TypeScript not only knows that `pet` is a `Fish` in the `if` branch; it also knows that in the `else` branch, you *don’t* have a `Fish`, so you must have a `Bird`.

You may use the type guard `isFish` to filter an array of `Fish | Bird` and obtain an array of `Fish`:

```react
const zoo: (Fish | Bird)[] = [getSmallPet(), getSmallPet(), getSmallPet()];
const underWater1: Fish[] = zoo.filter(isFish);
// or, equivalently
const underWater2: Fish[] = zoo.filter(isFish) as Fish[];
 
// The predicate may need repeating for more complex examples
const underWater3: Fish[] = zoo.filter((pet): pet is Fish => {
  if (pet.name === "sharkey") return false;
  return isFish(pet);
});Try
```

In addition, classes can [use `this is Type`](https://www.typescriptlang.org/docs/handbook/2/classes.html#this-based-type-guards) to narrow their type.



# Discriminated unions

Most of the examples we’ve looked at so far have focused around narrowing single variables with simple types like `string`, `boolean`, and `number`. While this is common, most of the time in JavaScript we’ll be dealing with slightly more complex structures.

For some motivation, let’s imagine we’re trying to encode shapes like circles and squares. Circles keep track of their radiuses and squares keep track of their side lengths. We’ll use a field called `kind` to tell which shape we’re dealing with. Here’s a first attempt at defining `Shape`.

```react
interface Shape {
  kind: "circle" | "square";
  radius?: number;
  sideLength?: number;
}
```

Notice we’re using a union of string literal types: `"circle"` and `"square"` to tell us whether we should treat the shape as a circle or square respectively. By using `"circle" | "square"` instead of `string`, we can avoid misspelling issues.

```react
function handleShape(shape: Shape) {
  // oops!
  if (shape.kind === "rect") {
      This comparison appears to be unintentional because the types '"circle" | "square"' and '"rect"' have no overlap.This comparison appears to be unintentional because the types '"circle" | "square"' and '"rect"' have no overlap.
    // ...
  }
}
```

We can write a `getArea` function that applies the right logic based on if it’s dealing with a circle or square. We’ll first try dealing with circles.

```react
function getArea(shape: Shape) {
  return Math.PI * shape.radius ** 2;
    'shape.radius' is possibly 'undefined'.'shape.radius' is possibly 'undefined'.
}Try
```

Under [`strictNullChecks`](https://www.typescriptlang.org/tsconfig#strictNullChecks) that gives us an error - which is appropriate since `radius` might not be defined. But what if we perform the appropriate checks on the `kind` property?

```react
function getArea(shape: Shape) {
  if (shape.kind === "circle") {
    return Math.PI * shape.radius ** 2;
      'shape.radius' is possibly 'undefined'.'shape.radius' is possibly 'undefined'.
  }
}Try
```

Hmm, TypeScript still doesn’t know what to do here. We’ve hit a point where we know more about our values than the type checker does. We could try to use a non-null assertion (a `!` after `shape.radius`) to say that `radius` is definitely present.

```react
function getArea(shape: Shape) {
  if (shape.kind === "circle") {
    return Math.PI * shape.radius! ** 2;
  }
}
```



But this doesn’t feel ideal. We had to shout a bit at the type-checker with those non-null assertions (`!`) to convince it that `shape.radius` was defined, but those assertions are error-prone if we start to move code around. Additionally, outside of [`strictNullChecks`](https://www.typescriptlang.org/tsconfig#strictNullChecks) we’re able to accidentally access any of those fields anyway (since optional properties are just assumed to always be present when reading them). We can definitely do better.

The problem with this encoding of `Shape` is that the type-checker doesn’t have any way to know whether or not `radius` or `sideLength` are present based on the `kind` property. We need to communicate what *we* know to the type checker. With that in mind, let’s take another swing at defining `Shape`.

```react
interface Circle {
  kind: "circle";
  radius: number;
}
 
interface Square {
  kind: "square";
  sideLength: number;
}
 
type Shape = Circle | Square;Try
```

Here, we’ve properly separated `Shape` out into two types with different values for the `kind` property, but `radius` and `sideLength` are declared as required properties in their respective types.

Let’s see what happens here when we try to access the `radius` of a `Shape`.

```react
function getArea(shape: Shape) {  
    return Math.PI * shape.radius ** 2;
    Property 'radius' does not exist on type 'Shape'.
  Property 'radius' does not exist on type 'Square'.Property 'radius' does not exist on type 'Shape'.
  Property 'radius' does not exist on type 'Square'.}
```



Like with our first definition of `Shape`, this is still an error. When `radius` was optional, we got an error (with [`strictNullChecks`](https://www.typescriptlang.org/tsconfig#strictNullChecks) enabled) because TypeScript couldn’t tell whether the property was present. Now that `Shape` is a union, TypeScript is telling us that `shape` might be a `Square`, and `Square`s don’t have `radius` defined on them! Both interpretations are correct, but only the union encoding of `Shape` will cause an error regardless of how [`strictNullChecks`](https://www.typescriptlang.org/tsconfig#strictNullChecks) is configured.

But what if we tried checking the `kind` property again?

```react
function getArea(shape: Shape) {
  if (shape.kind === "circle") {
    return Math.PI * shape.radius ** 2;
                      
(parameter) shape: Circle
  }
}Try
```

That got rid of the error! When every type in a union contains a common property with literal types, TypeScript considers that to be a *discriminated union*, and can narrow out the members of the union.

In this case, `kind` was that common property (which is what’s considered a *discriminant* property of `Shape`). Checking whether the `kind` property was `"circle"` got rid of every type in `Shape` that didn’t have a `kind` property with the type `"circle"`. That narrowed `shape` down to the type `Circle`.

The same checking works with `switch` statements as well. Now we can try to write our complete `getArea` without any pesky `!` non-null assertions.

```react
function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
                        
(parameter) shape: Circle
    case "square":
      return shape.sideLength ** 2;
              
(parameter) shape: Square
  }
}Try
```

The important thing here was the encoding of `Shape`. Communicating the right information to TypeScript - that `Circle` and `Square` were really two separate types with specific `kind` fields - was crucial. Doing that lets us write type-safe TypeScript code that looks no different than the JavaScript we would’ve written otherwise. From there, the type system was able to do the “right” thing and figure out the types in each branch of our `switch` statement.



Discriminated unions are useful for more than just talking about circles and squares. They’re good for representing any sort of messaging scheme in JavaScript, like when sending messages over the network (client/server communication), or encoding mutations in a state management framework.



# Exhaustiveness checking

The `never` type is assignable to every type; however, no type is assignable to `never` (except `never` itself). This means you can use narrowing and rely on `never` turning up to do exhaustive checking in a switch statement.

For example, adding a `default` to our `getArea` function which tries to assign the shape to `never` will raise an error when every possible case has not been handled.

```react
type Shape = Circle | Square;
 
function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.sideLength ** 2;
    default:
      const _exhaustiveCheck: never = shape;
      return _exhaustiveCheck;
  }
}Try
```

Adding a new member to the `Shape` union, will cause a TypeScript error:

```react
interface Triangle {
  kind: "triangle";
  sideLength: number;
}
 
type Shape = Circle | Square | Triangle;
 
function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.sideLength ** 2;
    default:
      const _exhaustiveCheck: never = shape;Type 'Triangle' is not assignable to type 'never'.Type 'Triangle' is not assignable to type 'never'.
      return _exhaustiveCheck;
  }
}
```





## 함수 타입 표현식

함수를 설명하는 가장 간단한 방법은 *함수 타입 표현식* 입니다. 이 타입은 화살표 함수와 문법적으로 유사합니다.

```react
function greeter(fn: (a: string) => void) {
  fn("Hello, World");
}
 
function printToConsole(s: string) {
  console.log(s);
}
 
greeter(printToConsole);Try
```

`(a: string) => void` 라는 문법은 “문자열 타입 `a`를 하나의 매개변수로 가지고 반환값이 없는 함수”를 의미합니다. 함수 선언처럼, 매개변수의 타입이 지정되지 않으면, 암묵적으로 `any`가 됩니다.

> 매개변수 이름이 **필수** 라는것을 명심하십시오. 함수 타입 `(string) => void`는 ”`any` 타입을 가진 `string`이라는 이름의 매개변수를 가진 함수를 뜻합니다!

물론 타입 별칭을 사용해서 함수의 타입에 이름을 붙일 수 있습니다.

```react
type GreetFunction = (a: string) => void;
function greeter(fn: GreetFunction) {
  // ...
}
```



## 호출 시그니처

JavaScript에서, 함수들은 호출이 가능할 뿐만 아니라, 프로퍼티도 가질 수 있습니다. 하지만, 함수 타입 표현식 문법은 프로퍼티를 정의하는 것을 허락하지 않습니다. 만약 우리가 호출 가능하면서 프로퍼티를 가진 무언가를 설명하려고 하면, 객체 타입에 *호출 시그니처* 를 사용하여 표현할 수 있습니다.

```react
type DescribableFunction = {
  description: string;
  (someArg: number): boolean;
};
function doSomething(fn: DescribableFunction) {
  console.log(fn.description + " returned " + fn(6));
}Try
```

이 문법은 함수 타입 표현식과 다릅니다. 매개변수 타입과 반환값의 타입 사이에 `=>`가 아닌 `:`를 사용해야 합니다.



## 구성 시그니처

JavaScript 함수는 `new`연산자를 통해서도 호출 될 수 있습니다. TypeScript는 이런 것들이 주로 새로운 객체를 생성하는데 사용되기 때문에 *생성자* 로 간주합니다. 여러분은 호출 시그니처 앞에 `new` 키워드를 붙임으로서, *구성 시그니처*를 작성할 수 있습니다.

```react
type SomeConstructor = {
  new (s: string): SomeObject;
};
function fn(ctor: SomeConstructor) {
  return new ctor("hello");
}Try
```

JavaScript의 `Date` 객체와 같은 몇몇 객체는 `new`가 있든 없든 호출될 수 있습니다. 여러분은 호출 시그니처와 구성 시그니처를 임의로 같은 타입에서 결합시킬 수 있습니다.

```react
interface CallOrConstruct {
  new (s: string): Date;
  (n?: number): number;
}
```



## 제네릭 함수

입력 값이 출력 값의 타입과 관련이 있거나, 두 입력값의 타입이 서로 관련이 있는 형태의 함수를 작성하는 것은 흔히 일어나는 일입니다. 잠시 배열의 첫 번째 원소를 반환하는 함수를 생각해 봅시다.

```react
function firstElement(arr: any[]) {
  return arr[0];
}
```

함수는 제 역할을 하지만, 아쉽게도 반환 타입이 `any` 입니다. 함수가 배열 원소의 타입을 반환한다면 더 나을 것 같습니다.

TypeScript에서, *제네릭* 문법이 두 값 사이의 상관관계를 표현하기 위해서 사용됩니다. 우리는 함수 시그니처에서 *타입 매개변수*를 선언함으로서 그런 표현을 할 수 있습니다.

```react
function firstElement<Type>(arr: Type[]): Type | undefined {
  return arr[0];
}Try
```

타입 매개변수 `Type`을 이 함수에 선언하고, 필요한 두 곳에 사용함으로써 우리는 함수의 입력 값(배열)과 출력(반환 값) 사이에 연결고리를 만들었습니다. 이제 우리가 이 함수를 호출할 때, 더 명확한 타입을 얻을 수 있습니다.

```react
// s는 "string" 타입
const s = firstElement(["a", "b", "c"]);
// n은 "number" 타입
const n = firstElement([1, 2, 3]);
// u는 "undefined" 타입
const u = firstElement([]);
```



### 추론(Inference)

이 예제에서 우리는 `Type`을 특정하지 않았음에 주목하세요. 여기서 타입은 *추론되었습니다* 즉 TypeScript에 의해서 자동적으로 선택된 것입니다.

우리는 여러 개의 타입 매개변수도 사용할 수 있습니다. 예를 들어서, `map`의 스탠드얼론 버전은 아래와 같을 것 입니다.

```
function map<Input, Output>(arr: Input[], func: (arg: Input) => Output): Output[] {
  return arr.map(func);
}
 
// 매개변수 'n'의 타입은 'string' 입니다.
// 'parsed'는 number[] 타입을 하고 있습니다.
const parsed = map(["1", "2", "3"], (n) => parseInt(n));Try
```

이 예제에서 TypeScript는 `Input` 타입과(입력으로 주어진 `string` 배열로부터) `Output`타입을 함수 표현식의 반환 값(`number`)를 통해서 추론할 수 있는 점을 눈여겨보십시오.





### 타입 제한 조건

우리는 *모든* 타입에 대해서 동작하는 제네릭 함수들을 작성하였습니다. 가끔, 우리는 두 값을 연관시키기 원하지만 특정한 값들의 부분집합에 한해서만 동작하기를 원할 때가 있습니다. 이러한 경우에 우리는 *타입 제한 조건*을 사용하여, 타입 매개변수가 받아들일 수 있는 타입들을 제한할 수 있습니다.

두 값 중에 더 긴 것을 반환하는 함수를 작성해 봅시다. 이 작업을 위해, number인 `length` 프로퍼티가 필요합니다. `extends`절을 이용해서 타입 매개변수를 그 타입으로 *제한* 할 수 있습니다.

```react
function longest<Type extends { length: number }>(a: Type, b: Type) {
  if (a.length >= b.length) {
    return a;
  } else {
    return b;
  }
}
 
// longerArray 의 타입은 'number[]' 입니다'
const longerArray = longest([1, 2], [1, 2, 3]);
// longerString 의 타입은 'alice' | 'bob' 입니다.
const longerString = longest("alice", "bob");
// 에러! Number에는 'length' 프로퍼티가 없습니다.
const notOK = longest(10, 100);Argument of type 'number' is not assignable to parameter of type '{ length: number; }'.Argument of type 'number' is not assignable to parameter of type '{ length: number; }'.Try
```

이 예시에서는 몇 가지 흥미로운 점에 주목해야 합니다. 우리는 TypeScript가 `longest`의 반환 타입을 *추론* 하도록 허용했습니다. 반환 타입 추론은 제네릭 함수에서도 작동합니다.

우리가 `Type`을 `{ length: number }`로 제한했기에, 우리는 `a`와 `b` 매개변수에 대해서 `.length` 프로퍼티에 접근할 수 있었습니다. 타입 제한이 없다면, 이러한 값들이 length 프로퍼티를 가지지 않는 다른 타입일 수 있기 때문에, 그 프로퍼티에 접근 할 수 없었을 것입니다.

`longerArray`와 `longerString`의 타입은 인수를 기반으로 추론되었습니다. 제네릭은 두 개 이상의 값을 같은 타입으로 연관 짓는 것이라는 사실을 기억해야 합니다!

결국 우리가 원하는 대로 `longest(10,100)`은 `number`타입이 `.length` 프로퍼티를 가지고 있지 않았기 때문에 호출이 거부된 것을 볼 수 있습니다.



### 제한된 값으로 작업하기

다음은 제네릭 타입 제약 조건을 사용할 때, 흔히 범할 수 있는 실수입니다.

```react
function minimumLength<Type extends { length: number }>(  
    obj: Type,
    minimum: number
): Type {  
    if (obj.length >= minimum) {    
        return obj;  
    } else {    
        return { length: minimum };
 Type '{ length: number; }' is not assignable to type 'Type'.
  '{ length: number; }' is assignable to the constraint of type 'Type', but 'Type' could be instantiated with a different subtype of constraint '{ length: number; }'.Type '{ length: number; }' is not assignable to type 'Type'.
  '{ length: number; }' is assignable to the constraint of type 'Type', but 'Type' could be instantiated with a different subtype of constraint '{ length: number; }'.  }}Try
```

이 함수는 문제가 없는 것처럼 보입니다. `Type`은 `{ lenght: number }`로 제한되어 있고, 함수는 `Type`이나 저 제약조건을 만족하는 값을 반환합니다. 문제는 이 함수가 제약사항을 만족하는 *어떤* 객체가 아닌, 입력된 *어떤* 객체를 반환한다는 점입니다. 만약 이 코드가 유효하다면, 여러분들은 확실히 동작하지 않을 아래의 코드를 작성할 수 있을 것입니다.

```react
// 'arr' gets value { length: 6 }
const arr = minimumLength([1, 2, 3], 6);
// 여기서 배열은 'slice' 메서드를 가지고 있지만
// 반환된 객체는 그렇지 않기에 에러가 발생합니다!
console.log(arr.slice(0));
```



### 타입 인수를 명시하기

TypeScript는 제네릭 호출에서 의도된 타입을 대체로 추론해 내지만, 항상 그렇지는 않습니다. 예를 들어서, 여러분들이 두 배열을 결합하는 함수를 하나 작성했다고 합시다.

```react
function combine<Type>(arr1: Type[], arr2: Type[]): Type[] {
  return arr1.concat(arr2);
}Try
```

일반적으로 짝이 맞지 않는 배열과 함께 해당 함수를 부르는 것은 잘못된 것일 것입니다.

```react
const arr = combine([1, 2, 3], ["hello"]);
Type 'string' is not assignable to type 'number'.Type 'string' is not assignable to type 'number'.Try
```

만약 여러분이 이런 것을 의도하셨다면, 여러분은 수동으로 `Type`을 명시해야 합니다.

```react
const arr = combine<string | number>([1, 2, 3], ["hello"]);
```





#### 타입 매개변수는 두 번 나타나야 합니다.

가끔 우리는 함수가 제네릭이 필요 없을 수 있다는 사실을 간과합니다.

```react
function greet<Str extends string>(s: Str) {
  console.log("Hello, " + s);
}
 
greet("world");Try
```

우리는 간단한 버전을 쉽게 작성할 수 있었을 것입니다.

```react
function greet(s: string) {
  console.log("Hello, " + s);
}Try
```

타입 매개변수는 *여러 값의 타입을 연관*시키는 용도로 사용함을 기억해 주십시오. 만약 타입 매개변수가 함수 시그니처에서 한 번만 사용되었다면, 어떤 것도 연관시키지 않고 있는 것입니다.

> **규칙**: 만약 타입 매개변수가 한 곳에서만 나온다면, 정말로 필요한 건지 다시 생각해 보십시오.



### 콜백 함수에서의 선택적 매개변수

선택적 매개변수 및 함수 타입 표현식에 대해 알게 되면, 콜백을 호출하는 함수를 작성할 때 아래와 같은 실수를 범하기 쉽습니다.

```react
function myForEach(arr: any[], callback: (arg: any, index?: number) => void) {
  for (let i = 0; i < arr.length; i++) {
    callback(arr[i], i);
  }
}
```

사람들이 `index?`를 선택적 매개변수로 사용하기 위해 작성할 때 보통 의도하는 것은 두 호출 모두 유효하기를 바라는 것입니다.

```react
myForEach([1, 2, 3], (a) => console.log(a));
myForEach([1, 2, 3], (a, i) => console.log(a, i));Try
```

*실제로* 이것이 의미하는 바는 *`callback`이 하나의 인수로 호출될 수 있음* 입니다. 다시 말해, 이전의 함수 정의는 구현이 다음과 같을 수도 있다고 하는 것과 같습니다.

```react
function myForEach(arr: any[], callback: (arg: any, index?: number) => void) {
  for (let i = 0; i < arr.length; i++) {
    // 오늘은 index를 제공하고 싶지 않아
    callback(arr[i]);
  }
}Try
```

결국, TypeScript는 이러한 의미를 강제하여 실제로 일어나지 않을 에러를 발생시킵니다.

```react
myForEach([1, 2, 3], (a, i) => {
  console.log(i.toFixed());'i' is possibly 'undefined'.'i' is possibly 'undefined'.
});Try
```

JavaScript에서, 매개변수로 지정된 것보다 많은 인수를 전달하여 호출되면, 남은 인수들은 단순히 무시됩니다. TypeScript도 같은 방식으로 동작합니다. (같은 타입을 가진) 매개변수가 더 적은 함수는 더 많은 매개변수가 있는 함수를 대체할 수 있습니다.

> 콜백에 대한 함수 타입을 작성할 때, 해당 인수 없이 *호출할* 의도가 없는 한, *절대로* 선택적 매개변수를 사용하지 마십시오.





## 나머지 매개변수와 인수

> 배경지식 읽기:
> [나머지 매개변수(Rest Parameter)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters)
> [전개 구문(Spread Syntax)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

### 나머지 매개변수(Rest Parameter)

선택적 매개변수와 오버로드를 사용하여 다양한 정해진 인수들을 받아들일 수 있지만, 우리는 *정해지지 않은* 수의 인수를 받아들이는 함수를 *나머지 매개변수*를 이용하여 정의할 수 있습니다.

나머지 매개변수는 다른 모든 매개변수 뒤에 나타나며, `...` 구문을 사용합니다.

```react
function multiply(n: number, ...m: number[]) {
  return m.map((x) => n * x);
}
// 'a' gets value [10, 20, 30, 40]
const a = multiply(10, 1, 2, 3, 4);Try
```

TypeScript에서는, 이러한 매개변수에 대한 타입 표기는 암묵적으로 `any`가 아닌 `any[]`를 사용하며, 타입 표현식은 `Array<T>` 또는 `T[]` 또는 튜플 타입(나중에 배울 것입니다)으로 표현해야 합니다.

### 나머지 인수(Rest Argument)

반대로 우리는 전개 구문을 사용하여 배열에서 제공되는 인수의 개수를 *제공*할 수 있습니다. 예를 들어, 배열의 `push` 메서드는 인수를 몇 개든 받을 수 있습니다.

```react
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
arr1.push(...arr2);Try
```

일반적으로 TypeScript는 배열이 불변하다고 간주하지 않습니다. 이로 인해 다음과 같은 놀라운 동작이 발생할 수 있습니다.

```react
// 추론된 타입은 0개 이상의 숫자를 가지는 배열인 number[]
// 명시적으로 2개의 숫자를 가지는 배열로 간주되지 않습니다
const args = [8, 5];
const angle = Math.atan2(...args);A spread argument must either have a tuple type or be passed to a rest parameter.A spread argument must either have a tuple type or be passed to a rest parameter.Try
```

이러한 상황의 최선의 해결책은 코드에 따라서 다르지만, 일반적으로 `const` 콘텍스트가 가장 간단한 해결책입니다.

```react
// 길이가 2인 튜플로 추론됨
const args = [8, 5] as const;
// OK
const angle = Math.atan2(...args);Try
```

나머지 인수를 사용하는 것은 오래된 런타임을 대상으로 할 때, [`downlevelIteration`](https://www.typescriptlang.org/tsconfig#downlevelIteration)을 필요로 할 수 있습니다.





## 매개변수 구조 분해(Parameter Destructing)

> 배경지식 읽기:
> [구조분해 할당](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

매개변수 분해를 사용하여 인수로 제공된 객체를 함수 본문에서 하나 이상의 지역 변수로 편리하게 언팩 할 수 있습니다. JavaScript에서는 아래의 형태처럼 생겼습니다.

```react
function sum({ a, b, c }) {
  console.log(a + b + c);
}
sum({ a: 10, b: 3, c: 9 });
```

객체를 위한 타입 표기는 분해 구문 뒤에 위치하게 됩니다.

```react
function sum({ a, b, c }: { a: number; b: number; c: number }) {
  console.log(a + b + c);
}Try
```

약간 장황하게 느껴질 수 있지만, 여기에서도 이름 붙은 타입을 사용할 수 있습니다.

```react
// 이전 예제와 동일
type ABC = { a: number; b: number; c: number };
function sum({ a, b, c }: ABC) {
  console.log(a + b + c);
}
```