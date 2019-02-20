# 与数组相关的操作

## 数组去重
```js	
方法一：利用hash表
Array.prototype.unique = function () {  
	var result = [],hash={};
	this.forEach(function (v) {
		if (!hash[v]) {
			hash[v]=true;
			result.push(v);
		}
	});
	return result;
}
方法二：利用set
var set =new Set([array]);
var tempArray=[];
set.forEach(function(v){
    tempArray.push(v)
})

得到数组[...set]
//更多set返回值与array转换->查mdn
```