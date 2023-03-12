# How to abort Asynchronous task

There’s a special built-in object for such purposes: `AbortController`. It can be used to abort not only `fetch`, but other asynchronous tasks as well.

The usage is very straightforward:

## [The AbortController object](https://javascript.info/fetch-abort#the-abortcontroller-object)

Create a controller:

```javascript
let controller = new AbortController();
```

A controller is an extremely simple object.

- It has a single method `abort()`,
- And a single property `signal` that allows to set event listeners on it.

When `abort()` is called:

- `controller.signal` emits the `"abort"` event.
- `controller.signal.aborted` property becomes `true`.

Generally, we have two parties in the process:

1. The one that performs a cancelable operation, it sets a listener on `controller.signal`.
2. The one that cancels: it calls `controller.abort()` when needed.

When a fetch is aborted, its promise rejects with an error `AbortError`, so we should handle it, e.g. in `try..catch`.

Fetch메소드를 실행시키면 promise로 관리.

```javascript
let controller = new AbortController();
let signal = controller.signal;

// The party that performs a cancelable operation
// gets the "signal" object
// and sets the listener to trigger when controller.abort() is called
signal.addEventListener('abort', () => alert("abort!"));

// The other party, that cancels (at any point later):
controller.abort(); // abort!

// The event triggers and signal.aborted becomes true
alert(signal.aborted); // true
```



**with the fetch()**

```javascript
// abort in 1 second
let controller = new AbortController();
setTimeout(() => controller.abort(), 1000);

try {
  let response = await fetch('/article/fetch-abort/demo/hang', {
    signal: controller.signal
  });
} catch(err) {
  if (err.name == 'AbortError') { // handle abort()
    alert("Aborted!");
  } else {
    throw err;
  }
}
```

