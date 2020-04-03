---
title: http状态码
date: 2020-03-29 14:40:03
tags: http状态码
---

<div><image src="http://pic.netbian.com/uploads/allimg/180803/084010-15332568107994.jpg"></image></div>
<h4 style="font-weight:bold">一些常见的状态码有</h4>
```html
<span style="color:MediumSlateBlue">200</span>       //服务器请求成功
<span style="color:MediumSlateBlue">403</span>       //服务器理解请求客户端的请求，但是拒绝执行此请求
<span style="color:MediumSlateBlue">404</span>       //服务器请求的网页不存在
<span style="color:MediumSlateBlue">503</span>       //服务器不可用
```
<p>所有状态解释：</p>
<h4 style="font-weight:bold">1XX(临时响应)</h4>
<p>表示临时响应需要请求者继续执行操作的状态码</p>
<pre>
<span style="color:MediumSlateBlue">100</span>       //服务器收到请求的一部分，正在等待剩余部分
<span style="color:MediumSlateBlue">101</span>       //请求切换协议，服务器确认并切换
</pre>
<h4 style="font-weight:bold">2XX(成功)</h4>
<p>表示响应成功--status</p>
```html
<span style="color:MediumSlateBlue">200</span>       //OK    请求成功。一般用于GET与POST请求
<span style="color:MediumSlateBlue">201</span>       //Created    已创建。成功请求并创建了新的资源
<span style="color:MediumSlateBlue">202</span>       //Accepted    已接受。已经接受请求，但未处理完成
<span style="color:MediumSlateBlue">203</span>       //Non-Authoritative Information    非授权信息。请求成功。但返回的meta信息不在原始的服务器，而是一个副本
<span style="color:MediumSlateBlue">204</span>       //无内容。服务器成功处理，但未返回内容。在未更新网页的情况下，可确保浏览器继续显示当前文档
<span style="color:MediumSlateBlue">205</span>       //重置内容。服务器处理成功，用户终端（例如：浏览器）应重置文档视图。可通过此返回码清除浏览器的表单域
<span style="color:MediumSlateBlue">206</span>       //部分内容。服务器成功处理了部分GET请求
```
<h4 style="font-weight:bold">3XX(重定向)</h4>
<p>表示要完成请求，需要进一步操作。通常，这些状态代码用来重定向</p>
```html
<span style="color:MediumSlateBlue">300</span>       //多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端（例如：浏览器）选择
<span style="color:MediumSlateBlue">301</span>       //永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替
<span style="color:MediumSlateBlue">302</span>       //临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI
<span style="color:MediumSlateBlue">303</span>       // 查看其它地址。与301类似。使用GET和POST请求查看
<span style="color:MediumSlateBlue">304</span>       // 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源
<span style="color:MediumSlateBlue">305</span>       // 使用代理。所请求的资源必须通过代理访问
<span style="color:MediumSlateBlue">306</span>       //已经被废弃的HTTP状态码
<span style="color:MediumSlateBlue">307</span>       //临时重定向。与302类似。使用GET请求重定向
</pre>
<h4 style="font-weight:bold">4XX(请求错误)</h4>
<p>这些状态码表示请求可能出错，妨碍了服务器的处理。</p>
```html
<span style="color:MediumSlateBlue">400</span>       //客户端请求的语法错误，服务器无法理解
<span style="color:MediumSlateBlue">401</span>       //请求要求用户的身份认证
<span style="color:MediumSlateBlue">402</span>       //保留，将来使用
<span style="color:MediumSlateBlue">403</span>       //服务器理解请求客户端的请求，但是拒绝执行此请求
<span style="color:MediumSlateBlue">404</span>       //服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面
<span style="color:MediumSlateBlue">405</span>       //客户端请求中的方法被禁止
<span style="color:MediumSlateBlue">406</span>       //服务器无法根据客户端请求的内容特性完成请求
<span style="color:MediumSlateBlue">407</span>       //请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权
<span style="color:MediumSlateBlue">408</span>       //服务器等待客户端发送的请求时间过长，超时
<span style="color:MediumSlateBlue">409</span>       //服务器完成客户端的PUT请求是可能返回此代码，服务器处理请求时发生了冲突
<span style="color:MediumSlateBlue">410</span>       //客户端请求的资源已经不存在。410不同于404，如果资源以前有现在被永久删除了可使用410代码，网站设计人员可通过301代码指定资源的新位置
<span style="color:MediumSlateBlue">411</span>       //服务器无法处理客户端发送的不带Content-Length的请求信息
.....
```
<h4 style="font-weight:bold">5XX(服务器错误)</h4>
<p>这些状态码表示服务器在尝试处理请求时发生内部错误。这些错误可能是服务器本身的错误，而不是请求出错。</p>
```html
<span style="color:MediumSlateBlue">100</span>       // 服务器内部错误，无法完成请求
<span style="color:MediumSlateBlue">101</span>       //服务器不支持请求的功能，无法完成请求
<span style="color:MediumSlateBlue">102</span>       //作为网关或者代理工作的服务器尝试执行请求时，从远程服务器接收到了一个无效的响应
<span style="color:MediumSlateBlue">103</span>       //由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的Retry-After头信息中
<span style="color:MediumSlateBlue">104</span>       //充当网关或代理的服务器，未及时从远端服务器获取请求
<span style="color:MediumSlateBlue">105</span>       //服务器不支持请求的HTTP协议的版本，无法完成处理
```
<ul><li><h4 style="font-weight:bold">强，协商缓存</h4></li></ul>
<p>顺便记录一下强缓存和协商缓存</p>
缓存分为两种：强缓存和协商缓存，根据响应的header内容来决定。
<table>
<tr>
<th>    </th>
<th>获取资源形式</th>
<th>状态码</th>
<th>是否发送请求到服务器</th>
</tr>
<tr>
<th>强缓存</th>
<th>从缓存取</th>
<th>200</th>
<th>否，直接从缓存取</th>
</tr>
<tr>
<th>协商缓存</th>
<th>从缓存取</th>
<th>状304</th>
<th>	
是，通过服务器来告知缓存是否可用</th>
</tr>
</table>
<a href="https://591616.coding-pages.com/2020/03/29/http状态码/">本文链接(https://591616.coding-pages.com/2020/03/29/http状态码/)</a>
