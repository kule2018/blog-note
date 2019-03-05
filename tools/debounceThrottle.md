## 防抖（debounce）：在没有被执行前，又触发，重新开始计时

应用场景：
- 防止连续多次点击按钮，提交信息。
- 搜索输入框，减少请求次数。
- 判断scroll是否滑到底部
- 即只需执行连续操作的最后一次

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


## 节流（throttle）：规定时间内无论被触发多少次，都执行一次

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

## 鼠标移动实例
```html
<div id="move" style="height: 500px;background-color: rgb(0, 255, 200);"></div>
```

```js
document.getElementById('move').addEventListener('mousemove', mouseMove(printLog)

function printLog(e) {
    console.log(e.clientX, e.clientY);
}

function mouseMove(callback) {
    var startTime = Date.now(), timeInterval = 2000, timeout='';

    return function (event) {
        var  timeNow = Date.now();
        // 第一次和连续动作时间间隔会执行
        if(timeNow-startTime >  timeInterval) {
            callback(event)
            startTime = timeNow
        } else {
            // 在动作完成后间隔2s执行最后一次
            clearTimeout(timeout)
            timeout = setTimeout(function() {
                console.log('last');
                startTime = timeNow
                callback(event)
            }, timeInterval);
        }
    }
}
```