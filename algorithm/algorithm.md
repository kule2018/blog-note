# 斐波拉契数列
> 利用生成器

f0 = 0; f1 = 1; fn = f(n-1) + f(n-2); n>=2
```js
function* fibonacci() {
    let [current, v] = [0, 1]
    console.log('斐波拉契数列(0-100): ');
    console.log(current);
    while (true) {
        [current, v] = [v, current + v]
        yield current
    }
}

for (const v of fibonacci()) {
    if(v > 100) break
    console.log(v);
}
```