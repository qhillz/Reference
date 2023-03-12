# FormData

The special thing about `FormData` is that network methods, such as `fetch`, can accept a `FormData` object as a body. It’s encoded and sent out with `Content-Type: multipart/form-data`.

HTML form을 fetch메소드를 활용하서 server에 request할 수 있는 방식이다.



There’s also method `set`, with the same syntax as `append`. The difference is that `.set` removes all fields with the given `name`, and then appends a new field. So it makes sure there’s only one field with such `name`, the rest is just like `append`:

- `formData.set(name, value)`,
- `formData.set(name, blob, fileName)`.



## [Sending a form with Blob data](https://ko.javascript.info/formdata#ref-1589)

As we’ve seen in the chapter [fetch](https://ko.javascript.info/fetch), it’s easy to send dynamically generated binary data e.g. an image, as `Blob`. We can supply it directly as `fetch` parameter `body`.

In practice though, it’s often convenient to send an image not separately, but as a part of the form, with additional fields, such as “name” and other metadata.



formData를 활용하여 기존의 HTML form을 name / value 형식으로 프레임화 시킨다.

여기서 append와 set을 활용하여 파일이나 'name/value' 형태를 fetch 요청 할 수 있게 만든다.



[FormData](https://xhr.spec.whatwg.org/#interface-formdata) objects are used to capture HTML form and submit it using `fetch` or another network method.

We can either create `new FormData(form)` from an HTML form, or create an object without a form at all, and then append fields with methods:

- `formData.append(name, value)`
- `formData.append(name, blob, fileName)`
- `formData.set(name, value)`
- `formData.set(name, blob, fileName)`

Let’s note two peculiarities here:

1. The `set` method removes fields with the same name, `append` doesn’t. That’s the only difference between them.
2. To send a file, 3-argument syntax is needed, the last argument is a file name, that normally is taken from user filesystem for `<input type="file">`.

Other methods are:

- `formData.delete(name)`
- `formData.get(name)`
- `formData.has(name)`