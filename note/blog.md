
jsonp 同源策略 跨域处理方式 浏览器安全

## HTML
### HTML5
- 语义化 新标签
- 通信： web socket webRTC
- 存贮： indexDB
- 绘图： Canvas svg
- 性能： web workder

## css

1. 伪类与伪元素
伪类用于当已有元素处于的某个状态时，为其添加对应的样式，这个状态是根据用户行为而动态变化的
伪元素用于创建一些不在文档树中的元素，并为其添加样式
伪元素 ::before ::after ::first-letter ::first-line
2. css3新特性
 圆角 阴影 渐变 transitions(过渡) animations(动画) flex grid  transform 媒体查询 多列布局

3. flex
flex属性是flex-grow flex-shrink flex-basis的简写  默认值是0 1 auto  后两个属性可选

4. 不知宽高垂直居中
  -   flex
  -  absolute + transition



## Javascript
 - 如何串行发送请求
   这个问题在与 async await 在常规的高阶方法forEach  map 中是没有无效  但是在如下有效
  - for...of  + async/await  
  - reduce(返回promise) + async/await

- 并发发送请求（async-pool async ）
 promise.race 

- 如何优化一个首屏加载

- 高性能渲染十万条数据
https://cloud.tencent.com/developer/article/1533206

- 可选连语法
语法细节 https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Optional_chaining
如何搭配环境使用 https://juejin.cn/post/6844904002795077640

  

### ES6
- let const
- 魔板字符串
- 解构赋值
- 新的基本数据类型 symbol bigInt
- 新的迭代结构  map 和 set  weakMap  weakSet 
- 遍历迭代结构  for of
- proxy和reflect
- promise
- genetator
- async await
- class
- module
- 箭头函数
- math + number + string + array + object APIs

[参考](https://github.com/lukehoban/es6features#readme)






## 回复（整理那些没有完全掌握的东西

1. 发现自己对PureComponent 与React.memo理解还不够

- 前者比较包括props state , 后者只有props
-  我没有真正理解浅比较（非常严重）， 浅比较相当于之比较引用， 深比较是比较每一层的属性值
-  还有点不同 React.memo是可以通过第二个参数自定义比较对象

2. cloneElement没有完全理解
主要还是没怎么使用 以element 元素为样板克隆并返回新的 React 元素。返回元素的 props 是将新的 props 与原始元素的 props 浅层合并后的结果

使用场景 劫持children element 混入props 这样我突然想起lms里面的拖拽就是这么实现的

3. useImperativehandle 
又是一个盲点 很早的时候用过这个api  类组件获取子组件的实例用forwordRef  函数式组件就需要这个配合forwordRef使用

4. 高阶组件
这个掌握的太差了
https://juejin.cn/post/6940422320427106335#heading-44






- react vs vue
相同点  都是数据驱动
 react 有很多开创性的概念  因此 上手要难一些
 dom变化的检测不一样 vue是通过属性代理自动检测 react是手动用diff算法对比
 https://www.zhihu.com/question/301860721
 
- 如何code review 
https://jimmysong.io/eng-practices/




## 数据结构与算法




## 具体
1. JS实现大树运算 https://zhuanlan.zhihu.com/p/72179476
EEE754类型的值有一个特点，它在介于 -(2^53 -1) 到 2^53-1之间时是精确

2. 如何手动实现一个Promise.all
https://github.com/YvetteLau/Step-By-Step/issues/25


3 实现一个数组转树形结构的函数
https://stackoverflow.com/questions/18017869/build-tree-array-from-flat-array-in-javascript

4. JSONP 的工作原理是什么？
https://www.zhihu.com/question/19966531
http://www.thewashingtonhua.com/blog/2016/08/17/jsonp

5. 如何用js实现一个红绿灯

https://juejin.cn/post/6844903784838070280
https://github.com/haizlin/fe-interview/issues/1027

6. 如何实现一个Event(发布订阅模式)
https://juejin.cn/post/6844903587043082247
https://github.com/browserify/events
http://nodejs.cn/api/events.html#events_events


7. bind实现
```js
Function.prototype.bind = function (context) {
  const fn = this;
  // 没有考虑到传参以及被new调用情况
  return function () {
    return fn.call(context)
  }
}
```

8. 防抖和节流
```js
const debounce = (fn, wait = 1000) => {
  let timeID

  return function() {
    const context = this;

    if (timeID) {
      clearTimeout(timeID)
    }

    timeID = setTimeout(
      () => {
        fn.call(context, arguments)
      },
      wait
    )
  }
}

// =====================================
function throttle(fn, wait=1000) {
  let timeID

  return function() {
    const context = this;

    if (!timeID) {
      timeID = setTimeout(() => {
        fn.call(context, arguments)
        timeID = null;
      })
    }
    
  }
}

```

这里检测是否被new过可以用es6中 new.target属性

https://github.com/mqyqingfeng/Blog/issues/12
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new.target

8. 深拷贝
https://cloud.tencent.com/developer/article/1497418


## 质量
1.如何提高代码质量
- 执行编码规范
- lint检测
- code review
- 单元测试


# 后端
 1.DNS域名解析具体过程





## 工程化
### babel

[the-super-tiny-compiler ](https://github.com/jamiebuilds/the-super-tiny-compiler/blob/master/the-super-tiny-compiler.js)

## babel
- babel 相当于一个js的编译器 主要要个阶段  parse transform generate
- 大概流程如下  或许es6代码 => 通过@babel/parse解析成Ast(词法分析 语法分析) => 插件通过@babel/traverse 遍历Ast得到新的Ast => 通过@babel/generator把ast生成新的es5
- 核心包  @babel/core @babel/parse @babel/traverse 
[参考](https://github.com/willson-wang/Blog/issues/67) 这篇博客写的很细很深入
https://github.com/jamiebuilds/the-super-tiny-compiler/blob/master/the-super-tiny-compiler.js











