[toc]

# iView 实现可编辑表格
> create at： 2019-02-20

## 组件 
```html
    <i-table highlight-row ref="currentRowTable" :columns="columns" :data="tableData"></i-table>
```

实现方式：

- 记录当前需要编辑的列的id，默认为空
- 需要编辑的列与当前需要编辑的id进行匹配，成功则将该列渲染为包含input标签组件，并绑定input事件

## 数据处理
```js
export default {
    data () {
        return {
            currentId: '',
            currentScore: '',
            columns: [
                { title: '名称', key: 'name', align: 'center' },
                {
                title: '班级',
                align: 'center',
                render: (h, p) => {
                    const { id, score } = p.row
                    const inp = h('input', {
                    style: {
                        width: '30%',
                        padding: '4px 2px',
                        borderRadius: '4px',
                        border: '1px solid #e9eaec',
                        textAlign: 'center'
                    },
                    attrs: {
                        maxlength: 16
                    },
                    domProps: {
                        value: score
                    },
                    on: {
                            input: (event) => {
                            this.currentScore = event.target.value
                        }
                    }
                    })
                    return this.currentId === p.row.id ? inp : h('span', score)
                }
                },
                {
                title: '操作',
                align: 'center',
                render: (h, p) => {
                    const { currentId } = this
                    const { id } = p.row
                    const btnEdit = h('i-button', {
                    on: {
                        click: () => {
                            this.currentId = id
                        }
                    }
                    }, '编辑')

                    const btnSaveCancel = [
                        h('i-button', {
                            on: {
                            click: () => {
                                this.handleSave(id)
                            }
                            }
                        }, '保存'),
                        h('i-button', {
                            on: {
                            click: () => {
                                this.currentId = ''
                                this.currentScore = ''
                            }
                            }
                        }, '取消')]
                    return currentId === id ? h('div', btnSaveCancel) : btnEdit
                }
                }
            ],
            tableData: [
                { id: 1, name: 1, score: 1 },
                { id: 2, name: 2, score: 2 }]
        }
    },

    methods: {
        handleSave (id) {
            const {currentScore, tableData} = this
            this.tableData = tableData.map(v => {
                return v.id === id ? { ...v, score: currentScore } : v
            })
            this.currentId = ''
            this.currentScore = ''
        }
    }
}
```

注意： 如果采用的是在 head 标签中引入 iView，该方法在项目中会失效；通过编译开发的项目可行；

> 欢迎交流 [Github](https://github.com/NameHewei/blog-note)