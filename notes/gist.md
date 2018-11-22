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

> positive (integers or decimals) 
```js
/^[+]?\d+([.]\d+)?$/
```

> Remove the leading and trailing Spaces
```js
string.replace(/(^\s*|\s*$)/g, '')
```
---

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
---
# 防抖节流

**防抖（debounce）：在没有被执行前，又触发，重新开始计时**

应用场景：
- 防止连续多次点击按钮，提交信息。
- 搜索输入框，减少请求次数。
- 判断scroll是否滑到底部
- 即只需执行一次来获取响应的情况

```js
class Debounce {
    constructor(time) {
        this.time = time
        this.clear = null
    }

    setTime() {
        clearTimeout(this.clear)
        this.clear = setTimeout(() => {
            console.log('ececute code', new Date().getSeconds())
        }, this.time)
        
    }
}
const executeFn = new Debounce(2000)

// 模拟连续点击等操作
let i = 0
const fn = () => {
    i++
    setTimeout(() => {
        if (i<5) fn()
        executeFn.setTime()
        console.log('time', new Date().getSeconds())
    }, 500)
}

fn()
```


**节流（throttle）：规定时间内无论被触发多少次，都执行一次**

应用场景：
- 连续的操作，不仅仅是最后一次触发需要执行，中途的也需要执行，但不需太过频繁

```js
function throttle (time) {
    let startTime = Date.now()
    
    return () => {
        const nowTime = Date.now()
        if(nowTime - startTime > time){
            console.log('execute code', new Date().getSeconds())
            startTime = Date.now()
        }
    }
}

// 模拟scroll滑动操作
let i = 0
const fn = throttle(2000)
const clear = setInterval(() => {
    i++
    if (i>50) clearInterval(clear)
    fn()
    console.log('time', i)
}, 1000)

```
---




