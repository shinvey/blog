# Let's take a look at debounce function

```js
function debounce(fn, wait) {
    let timeout;
    // 给外部返回一个debounce包装的wrapper函数，接收任何参数
    return function wrapper(...args) {
        // 使用箭头函数保持函数的this上下文指向wrapper
        let callLater = () => {
            timeout = null; // 清除timeout引用便于GC内存回收
            fn.apply(this, args);
        }

        // 比如绑定了scroll事件，进行高频率调用，这里会清除之前的timeout
        clearTimeout(timeout);

        // 始终会有一个timeout再wait毫秒之后执行
        timeout = setTimeout(callLater, wait);
    }
}
var myEfficientFn = debounce(function() {
    // All the taxing stuff you do
    console.log('scroll event was debounced');
}, 500);

window.addEventListener('scroll', myEfficientFn);
```