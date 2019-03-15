[toc]

---

安装路径： C:\Users\hewei\AppData\Local\Programs\Microsoft VS Code

用户配置

settings.json
```json
{
    // 定义 VSCode 的显示语言
    // 请参阅 https://go.microsoft.com/fwlink/?LinkId=761051，了解支持的语言列表
    // 更改此值需要重启 VSCode
    "locale":"en-US",
    "workbench.colorTheme": "Monokai",
    //eslint 配置解释可以setting查看
    "editor.fontSize": 15,
    "eslint.enable": true,
    "eslint._legacyModuleResolve": true,
    "eslint.alwaysShowStatus": true,
    // 在保存时自动修复
    "eslint.autoFixOnSave": true,
    // 使如下语言生效
    "eslint.validate": [ 
        "javascript",
        "javascriptreact",
        "html",
        { "language": "vue", "autoFix": true }
    ],
    "terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe",

    // 装了插件后可以不配置
    "markdown.styles": [
        "C:\\Program Files (x86)\\Microsoft VS Code\\github.css"
    ],

    // 拼写检测支持vue文件
    "cSpell.enabledLanguageIds": [
        "vue"
    ]
}
```

插件迁移

将 C:\Users\hewei\.vscode(注意前面的.) 下的 extensions 文件夹拷贝到其它电脑对应的位置即可

snippets位置

C:\Users\hewei\AppData\Roaming\Code\User\snippets

---

- ctrl+d 选中当前单词 连续操作可选中下一个相同单词

---
**Ctrl+P**

- 直接输入文件名，快速打开文件

- ? 列出当前可执行的动作  相当于帮助

- ! 显示Errors或Warnings，也可以Ctrl+Shift+M

- : 跳转到行数，也可以Ctrl+G直接进入

- @ 跳转到symbol（搜索变量或者函数），也可以Ctrl+Shift+O直接进入

- @:根据分类跳转symbol，查找属性或函数，也可以Ctrl+Shift+O后输入:进入

- #根据名字查找symbol，也可以Ctrl+T