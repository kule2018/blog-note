# 正则匹配

> phone number 电话号码
```js
/^(1[356789]\d|14[57])\d{8}$/
```

> replace all non-numeric characters and starting with 0 替换所有0和非数字字符串
```js
replace(/^[^1-9]+|[^\d]+/g, '')
```

> integer 整数
```js
/(^-[1-9]|^0$|^[1-9])\d*$/
```

> positive integer 正整数
```js
/^[1-9]\d*$/
```

> cookie
或使用：https://github.com/js-cookie/js-cookie
```js
function getCookieValue(key) {
  var reg = new RegExp(`${key}=([^&]*)`, 'i')
}
```

> positive (integers or decimals) 正数和零
```js
/(^0|^[1-9]\d*)([.]\d+)?$/
```

> Remove the leading and trailing Spaces 删除首尾空格
```js
string.replace(/(^\s*|\s*$)/g, '')
```