---
title: javaScript(一)
date: 2020-03-29 16:56:58
tags:
---
<ul><li><h4>把多个JavaScript函数绑定到onload时间处理函数上</h4></li></ul>
<p>假设我有两个函数：firstFunction()和secondFunction()。如果我想让他们俩都在页面加载时得到执行，我该怎么办？如果把他们逐一绑定到onload事件上，他们当中将只有最后那个被执行：</p>
<pre>
<code>window.onload = firstFunction;</code>
<code>window.onload = scondFunction;</code>
</pre>
secondFunction将取代firstFunction。所以得出结论：每个事件处理函数只能绑定一条指令
<pre><code>
<span style="color:orange">function</span> <span style="color:purple">addLoadEvent</span><span>(func){
  var oldload = window.onload;
  if(typeof window.onload != 'function'){
    window.onload = fnc;
  }else{
    window.onload = function(){
      oldonload();
      func();
    }
  }
}</span>
</code></pre>
这相当于把那些将在页面加载完毕时执行的函数创建为一个队列。如果想把刚才那两个函数添加到这个队列里去，只需要写如下代码：
<pre>
addLoadEvent(firstFunction)
addLoadEvent(secondFunction)
</pre>
---未完待续