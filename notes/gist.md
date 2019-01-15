[toc]

# RegExp

- phone number 电话号码
```js
/^(1[356789]\d|14[57])\d{8}$/
```
---

- integer 整数
```js
/(^-[1-9]|^0$|^[1-9])\d*$/
```
---

- positive integer 正整数
```js
/^[1-9]\d*$/
```
---

- positive (integers or decimals) 正数和零
```js
/(^0|^[1-9]\d*)([.]\d+)?$/
```

---

- cookie 获取某个cookie值
```js
function getCookieValue(key) {
  var reg = new RegExp(`${key}=(.*)(;|$)`, 'i')
}
```

---

- Remove the leading and trailing Spaces 删除首尾空格
```js
string.replace(/(^\s*|\s*$)/g, '')
```

---

# time format 时间格式化
```js
function formatTime(data = {}) {
    const {
        time: time = Date(),
        type: type = 'dateTime',
        dateSeparator: dateSeparator = '-',
        timeSeparator: timeSeparator = ':'
    } = data 
    const timeObj = (typeof time) === 'object' ? time : new Date(time)
    const addZeroCharacter = (n) => n < 10 ? `0${n}` : n

    let y = timeObj.getFullYear(),
        mon = timeObj.getMonth() + 1,
        day = timeObj.getDate(),
        h = timeObj.getHours(),
        m = timeObj.getMinutes(),
        s = timeObj.getSeconds();
    let re = ''

    const dateString = `${y}${dateSeparator}${addZeroCharacter(mon)}${dateSeparator}${addZeroCharacter(day)}`
    const timeString = `${addZeroCharacter(h)}${timeSeparator}${addZeroCharacter(m)}${timeSeparator}${addZeroCharacter(s)}`

    const commandObj = {
        date: () => dateString,
        time: () => timeString,
        dateTime: () => `${dateString} ${timeString}`
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

# 动态插入元素
```js
const loopInsert = (element, attribute, parent) => {
    const s = document.createElement(element);
    for (let n = 0; n < attribute.length; n++) {
        s[attribute[n].key] = attribute[n].value;
    }
    document.querySelector(parent).appendChild(s);
};

const attribute = [
    { key: 'href', value: `/a/css/b.css` }
    { key: 'rel', value: `stylesheet` }
];

loopInsert('link', attribute, 'head');

```


