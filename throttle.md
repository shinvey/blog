# A simple example of throttle function

```js
function throttle(fn, wait) {
    let inTrottle; // 默认打开阀门
    // 给外部返回一个throttle包装的wrapper函数，接收任何参数
    return function wrapper(...args) {
        if (!inTrottle) { // 阀门被打开
            fn.apply(this, args);
            inTrottle = true; // 关闭阀门
            setTimeout(() => inTrottle = false, wait); // 等待wait毫秒后开一次阀
        }
    }
}

window.addEventListener('scroll', throttle(function() {
    console.log('scroll event was out of throttle');
}, 1000));
```