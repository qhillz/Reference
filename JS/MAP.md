# MAP

The **`Map`** object holds key-value pairs and remembers the original insertion order of the keys.

A `Map` object iterates its elements in insertion order — a [`for...of`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of) loop returns an array of `[key, value]` for each iteration.

- 키의 타입에 제약이 없습니다. 객체도 키가 될 수 있습니다.
- `size` 프로퍼티 등의 유용한 메서드나 프로퍼티가 있습니다.

## Introduction to JavaScript Map object

Before ES6, we often used an [object](https://www.javascripttutorial.net/javascript-objects/) to emulate a map by mapping a key to a value of any type. But using an object as a map has some side effects:

1. An object always has a default key like the [prototype](https://www.javascripttutorial.net/javascript-prototype/).
2. **A key of an object must be a [string](https://www.javascripttutorial.net/javascript-string/) or a [symbol](https://www.javascripttutorial.net/es6/symbol/), you cannot use an object as a key.**
3. An object does not have a property that represents the size of the map.

