---
title: ES6语法总结（一）
date: 2020-04-02 23:18:14
tags: 
  - ES6
  - let
  - const
---
<h4>let 和 const</h4>
<p>在原来的ES5时，定义变量，函数用的var会造成变量提升，于是ES6新增了<code>let</code>和<code>const</code>语法。接下来用代码说明</p>
```javascript
var a=[]
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6]()
var b = [];
for (let j = 0; j < 10 ;j++){
  b[j] = function () {
    console.log(j)
  }
}
b[6]()
//输出：
10
6
```
上下仅有的不同是for循环里面的<code> i </code>，<code> j </code>定义方式不同，上面定义的<code> i </code>为全局变量，for循环结束，<code> i </code>为10。而下面定义的<code> j </code>为局部变量，只在for（）｛｝的作用域内有效，于是形成了上面的结果。
<p>另外for循环的的设置循环变量括号内部是父作用域，而循环体则是子作用域。---来自阮一峰老师的博客介绍</p>
<code>var</code>的变量存在变量提升，什么意思呢，就是<code>var</code>定义的变量，在js运行时，会在运行开始的时候执行一条语句<code> var a </code>此时<code>a</code>为<code>undefined</code>，如果在定义<code>a</code>变量之前调用<code>a</code>变量,会显示<code>undefined</code>。而现在ES6为了减少这种情况，同时规范代码，新提出了<code>let</code>指令，let定义的变量，只有在let的块作用域内有效，出了作用域调用就会报错<code>// 报错ReferenceError</code><br>
<h4>暂时性死区</h4>
ES6 明确规定，如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。即在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）。有了这个，<code>typeof</code>就会更加安全，如果let定义之前typeof，会报错，而如果没有定义，则会输出undefined。<br>
还有一点：<code> let </code>不允许重复定义，不能同时定义相同的变量两次。
<h4>块作用域</h4>
<p>在ES5中只有全局作用域和局部作用域，带来了很多不合理的场景，所以如今ES6提出了块作用域，强调规范</p>
第一种场景，内层变量可能会覆盖外层变量。
第二种场景，用来计数的循环变量泄露为全局变量。(上面开头例子)
详见阮一峰老师的博客<a href="https://es6.ruanyifeng.com/#docs/let">阮一峰-let和const</a>
<h4>关于函数声明</h4>
<p>ES5中规定：函数只能在顶层作用域或者函数作用域中声明，不能在块级作用域申明。但是浏览器中还是支持在块级作用域中申明函数，不会报错。</p>
<p>而ES6引入了块级作用域，规定块级作用域外不可引用作用域内的函数</p>
```javascript
function fnc() { 
   console.log('I am outside!');
   }
(function () {
  if (0) {
    function f() { console.log('I am inside!'); }
  }

  f();
}());
```
上面的代码在ES5中会输出<code>I am inside!</code>，因为类似于<code>var</code>变量，函数会var声明提前，将if作用域内的<code>function</code>会提前至if之前，即<code> var f = undefined</code>于是在ES6中回报错。
```javascript
  test.js:10
  f();
  ^
TypeError: f is not a function
```
原因是ES6 在附录 B里面规定，浏览器的实现可以不遵守上面的规定，有自己的行为方式。
<ul>
<li>允许在块级作用域内声明函数。</li>
<li>函数声明类似于var，即会提升到全局作用域或函数作用域的头部。</li>
<li>同时，函数声明还会提升到所在的块级作用域的头部。</li>
</ul>
<h4>const命令</h4>
<p><code>const</code>会声明一个只读的变量，不能更改，也不能再定义并且定义的同时要立即赋值。同时const也是存在暂时性死区和块级作用域。与之前let类似</p>
<p>const只是定义数据所在的内存地址不能变动，而不是数据不能改动，即如果const定义一个数组或者对象，数组的push()，push()方法依然有效，对象设置属性也正常，但是对const定义的数组或者对象等再次赋值，负责会报错。如果永久冻结，不能变动，有一个冻结方法是<code>Object.freeze</code></p>
<p>如果有如下的定义：</p>
```javascript
const foo = Object.freeze({});
foo.prop = 123;
```
<p>正常模式会无效，而严格模式会报错（具体没有尝试，还没有具体碰到两种模式，只是了解）</p>
<h4>ES6申明变量6种方法</h4>
<ul>
  <li><code>var</code></li>
  <li><code>function</code></li>
  <li><code>let</code></li>
  <li><code>const</code></li>
  <li><code>import</code></li><a href="#">具体介绍</a>
  <li><code>class</code></li><a href="#">具体介绍</a>
</ul>
<h4>globalThis对象</h4>
<p>ES6还引入了globalThis对象，用来表示顶层对象，比如浏览器的顶层对象是<code>window</code>，WebWorker的顶层对象是<code>self</code>，Node里面是<code>global</code></p>
<span style="float:right">本次博客主要参考自阮一峰的ECMAScript6入门(一)</span>

























