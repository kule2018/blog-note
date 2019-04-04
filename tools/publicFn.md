[toc]

# 公用方法

## ajax

```javascript
function ajaxFn() {
    // IE5,6用 new ActiveXObject('Microsoft.XMLHTTP');
    var xhr=new XMLHttpRequest();  
    xhr.open('get','https://updateapp001.sinaapp.com/version.php',true);（true表示异步）//规定请求的内容
    xhr.send(null);//将请求发送到服务器
    xhr.onreadystatechange=function(){//这个事件函数放在哪里都可
        if(xhr.readyState==4){//针对open方法可以调用并且接受了全部响应数据
                if(xhr.status==200){//响应的http状态
                    alert(xhr.responseText);
                }
        }
    };
} 
```
status 200表示成功，304表示 资源没有修改可以直接使用浏览器缓存

必须在调用open()方法之后且调用send()方法之前调用setRequestHeader()


## 批量动态插入元素
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

## time format 时间格式化
moment.js | Day.js(https://github.com/iamkun/dayjs)
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

## 浏览器全屏
```js
function fullScreen() {
    // 方法必须放到用户触发的事件里面  
    e.click(function(){  
        document.documentElement.webkitRequestFullScreen();  
        document.webkitExitFullScreen();//退出全屏  
    })  
    // 除了opera不加前缀，还有moz；ie暂不支持；  
    // IE中用  
    function a(){  
        var b=new ActiveXObject("Wscript.shell");  
        b.sendKeys("{F11}");  
    }  
    a()
}
```
