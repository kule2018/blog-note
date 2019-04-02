[toc]
# 利用hash或history实现单页面路由
> 在chrome(版本 70.0.3538.110)测试正常
> 编写涉及：css, html,js, node(koa)

[在线演示codepen](https://codepen.io/Hewitt/pen/gQymam)

# html代码
```html
 <div class="hash">
        <div class="title">hash 路由</div>
        <a href="#/one">hash 1</a> <a href="#/two">hash 2</a> <a href="#/three">hash 3</a> <a onclick="hashRoute.skip('other')">other</a>
        <div id="hashContent"></div>
    </div>
    <div class="history">
        <div class="title">history 路由</div>
        <div>
            <button onclick="historyRoute.skip('pushStateOne')">history.pushState(1)</button>
            <button onclick="historyRoute.skip('pushStateTwo')">history.pushState(2)</button>
            <button onclick="historyRoute.skip('pushStateThree')">history.pushState(3)</button>
            <button onclick="historyRoute.skip('pushStateTwo')">history.replaceState(pushStateTwo)</button>
            <button onclick="historyRoute.skip('go')">history.go(2)</button>
            <button onclick="historyRoute.skip('forward')">history.forward()</button>
            <button onclick="historyRoute.skip('back')">history.back()</button>
        </div>
        <div id="historyContent"></div>
    </div>
```

# css代码
```css
.hash a {
    display: inline-block;
    padding: 5px 8px;
    margin: 10px 10px 10px 0;
    font-size: 15px;
    text-decoration: none;
    border: 0;
    cursor: pointer;
    color: #fff;
    background-color: rgb(17, 130, 236);
}
.title{
    margin: 10px 0;
    padding: 5px 8px;
    border-left: rgb(168, 168, 168) solid 2px;
    background-color: rgb(230, 230, 230);
}
.hash div:last-child{
    padding: 6px;
    min-height: 100px;
    background-color: rgb(243, 243, 243);
}

.history{
    margin: 10px 0;
}
.history button {
    margin: 10px 10px 10px 0;
    padding: 8px 10px;
    border: 0;
    color: #fff;
    background-color: rgb(250, 144, 44);
}
.history div:last-child{
    margin-top: 10px;
    padding: 6px;
    min-height: 100px;
    background-color: rgb(243, 243, 243);
}
```

# JavaScript代码
## hash方式
```js
class HashRoute {
    setRoute() {
        const commandObj = {
            one: 'page one',
            two: 'page two',
            three: 'page three'
        }
        const hashRoute = location.hash ? location.hash.slice(2) : 'one'
        let re = commandObj[hashRoute]

        document.getElementById('hashContent').innerHTML =  re ? re : 'page not find'
    }

    skip(path) {
        window.location.hash= `#/${path}`
    }

    init() {
        window.addEventListener('DOMContentLoaded', this.setRoute)

        // 1.直接更改浏览器地址，在最后面增加或改变#hash； 
        // 2.通过改变location.href 或 location.hash的值； 
        // 3.通过触发点击带锚点的链接； 
        // 4.浏览器前进后退可能导致hash的变化，前提是两个网页地址中的hash值不同
        window.addEventListener('hashchange', this.setRoute)
    }
}

const hashRoute = new HashRoute()

hashRoute.init()
```

## history 方式

### 浏览器端代码
```js
// 服务端有效
class HistoryRoute {
    constructor() {
        this.currentPath = ''
    }

    renderView(component) {
        const route = {
            pushStateOne: 'route pushState one',
            pushStateTwo: 'route pushState two',
            pushStateThree: 'route pushState three',
            replaceState: 'route replaceState',
            go: 'route go',
            forward: 'route forward',
            back: 'route back',
            notFind: 'not find',
        }
        document.getElementById('historyContent').innerHTML = route[component]
    }

    // 这里所有涉及的跳转都用js方式，不采用a标签(采用a标签请设置拦截)
    skip(path) {
        const commandObj = {
            pushStateOne: () => {
                history.pushState({ path }, path,path)
                this.renderView(path)
            },
            pushStateTwo: () => {
                history.pushState({ path }, path, path)
                this.renderView(path)
            },
            pushStateThree: () => {
                history.pushState({ path }, path, path)
                this.renderView(path)
            },
            replaceState: () => {
                // 是用来修改当前的history实体而不是创建一个新的,比如跳转顺序为1，2，3，1执行replaceState(2),再执行back()，返回1，而不是3
                history.replaceState({ path }, path, path)
                this.renderView(path)
            },
            go: () => {
                history.go(2)
                this.renderView('go')
            },
            forward: () => {
                history.forward()
                this.renderView('forward')
            },
            back: () => {
                history.back()
            },

        }

        this.currentPath = path;
        commandObj[path]()
    }

    init() {
        window.addEventListener('DOMContentLoaded', () => {
            // 针对F5刷新问题:
            // 1.可以使用？后面跟参数形式
            // 2.统一入口利用忽略地址方式（后端配置 /page/:path 忽略page后跟的所有地址，通过前端去请求page后的对应路由数据，如下）

            const path = location.href.split('/page/') 
            this.skip(path[1])
        })

        // 调用history.pushState()或history.replaceState()不会触发popstate。
        // 只有在用户点击前进回退按钮，(或history.back()，forward，go)
        window.addEventListener('popstate', (event) => {
            console.log('popstate', this.currentPath, event.state);
            const { state } = event
            if (state && state.path) {
                this.renderView(state.path)
            } else {
                this.renderView('404')
            }
        })
    }
}

const historyRoute = new HistoryRoute()

historyRoute.init();
```

### 服务器端
```js
// 结合前端，可以用以下方式处理
router.get('/page/:path', (ctx, next) => {
    ctx.response.type = 'html';
    // 此处的singlePageRoute.html为单页面html容器，即放置本文中的所有代码文件
    ctx.response.body = fs.createReadStream('./dist/public/files/singlePageRoute.html');
    return next();
})
```

> 若有疑问或错误，请留言，谢谢！[Github blog issues](https://github.com/NameHewei/blog/issues)