# 과제 - 요소 검색하기

https://ko.javascript.info/task/find-elements

```html
<html>

<head>
    <style>
        table,tr,td{
            border: solid;
            border-collapse: collapse;
        }
    </style>
</head>

<body>
    xxxxxxxxxxxxxxxxxxxx
    <table>
        <tr>
            zxczxczxc
        </tr>
        <tr>
            <td>1</td>
            <td>2</td>
            <td>3</td>
        </tr>
        xbxcvxc
    </table>
    xcbxcxv
</body>

<script>


</script>

</html>
```



# input

## Zero or more 'td' and/or 'th' elements; script-supporting elements (script and template) are also allowed



tr에는 text node의 삽입을 스펙에서 제한하고 있다. 기본적으로 tr태그 안에 들어간 text는 상위로 방출되는 case이다.