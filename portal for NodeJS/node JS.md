# node JS

console.log(__dirname + url);

__dirname : 루트 폴더
url : 파일이름.

```javascript
response.end(fs.readFileSync(__dirname + url));
```

현재 루트폴더(__dirname)에서 파일(url)을 읽고 response로 전달시키는 함수.



Template Literal 은 띄어쓰기 character가 필요없음.



```html
  <head>
      <title>WEB1 - ${title}</title>
      <meta charset="utf-8">
  </head>
```

페이지 제목을 나타냄.