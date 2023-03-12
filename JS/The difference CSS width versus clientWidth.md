### [The difference: CSS width versus clientWidth](https://ko.javascript.info/size-and-scroll#ref-420)



중요도: 5

What’s the difference between `getComputedStyle(elem).width` and `elem.clientWidth`?

Give at least 3 differences. The more the better.

해답

Differences:

1. `clientWidth` is numeric, while `getComputedStyle(elem).width` returns a string with `px` at the end.
2. `getComputedStyle` may return non-numeric width like `"auto"` for an inline element.
3. `clientWidth` is the inner content area of the element plus paddings, while CSS width (with standard `box-sizing`) is the inner content area *without paddings*.
4. If there’s a scrollbar and the browser reserves the space for it, some browser substract that space from CSS width (cause it’s not available for content any more), and some do not. The `clientWidth` property is always the same: scrollbar size is substracted if reserved.