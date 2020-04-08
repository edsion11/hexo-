---
title: Vue双向绑定
date: 2020-04-08 14:27:04
tags: Vue
---

<p>Vue的双向绑定是v-model指令</p>
<p>具体的实现原理是用了js中的<code>Object.defineProperty</code>方法来修改目标对象的属性</p>
<img src="https://vue-js.com/learn-vue/assets/img/3.0b99330d.jpg">
先看看Vue中源码中的解释:
<a href="https://github.com/vuejs/vue/blob/dev/src/core/observer/index.js">源码地址</a>
<h4>1.使Object数据变得可侦测 </h4>
<p>数据的每次读和写能够被我们看的见，即我们能够知道数据什么时候被读取了或数据什么时候被改写了，我们将其称为数据变的‘可观测’。</p>
<p>要将数据变的‘可观测’，我们就要借助前言中提到的<code>Object.defineProperty</code>方法了，在本文中，我们就使用这个方法使数据变得“可观测”。</p>

```javascript
var Obj = {
  val: 'hello',
}
Object.defineProperty(Obj, 'val', {
  get: function () {
    console.log('数据已读取')
  },
  set: function () {
    console.log('数据已修改')
  },
})
Obj.val
Obj.val = '123'
```

<p>上面是创建一个对象Obj，然后读取和赋值，下面是输出结果</p>
```javascript
数据已读取
数据已修改
[Done] exited with code=0 in 0.118 seconds
```
<p>上面是Object.defineProperty方法对数据进行观测拦截，每当该属性进行读或写操作的时候就会触发<code>get()</code>和<code>set()</code>,这样的方法在原来html页面进行简单的双向绑定，大型项目会很复杂，Vue框架的双向绑定引入观测模式，封装在index.js中，就是Vue的双向绑定。</p>
```javascript
Observer类会通过递归的方式把一个对象的所有属性都转化成可观测对象
export class Observer {
  constructor (value) {
    this.value = value
    // 给value新增一个__ob__属性，值为该value的Observer实例
    // 相当于为value打上标记，表示它已经被转化成响应式了，避免重复操作
    def(value,'__ob__',this)
    if (Array.isArray(value)) {
      // 当value为数组时的逻辑
      // ...
    } else {
      this.walk(value)
    }
  }
   walk (obj: Object) {
    const keys = Object.keys(obj)
    for (let i = 0; i < keys.length; i++) {
      defineReactive(obj, keys[i])
    }
  }
}
* 使一个对象转化成可观测对象
 * @param { Object } obj 对象
 * @param { String } key 对象的key
 * @param { Any } val 对象的某个key的值
function defineReactive (obj,key,val) {
  // 如果只传了obj和key，那么val = obj[key]
  if (arguments.length === 2) {
    val = obj[key]
  }
  if(typeof val === 'object'){
      new Observer(val)
  }
  Object.defineProperty(obj, key, {
    enumerable: true,
    configurable: true,
    get(){
      console.log(`${key}属性被读取了`);
      return val;
    },
    set(newVal){
      if(val === newVal){
          return
      }
      console.log(`${key}属性被修改了`);
      val = newVal;
    }
  })
}
````

<p>上面是数据可观测的过程，上面的代码中我们定义了<code>observer</code>类，它用来将一个正常的<code>object</code>转换成可观测的<code>object</code>。
并且给value新增一个<code>__ob__</code>属性，值为该value的<code>Observer</code>实例。这个操作相当于为<code>value</code>打上标记，表示它已经被转化成响应式了，避免重复操作
</p>
<p>
然后判断数据的类型，只有<code>object</code>类型的数据才会调用walk将每一个属性转换成<code>getter/setter</code>的形式来侦测变化。 最后，在<code>defineReactive</code>中当传入的属性值还是一个object时使用<code>new observer（val）</code>来递归子属性，这样我们就可以把obj中的所有属性（包括子属性）都转换成<code>getter/seter</code>的形式来侦测变化。 也就是说，只要我们将一个<code>object</code>传到<code>observer</code>中，那么这个<code>object</code>就会变成可观测的、响应式的<code>object</code>。
</p>
<h4>2.依赖收集</h4>
<p>之后还有依赖收集，我们在上面是实现了数据的可观测性，数据变换之后，还得通知对应的视图层变换，在整个视图层之中知道需要通知的部分，就是“依赖收集”。如果数据变了，就把数据的依赖数组通知变换。</p>
<p>总结一句话就是:<code>getter()</code>收集依赖 , <code>setter()</code>通知依赖更新</p>
