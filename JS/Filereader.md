# Filereader

[FileReader](https://www.w3.org/TR/FileAPI/#dfn-filereader) is an object with the sole purpose of reading data from `Blob` (and hence `File` too) objects.

It delivers the data using events, as reading from disk may take time.

The constructor:

```javascript
let reader = new FileReader(); // no arguments
```

As `File` inherits from `Blob`

The main methods:

- **`readAsArrayBuffer(blob)`** – read the data in binary format `ArrayBuffer`.
- **`readAsText(blob, [encoding])`** – read the data as a text string with the given encoding (`utf-8` by default).
- **`readAsDataURL(blob)`** – read the binary data and encode it as base64 data url.
- **`abort()`** – cancel the operation.

As the reading proceeds, there are events:

- `loadstart` – loading started.
- `progress` – occurs during reading.
- `load` – no errors, reading complete.
- `abort` – `abort()` called.
- `error` – error has occurred.
- `loadend` – reading finished with either success or failure.

When the reading is finished, we can access the result as:

- `reader.result` is the result (if successful)
- `reader.error` is the error (if failed).

**`FileReader` for blobs**

As mentioned in the chapter [Blob](https://javascript.info/blob), `FileReader` can read not just files, but any blobs.

We can use it to convert a blob to another format:

- `readAsArrayBuffer(blob)` – to `ArrayBuffer`,
- `readAsText(blob, [encoding])` – to string (an alternative to `TextDecoder`),
- `readAsDataURL(blob)` – to base64 data url.



In many cases though, we don’t have to read the file contents. Just as we did with blobs, we can create a short url with `URL.createObjectURL(file)` and assign it to `<a>` or `<img>`. This way the file can be downloaded or shown up as an image, as a part of canvas etc.

js엔진에서 자연스럽게 해석되기 위해서는 정해진 encode 규칙이 존재할 것이다.



