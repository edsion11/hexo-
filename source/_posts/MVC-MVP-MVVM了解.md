---
title: 'MVC,MVP,MVVM了解'
date: 2020-03-31 12:44:52
tags:
  - MVC
  - MVP
  - MVVM
---

<h4 style="text-align:center">MVC</h4>
<h5>MVC的概念</h5>
<div>M是指业务模型，V是指业务界面，C是控制器</div>
<ul>
<li>M即model模型，数据层，负责数据的的处理和获取的数据接口</li>
<li>V即view视图层，是用户看到并且交互的界面</li>
<li>C即control控制层，是model和view进行数据交互的桥梁</li>
</ul>
它们之间的通信用一个图表示：
<img src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1585640477674&di=5fa58e41fb0e7545fa31ca8ba8d798b2&imgtype=0&src=http%3A%2F%2Faliyunzixunbucket.oss-cn-beijing.aliyuncs.com%2Fjpg%2Fcbe8c7a255f7bf8b2fdf90868a100850.jpg%3Fx-oss-process%3Dimage%2Fresize%2Cp_100%2Fauto-orient%2C1%2Fquality%2Cq_90%2Fformat%2Cjpg%2Fwatermark%2Cimage_eXVuY2VzaGk%3D%2Ct_100">
<div>Model主要负责数据层的接口，View是展示层(GUI)，对于web前端来说所有以html开头的文件都属于这一层，Controller控制层，理论上所有的通信都是单向的。类似于 一个三角形通信结构。所以MVC更适合后端开发，相关发展比较成熟。</div><br>
<div>好处：    1.耦合性低。    2.重用性高    3.拓展新好    4.可维护性高</div>
<div>MVC不适合前端开发：
<ul>
<li>1.前端的View已经具备了独立处理用户事件的能力，如果每个事件都流经Controller层，这层会变得十分臃肿</li>
<li>2.MVC中的View和Controller一般都是一一对应的，捆绑起来表示一个组件，视图层和控制层的紧密连接让Controller和View无法复用</li>
</ul>
</div>
<h4 style="text-align:center">MVP模式</h4>
<div>MVP(Model-View-Presenter)是MVC的改良版，由IBM的子公司提出</div>
<div>在MVC中View可以直接操控Model，而在MVP模式中，View只能通过presenter来操控Model，而presenter和View和Model都是双向通信</div><br>
<div>与MVC相比，MVP通过解耦View和Model，完全分离视图和模型，使职责划分更清晰</div><br>
<div>View不依赖Model，可以将View分离出来做组件，组件化生产，只需要一系列接口提供给上层操作</div>
<img src="https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1294241556,276820963&fm=26&gp=0.jpg">
<div style="text-align:center">上图就是MVP模式图</div>
<div>MVP也存在问题</div>
<ul>
<li>Presenter作为View和Model的桥梁，除了基本业务逻辑外，还有大量代码需要对View到Model和从Model到View进行“手动同步”，这样显得presenter很重，维护麻烦</li>
<li>同时由于没有数据绑定，如果Presenter对视图渲染的需求增多，一旦试图需求发生改变，Presenter也需要改动
</li></ul>
<h5 style="text-align:center">MVVM的出现</h5>
<div>MVVM提出了ViewModel模型(最早由微软提出)</div>
<div>关键点在于ViewModel和Model层实现了数据的双向绑定</div>
<img src="https://upload-images.jianshu.io/upload_images/4050018-ce27fe8c0d60e299.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp">
<div>MVVM首先是将View和Model的同步逻辑自动化了，对应于MVP模式的“手动同步”</div>
<div>之前presenter负责的View和Model同步不用再手动同步了，而是交给框架提供的数据绑定负责，只需要告诉View显示的数据对应于Model的哪个部分即可。在这之中通过ViewModel进行数据绑定，Model发生变化，ViewModel自动刷新，同时如果ViewModel改变，Model也自动刷新</div>
<h4>总结：</h4>
<div>
<ul>
<li>整体上看，MVVM比MVC和MVP精简了很多，不仅优化了业务和界面的依赖，还解决了数据频繁更新的问题。</li>
<li>MVVM中，View不知道Model的存在，ViewModel和Model也察觉不到View，这种低耦合模式，让开发更容易</li>
<li>MVVM更适合试图更多的前端项目进行工程化开发</li>
</ul>
</div>
