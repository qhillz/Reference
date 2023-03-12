# Array.prototype.findIndex()

The **`findIndex()`** method returns the **index** of the first element in the array **that satisfies the provided testing function**. Otherwise, it returns `-1`, indicating that no element passed the test.

```javascript
const array1 = [5, 12, 8, 130, 44];

const isLargeNumber = (element) => element > 13;

console.log(array1.findIndex(isLargeNumber));
// expected output: 3
```

### [Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex#parameters)

- `callbackFn`

  A function to execute on each value in the array until the function returns `true`, indicating that the satisfying element was found.It takes three arguments:`element`The current element being processed in the array.`index` OptionalThe index of the current element being processed in the array.`array` OptionalThe array `findIndex()` was called upon.'

  

  element

  The current element being processed in the array.

  `index` Optional

  The index of the current element being processed in the array.

  `array` Optional

  The array `findIndex()` was called upon.

  

- `thisArg` Optional

  Optional object to use as `this` when executing `callbackFn`.



### [Return value](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex#return_value)

The index of the first element in the array that passes the test. Otherwise, `-1`.

Note: if the index of the first element in the array that passes the test is `0`, the return value of `findIndex` will be interpreted as [Falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) in conditional statements.



**Arr.push는 기존 존재하는 배열의 공간을 늘리면서 추가하는 것이다.**

