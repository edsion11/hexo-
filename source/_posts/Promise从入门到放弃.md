---
title: Promise从入门到放弃
date: 2020-04-28 23:34:41
tags:
  - Promise
  - async/await
  - 宏队列
  - 微队列
---

##### Promise 从入门到放弃

#### javascript 异步操作执行历史

JavaScript 语言的执行环境是“单线程”， 所谓单线程，就是一次只能完成一件任务， 如果有多个任务就需要排队，一个完成了，继续下一个，这种方式在实现来说是非常简单的，但是如果一个任务耗时很长，那么后面的任务就需要排队等着，会拖延整个程序的执行。 常见的浏览器无响应（假死）就是因为某一段 JavaScript 代码长时间运行（比如死循环），导致整个页面卡死，其他任务无法执行。

##### javascript 异步操作的类型

- 回调函数
- 事件监听
- 发布/订阅
- promise
- generator（ES6）
- async/await （ES7）

###### 回调函数

```javascript
function f1(func) {
  setTimeout(() => {
    console.log('我是f1')
    for (let i = 1; i < 50000; i++) {
      console.log('我是f1的' + i)
    }
    func()
  }, 500)
}
function f2() {
  alert('我是f2')
}

function f3() {
  alert('我是f3')
}
f1(f2) //这里f1(),f2()不会阻塞f3()的运行
f3()
```

这里主要利用`setTimeout()`函数来进行异步操作，f3`()`的执行不会受到`f1()`影响。主要是因为`setTimeout()`是异步函数。
