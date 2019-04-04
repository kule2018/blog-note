[toc]
# requestAnimationFrame 兼容方案
> 编写涉及：css, html, js

[在线演示codepen](https://codepen.io/Hewitt/pen/VgZapr)

# html代码
```html
<div class="roll-box">
    <div class="inner-box">move</div>
</div>

<button onclick="startMove()"> start move</button>
```

# css代码
```css
.roll-box {
    position: relative;
    width: 600px;
    height: 400px;
    background: #007acc;
    overflow: hidden;
    color: #fff;
}
.inner-box {
    position: absolute;
    top: 10px;
    left: 0;
    width: 50px;
    height: 50px;
    text-align: center;
    line-height: 50px;
    background-color: rgb(245, 152, 30);
}
button{
    margin-top: 20px;
    padding: 6px 10px;
    border: 0;
    color: #fff;
    background-color: rgb(39, 133, 240);
}
```

# JavaScript代码

```js      
let moveCount = 0;
let rafId = '';
const ele = document.querySelector('.inner-box');

window.requestAniFrame = (function () {
    return window.requestAnimationFrame

        // Older versions Chrome/Webkit
        window.webkitRequestAnimationFrame ||

        // Firefox < 23
        window.mozRequestAnimationFrame ||

        // opera
        window.oRequestAnimationFrame ||

        // ie
        window.msRequestAnimationFrame ||

        function (callback) {
            return window.setTimeout(callback, 1000 / 60);
        };
})()

window.cancelAnimation = (function () {
    return window.cancelAnimationFrame || window.mozCancelAnimationFrame || window.cancelRequestAnimationFrame || function (id) { clearTimeout(id) }
})()

function moveFn() {
    ele.setAttribute('style', 'left:' + moveCount + 'px');
    moveCount++

    if (moveCount > 550) {
        window.cancelAnimation(rafId)
    } else {
        rafId = window.requestAniFrame(moveFn)
    }
}

function startMove() {
    // 必须先清除，否者多次点击会生成多个动画帧，导致元素移动速度加快
    window.cancelAnimation(rafId)
    rafId = window.requestAniFrame(moveFn)
}
```

> 欢迎交流 [Github](https://github.com/NameHewei/blog-note)