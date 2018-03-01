# iview自定义实现多级表头

> 原理：利用多个Table组件通过显示和隐藏thead和tbody来拼接表格（较粗暴）

![](https://images2018.cnblogs.com/blog/974585/201803/974585-20180301133036728-24393396.png)

---
### html
```html
<div style="margin: 50px">
    <Table class="ud-table-no-body" :columns="columns0" :data="dataNull" border></Table>
    <Table class="ud-table-no-body ud-no-t-b ud-no-b-b" :columns="columns1" :data="dataNull" border></Table>
    <Table class="ud-table-no-body ud-no-b-b" :columns="columns2" :data="dataNull" border></Table>
    <Table class="ud-table-no-header" :columns="columns" :data="data" border></Table>
</div>
```

---
### javascript
- 非合并而来的列，请注意设置宽度（如下的宽度160）否则会被均分导致下面的行的列宽度不一致
- 这里是表格列数不固定的示例

```javascript
data() {
    return {
        columns0: [],
        columns1: [],
        columns2: [],
        columns: [],
        dataNull: [],
        data: [
            {
                name: 'Hewitt',
                values: [10, 11, 12, 13, 14, 15]
            }
        ],

        dates: []
    };
},

created() {
    const dates = [2016, 2017];
    const WIDTH = 160;

    this.columns0 = [{ title: '模块名称', width: WIDTH, align: 'center' }, { title: 'PV/UV', align: 'center' }];
    this.columns1 = [
        { renderHeader: () => (''), width: WIDTH },
        { title: '总计' },
        ...dates.map(v => ({ title: v }))
    ];

    const tempC2 = [{ renderHeader: () => (''), width: WIDTH }, { title: 'PV' }, { title: 'UV' }];
    dates.forEach(() => {
        tempC2.push({ title: 'PV' });
        tempC2.push({ title: 'UV' });
    });
    this.columns2 = tempC2;

    const tempC3 = [{ title: 'Name', key: 'name', width: WIDTH, align: 'center' }];
    for (let i = 0, l = (dates.length * 2) + 2; i < l; i++) {
        tempC3.push({ title: '', render: (h, p) => p.row.values[i] });
    }
    this.columns = tempC3;
}
```
---
### css

- 这里主要隐藏tbody和thead，以及删除header的一些border样式
```css
    .ud-table-no-body tbody{
        display: none;
    }
    .ud-no-t-b.ivu-table-wrapper{
        border-top: 0 ;
    }
    .ud-no-b-b .ivu-table:before{
        background-color: #fff;
    }
    .ud-table-no-header thead{
        display: none ;
    }
```