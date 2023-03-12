# canvas

```javascript
var ctx = canvas.getContext(contextType);
```



**contextType**

Is a [`DOMString`](https://developer.mozilla.org/en-US/docs/Web/API/DOMString) containing the context identifier defining the drawing context associated to the canvas. Possible values are:

- `"2d"`, leading to the creation of a [`CanvasRenderingContext2D`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D) object representing a two-dimensional rendering context.

```javascript
// take any image
let img = document.querySelector('img');

// make <canvas> of the same size
let canvas = document.createElement('canvas');
canvas.width = img.clientWidth;
canvas.height = img.clientHeight;

let context = canvas.getContext('2d');

// copy image to it (this method allows to cut image)
context.drawImage(img, 0, 0);
// we can context.rotate(), and do many other things on canvas

// toBlob is async operation, callback is called when done
canvas.toBlob(function(blob) {
  // blob ready, download it
  let link = document.createElement('a');
  link.download = 'example.png';

  link.href = URL.createObjectURL(blob);
  link.click();

  // delete the internal blob reference, to let the browser clear memory from it
  URL.revokeObjectURL(link.href);
}, 'image/png');
```



```javascript
// get readableStream from blob
const readableStream = blob.stream();
const stream = readableStream.getReader();

while (true) {
  // for each iteration: data is the next blob fragment
  let { done, data } = await stream.read();
  if (done) {
    // no more data in the stream
    console.log('all blob processed.');
    break;
  }

   // do something with the data portion we've just read from the blob
  console.log(data);
}
```



The HTML `<canvas>` element is used to draw graphics on a web page.

The graphic to the below is created with `<canvas>`. It shows four elements: a red rectangle, a gradient rectangle, a multicolor rectangle, and a multicolor text.

# HTML canvas stroke() Method

The stroke() method of the HTML canvas is used to draw the path. This path is drawn with moveTo() and lineTo() method. The <canvas> element allows you to draw graphics on a web page using JavaScript. Every canvas has two elements that describes the height and width of the canvas i.e. height and width respectively.



# CanvasRenderingContext2D.lineTo()

The [`CanvasRenderingContext2D`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D) method **`lineTo()`**, part of the Canvas 2D API, adds a straight line to the current sub-path by connecting the sub-path's last point to the specified `(x, y)` coordinates.

Like other methods that modify the current path, this method does not directly render anything. To draw the path onto a canvas, you can use the [`fill()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/fill) or [`stroke()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/stroke) methods.

## [Syntax](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineTo#syntax)

```
ctx.lineTo(x, y);
```

Copy to Clipboard

### [Parameters](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/lineTo#parameters)

- `x`

  The x-axis coordinate of the line's end point.

- `y`

  The y-axis coordinate of the line's end point.



# HTMLCanvasElement.toBlob()

The **`HTMLCanvasElement.toBlob()`** method creates a [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) object representing the image contained in the canvas. This file may be cached on the disk or stored in memory at the discretion of the user agent.

The desired file format and image quality may be specified. If the file format is not specified, or if the given format is not supported, then the data will be exported as `image/png`. Browsers are required to support `image/png`; many will support additional formats including `image/jpg` and `image/webp`.

The created image will have a resolution of 96dpi for file formats that support encoding resolution metadata.

## [Syntax](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/toBlob#syntax)

```
toBlob(callback, type, quality)
```

Copy to Clipboard

### [Parameters](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/toBlob#parameters)

- `callback`

  A callback function with the resulting [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) object as a single argument. `null` may be passed if the image cannot be created for any reason.

- `type` Optional

  A [`DOMString`](https://developer.mozilla.org/en-US/docs/Web/API/DOMString) indicating the image format. The default type is `image/png`; that type is also used if the given type isn't supported.

- `quality` Optional

  A [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) between `0` and `1` indicating the image quality to be used when creating images using file formats that support lossy compression (such as `image/jpeg` or `image/webp`). A user agent will use its default quality value if this option is not specified, or if the number is outside the allowed range.

