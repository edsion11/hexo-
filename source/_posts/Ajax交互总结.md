---
title: Ajax交互总结
date: 2020-03-30 14:43:18
tags: 
  - Ajax
  - JSONP
---
<h4 id="什么是Ajax和JSON，它们的优缺点">什么是Ajax和JSON，它们的优缺点</h4>
<ul>
<li>Ajax是全称是asynchronous JavaScript andXML，即异步JavaScript和xml，用于在Web页面中实现异步数据交互，实现页面局部刷新</li>
<li>优点：可以实现异步通信效果，页面局部刷新，带来更好的用户体验</li>
<li>JSON是一种轻量级的数据交换格式，看着像对象，本质是字符串</li>
<li>优点：轻量级、易于人的阅读和编写，便于js解析，支持复合数据类型</li>
</ul>
<h4 id="Ajax的交互流程有哪几步？">Ajax的交互流程有哪几步？</h4>
<ul>
<li>创建ajax对象</li>
<code>xhr = new XMLHttpRequest</code>
<li>规定请求地址</li>
<code>xhr.open(method,url,async)</code>
<li>等待服务器相应</li>
<code>xhr.onload</code>
<li>向服务器发送请求</li>
<code>xhr.send()</code>
</ul>
<p>下面是一个验证用户名的ajax例子</p>
```javascript
username.onblur = function(){
var usernameValue = username.value;
//将usernameValue提交给服务器，有服务器进行唯一性的校验
//1、创建对象 兼容处理
var xhr = null;
if(window.XMLHttpRequest) {
	xhr = new XMLHttpRequest();
} else {
	xhr = new ActiveXObject("Microsoft.XMLHTTP");
	}
	//2、准备发送
	xhr.open("get","./server/checkUsername.php?uname=" + usernameValue,true);
	//3、执行发送
	xhr.send(null);
	//制定回调函数
	xhr.onreadystatechange = function(){
	if(xhr.readyState == 4) {
	if(xhr.status == 200) {
		var result = xhr.responseText;
	var username_result = document.querySelector("#username_result");
	if(result == "ok") {
	username_result.innerText = "用户名可以使用";
} else {
		username_result.innerText = "用户名已经被注册";
		 }
	  }
     }
};
```
<h4 id="XMLHttpRequest对象在IE和Firefox中创建方式有没有不同？">XMLHttpRequest对象在IE和Firefox中创建方式有没有不同？</h4>
<span>
IE中通过new ActiveXObject()得到，Firefox中通过newXMLHttpRequest()得到.
使用jquery封装好的ajax，会避免这些问题
</span>

<h4 id="简述ajax的优缺点">简述ajax的优缺点</h4>
<span>
优点：
　　<li>无刷新更新数据（在不刷新整个页面的情况下维持与服务器通信）
　　<li>异步与服务器通信（使用异步的方式与服务器通信，不打断用户的操作）
　　<li>前端和后端负载均衡（将一些后端的工作交给前端，减少服务器与宽度的负担）
　　<li>界面和应用相分离（ajax将界面和应用分离也就是数据与呈现相分离）
　　<li>缺点：
　　<li>ajax不支持浏览器back按钮
　　<li>安全问题 Aajax暴露了与服务器交互的细节
　　<li>对搜索引擎的支持比较弱
　　<li>破坏了Back与History后退按钮的正常行为等浏览器机制
</span>
<h4 id="get与post的区别，什么时候使用post？">get与post的区别，什么时候使用post？</h4>
<p>get和post在HTTP中都代表着请求数据，其中get请求相对来说更简单、快速，效率高些</p>
<ul>
<li>get相对post安全性低</li>
<li>get有缓存，post没有</li>
<li>get体积小，post可以无限大</li>
<li>get的url参数可见，post不可见</li>
<li>get只接受ASCII字符的参数数据类型，post没有限制</li>
<li>get请求参数会保留历史记录，post中参数不会保留</li>
<li>get会被浏览器主动catch，post不会，需要手动设置</li>
<li>get在浏览器回退时无害，post会再次提交请求</li>
</ul>
<p>post一般用于修改服务器上的资源，对所发送的信息没有限制。比如</p>
<ul><li>无法使用缓存文件（更新服务器上的文件或数据库）</li>
<li>向服务器发送大量数据（POST 没有数据量限制）</li>
<li>发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠</li>
</ul>
<h4 id="XMLHttpRequest常用方法和属性">XMLHttpRequest常用方法和属性</h4>

open(get/post,url,是否异步)创建http请求

send()发送请求给服务器

setRequestHeader()设置头信息（使用post才会用到，get并不需要调用该方法）

常用的属性：

onreadystatechange 用于监听ajax的工作状态（readyState变化时会调用此方法）

readyState 用来存放XMLHttpRequest的状态

status 服务器返回的状态码

responseText 服务器返回的文本内容
<h4 id="readyState的几个状态">readyState的几个状态</h4>
0：请求未初始化（此时还没有调用open）

1：服务器连接已建立，已经发送请求开始监听

2：请求已接收，已经收到服务器返回的内容

3：请求处理中，解析服务器响应内容

4：请求已完成，且响应就绪
<h4 id="jquery ajax的实现">jquery ajax的实现</h4>
```javascript
$.ajax({
     url:发送请求的地址,
     data:数据的拼接,//发送到服务器的数据
     type:'get',//请求方式，默认get请求
     dataType:'json',//服务器返回的数据类型
     async:true,//是否异步，默认true
     cache:false,//设置为 false 将不会从浏览器缓存中加载请求信息
     success:function(){},//请求成功后的回调函数
     error: function(){}//请求失败时调用此函数
})
```
不足之处：

　　（1）针对MVC的编程,不符合现在前端MVVM的浪潮

　　（2）基于原生的XHR开发，XHR本身的架构不清晰，已经有了fetch的替代方案
<h4>同步和异步</h4>
同步：程序运行从上而下，浏览器必须把这个任务执行完毕，才能继续执行下一个任务

异步：程序运行从上而下，浏览器任务没有执行完，但是可以继续执行下一行代码
<h4 id="跨域">跨域</h4>
跨域的概念：协议、域名、端口都相同才同域，否则都是跨域

解决跨域问题：

1.使用JSONP（json+padding）把数据内填充起来

2.CORS方式（跨域资源共享），在后端上配置可跨域

3.服务器代理，通过服务器的文件能访问第三方资源
<h4>JSONP原理</h4>
ajax请求受同源策略影响，不允许进行跨域请求，而script标签src属性中的链接却可以访问跨域的js脚本，利用这个特性，服务端不再返回JSON格式的数据，而是返回一段调用某个函数的js代码，在src中进行了调用，这样实现了跨域。
<h4 id="Ajax和JSONP">Ajax和JSONP</h4>
ajax: { }

jsonp:fn( { } )

ajax的数据jsonp不能用，jsonp的数据ajax是可以用的

jsonp本质是通过URL的方式进行请求的，所以它是get方式请求，没有post