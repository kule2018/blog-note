# 正则匹配

> phone number
```js
/^(1[356789]\d|14[57])\d{8}$/
```

> replace all non-numeric characters and starting with 0
```js
replace(/^[^1-9]+|[^\d]+/g, '')
```

> integer
```js
/(^-[1-9]|^0$|^[1-9])\d*$/
```

> positive integer
```js
/^[1-9]\d*$/
```

> cookie
```js
function getCookieValue(key) {
  var reg = new RegExp(`${key}=(.*)(;|$)`, 'i')
}
```

> positive (integers or decimals) 
```js
/^[+]?\d+([.]\d+)?$/
```