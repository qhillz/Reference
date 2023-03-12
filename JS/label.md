## label

- label은 폼의 양식에 이름 붙이는 태그입니다.
- 주요 속성은 for입니다. label의 for의 값과 양식의 id의 값이 같으면 연결됩니다.
- label을 클릭하면, 연결된 양식에 입력할 수 있도록 하거나, 체크를 하거나, 체크를 해제합니다.

## 예제

- input 요소에 label을 붙인 간단한 예제입니다.

```
<!doctype html>
<html lang="ko">
	<head>
	<meta charset="utf-8">
		<title>HTML</title>
	</head>
	<body>
		<p>
			<label for="jb-input-text">Input - Text</label>
			<input type="text" id="jb-input-text">
		</p>
		<p>
			<label for="jb-input-checkbox">Input - Checkbox</label>
			<input type="checkbox" id="jb-input-checkbox">
		</p>
	</body>
</html>
```

![img](https://www.codingfactory.net/wp-content/uploads/html-tag-label-01.gif)

## Tip

input 등 양식을 label로 감싸면, id와 for가 없이도 같은 결과를 얻을 수 있습니다.

```javascript
<!doctype html>
<html lang="ko">
  <head>
  <meta charset="utf-8">
    <title>HTML</title>
  </head>
  <body>
    <p>
      <label>Input - Text
      <input type="text">
      </label>
    </p>
    <p>
      <label>Input - Checkbox
      <input type="checkbox">
      </label>
    </p>
  </body>
</html>
```