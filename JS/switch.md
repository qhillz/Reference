# switch

The **`switch`** statement evaluates an [expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators), matching the expression's value to a `case` clause, and executes [statements](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements) associated with that `case`, as well as statements in `case`s that follow the matching `case`.



```javascript
const expr = 'Papayas';
switch (expr) {
  case 'Oranges':
    console.log('Oranges are $0.59 a pound.');
    break;
  case 'Mangoes':
  case 'Papayas':
    console.log('Mangoes and papayas are $2.79 a pound.');
    // expected output: "Mangoes and papayas are $2.79 a pound."
    break;
  default:
    console.log(`Sorry, we are out of ${expr}.`);
}
```

