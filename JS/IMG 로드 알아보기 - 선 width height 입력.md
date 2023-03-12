# IMG 로드 알아보기 - 선 width height 입력.



**Attention: the pitfall!**

The code won’t work reliably while `<img>` has no width/height:

```markup
<img src="ball.png" id="ball">
```

When the browser does not know the width/height of an image (from tag attributes or CSS), then it assumes them to equal `0` until the image finishes loading.

So the value of `ball.offsetWidth` will be `0` until the image loads. That leads to wrong coordinates in the code above.

After the first load, the browser usually caches the image, and on reloads it will have the size immediately. But on the first load the value of `ball.offsetWidth` is `0`.

We should fix that by adding `width/height` to `<img>`:

```markup
<img src="ball.png" width="40" height="40" id="ball">
```

…Or provide the size in CSS:

```css
#ball {
  width: 40px;
  height: 40px;
}
```