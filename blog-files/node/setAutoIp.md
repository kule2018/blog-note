[toc]

# node获取本机动态IP,并对应修改相关JavaScript文件的IP地址

> 时间：2018-08-02

> 注意：在win10环境运行无问题

## 由于本机是自动获取分配的动态IP，所以每次重启后需要重新更改与IP相关文件

```js
const os = require('os')
const fs = require('fs') 

// 需要修改的文件地址
const FILE_URL = 'your file url'

// 由于node没有提供直接获取本机IP的方法所以用以下方法迂回解决
// 可打印NETWORK查看信息
const NETWORK = os.networkInterfaces()
let CURRENT_IP = ''

Object.keys(NETWORK).forEach((v => {
    for (let i = 0; i < NETWORK[v].length; i++) {
        if(!NETWORK[v][i].internal&&NETWORK[v][i].family.toLocaleLowerCase() === 'ipv4') CURRENT_IP =  NETWORK[v][i].address  
    }
}));

// 修改文件内容
fs.readFile(FILE_URL, 'utf8', (err, data) => {
    if (err) throw err
    // 这里的正则根据文件具体代码而定
    const _data = data.replace(/ip = .+/g, `ip = '${CURRENT_IP}';`)
    fs.writeFile(FILE_URL, _data, (err) => {
        if (err) throw err
        console.log(`已修改为当前动态IP:${CURRENT_IP}`);
    })
})
```

## 参考
- [node os api](https://nodejs.org/dist/latest-v8.x/docs/api/os.html)

- [node fs api](https://nodejs.org/dist/latest-v8.x/docs/api/fs.html)

> 欢迎交流 [Github](https://github.com/NameHewei/blog-note)
