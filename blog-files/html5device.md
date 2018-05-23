[toc]
# HTML5 device access 设备访问

## camera api (含图片预览)
> [参考地址](https://developer.mozilla.org/en-US/docs/Archive/B2G_OS/API/Camera_API/Introduction)

- 主要为利用input type=file, accept="image/*" 进行处理
- 图片预览方式（两种）

```js   
const file = e.target.files[0]
// 方式1 
const url1 = window.URL.createObjectURL(file);
let url2

// 方式2
const reader = new FileReader();
reader.onload = (e) => {
    url2 = e.target.result;
};
reader.readAsDataURL(file);
``` 

## touch events (触屏事件)
> [参考地址](https://developer.mozilla.org/en-US/docs/Web/API/Touch_events)

- touchstart
- touchen
- touchcancel **电话的接入或者弹出信息等比较高级的事件触发，一般做保存操作**
- touchmove

## geolocation 
> [参考地址](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/Using_geolocation)

- 注意谷歌浏览器要https才能提供定位服务

```js
    if (navigator.geolocation){
        navigator.geolocation.getCurrentPosition((position) => {
            this.geolocation = `latitude:${position.coords.latitude},longitude:${position.coords.longitude}`
        }, (err) => {
            console.log(err);
        }, {
                enableHighAccuracy: true, 
                maximumAge        : 30000,  // buffer memory timre
                timeout           : 27000   // waiting time 
        })
    } else {
        alert('geolocation not supported!')
    }
```

## device orientation and motion
> [参考地址](https://developer.mozilla.org/en-US/docs/Web/API/Detecting_device_orientation)

```js
    window.addEventListener('deviceorientation',(doe) => {
        this.absolute = doe.absolute //false 表示方向数据由设备本身坐标系提供
        this.alpha = doe.alpha // 绕Z轴0-360 进入时手机水平正对的方向为0或360
        this.beta = doe.beta // 绕X轴-180~180 描述由前向后旋转
        this.gamma = doe.gamma // 绕Y轴-90~90 描述由左向右旋转
    }, true)

    // chrome v65 只支持accelerationIncludingGravity和interval（应该因为一些限制没有找到），其它浏览器最新版基本都支持
    window.addEventListener('devicemotion', (dme) => {
        this.acceleration = dme.acceleration
        this.accelerationIncludingGravity = dme.accelerationIncludingGravity
        this.rotationRate = dme.rotationRate
        this.interval  = dme.interval 
    }, false)
```

## Pointer Lock(鼠标锁定)
> [参考地址](https://developer.mozilla.org/en-US/docs/Web/API/Pointer_Lock_API)

```html
    <button onclick="lockPointer();">锁住它!</button>
    <div id="pointer-lock-element" style="width:500px;height:500px;background-color: red"></div>
```

```js

    // 简单示例，将鼠标锁定在 pointer-lock-element 元素内
    let = document.getElementById("pointer-lock-element");
    
    document.addEventListener("mousemove", function(e) {
        var movementX = e.movementX 
            movementY = e.movementY

        // 打印鼠标移动的增量值。
        console.log("X=" + movementX, "Y=" + movementY);
    }, false);

    function lockPointer() {
        elem = document.getElementById("pointer-lock-element");
        elem.requestPointerLock = elem.requestPointerLock    ||
                            elem.mozRequestPointerLock ||
                            elem.webkitRequestPointerLock;
        elem.requestPointerLock();
    }
```

