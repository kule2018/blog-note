# 元素内容垂直循环滚动

## CSS
```css
ul,li {  padding: 0; margin: 0 }
.roll-box {
      height: 400px;
      background: #007acc;
      overflow: hidden;
      color: #fff;
 }
#roll li {
      height: 25px;
      border-bottom: 1px solid #ddd
}
```

## HTML
```html
<div class="roll-box">
    <ul id="roll">
    </ul>
</div>
```

## JS
```js
function getData() {
    var htmlStr = '';
    for (var i = 0; i < 20; i++) {
        htmlStr += '<li id="i-' + i + '">' + 'this is ' + i + '</li>'
    }

    return htmlStr;
}

(function roll() {
    var UL_HEIGHT = 400, SPEED = 100, LI_HEIGHT = 25;

    var ulObj = document.getElementById('roll');
    ulObj.innerHTML = getData();

    var height = ulObj.offsetHeight;
    var move = 0;
    var clearIn = '', mouseOut = true;

    // 添加鼠标操作相关事件
    ulObj.addEventListener('mouseenter',function(){
        mouseOut = false
    });
    ulObj.addEventListener('mouseleave',function(){
        mouseOut = true
        animationRoll()
    });
    ulObj.addEventListener('click',function(e){
        if(e.target.nodeName === 'LI') {
            alert('id is:' + e.target.id)
        }
    });
    
    // 滚动步骤
    // 1.将外部 ul 移动一个li的高度的距离 
    // 2.将移出的li元素放到最后，实现循环，并复原ul的移动距离。
    function animationRoll() {
        clearIn = setInterval(function () {
            if(mouseOut){
                move++;
                ulObj.setAttribute('style', 'margin-top:-' + move + 'px');
                if (move === LI_HEIGHT) {
                    move = 0;
                    ulObj.setAttribute('style', 'margin-top:-' + move + 'px');
                    var temp = ulObj.children[0];
                    ulObj.removeChild(temp)
                    ulObj.appendChild(temp)
                }
            } else {
                clearInterval(clearIn);
            }
        }, SPEED)
    }

    if (height > UL_HEIGHT) {
        animationRoll()
    } else {
        console.log(ulObj.offsetHeight);
    }
})()
```

> 欢迎交流 [Github](https://github.com/NameHewei/blog-note)