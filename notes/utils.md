[toc]

# RegExp

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

# time format
```js
function(dateString = Date(), type = 'date', separator = '/') {
    const date = (typeof dateString) === 'object' ? dateString : new Date(dateString)
    
    const addZero = (n) => n < 10 ? `0${n}` : n

    let y = date.getFullYear(),
        mon = date.getMonth() + 1,
        day = date.getDate(),
        h = date.getHours(),
        m = date.getMinutes(),
        s = date.getSeconds();

    let re = ''

    const commandObj = {
        date: () => `${y}${separator}${addZero(mon)}${separator}${addZero(day)}`,
        time: () => `${addZero(h)}${separator}${addZero(m)}${separator}${addZero(s)}`,
        dateTime: () => `${y}${separator}${addZero(mon)}${separator}${addZero(day)} ${addZero(h)}${separator}${addZero(m)}${separator}${addZero(s)}`
    }

    return commandObj[type]()
}
```