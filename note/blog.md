
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


## react技术栈
#### 虚拟dom

#### 组件
1. 状态
state
props

2. 通信

3. 生命周期

4. 更新机制
- props更新
- state更新 (setState forceUpdate useState)

5. 事件机制

### react
1. 高阶组件（HOC）
属性代理和逻辑复用
https://juejin.cn/post/6940422320427106335
https://juejin.cn/post/6844903782355042312#heading-28


2. 生命周期

挂载 constructor componentDidMount render
更新 shouldComponentUpdate componentDidUpdate render
卸载 componentWillUnmount

3. setState到底是异步还是同步

setState只在合成事件和钩子函数中是“异步”的，在原生事件和setTimeout 中都是同步的(待验证)
setState本身并不是异步，只是因为react的性能优化机制体现为异步。在react的生命周期函数或者作用域下为异步，在原生的环境（setTimeout，原生事件）下为同步。
https://juejin.cn/post/6850418109636050958


4. Context理解(TODO)

  - 使用场景： 主要是涉及跨组件传递高频使用数据  比如国际化语言 以及皮肤数据等
  - 语法： React.createContext()  无论是类组件还是函数式组件都需要提供context  所以比较好的实践是把context提取到单独的全局context文件 react-redux也是这么做的
  - 缺点：降低组件的复用性 以及可能导致一些无效渲染
  - 注意事项：提供给provider的值想state一样会引起渲染  所以如果值没变需要需要保持相同的引用 这意味着提供给value的值最好是不可变结构或者用useMemo处理
  - codesandbox demo: https://codesandbox.io/s/context-q93n0?file=/src/App.js


5. portal理解

  portal与render实现的功能一样 render一样可以把dom节点渲染后dom结构外
  视觉上portal科被放置到dom树的任何地方  但是行为上和作为react的子节点一致（比如context 事件冒泡这些特性没有改变  
  - [portal](https://zh-hans.reactjs.org/docs/portals.html)
  - [demo](https://codesandbox.io/s/create-portal-vs-render-forked-yzxph?file=/index.js)


6. 对react事件的理解
  react事件借鉴事件委托机制，react中事件最后都是被委托 绑定到document
  react这么做的原因：浏览器的兼容性处理 实现跨平台事件机制
  https://zhuanlan.zhihu.com/p/165089379
  https://www.jianshu.com/p/41776f2f4d8b
  https://juejin.cn/post/6844904066397503502

8. React Fiber理解
基于浏览器的单线程调度算法
https://github.com/xxn520/react-fiber-architecture-cn

9. hooks 
 - hooks 理解
 处理逻辑复用问题以及以及只能在组件最外层  而且不能在条件语句里面

  -  useEffect如何实现各个周期
  - useCallback useMemo区别

如何自定义hooks 比如自顶一个一个useRequest
```js
const useRequest = (url) => {
  const [data, setData] = useState(null)

  useEffect(
    async() => {
      const res = await fetch(url);
    },
    []
  )

  return data;
}
```

如何实现useReducer以及useState 
实现一些常见的自定hooks

10. 跨组件数据传递
  - context
  - useReducer

11. 阻止当前组件的渲染
 - shouldComponent
 - React.memo

 12. 如何设计一个react组件以及有哪些原则
    - 单一功能职责
    - 最小state props
    - 组合优于继承
    -  其他程序设计原则

### redux
1. redux-react中provider原理
  context
1. 理解redux中间件(store.dispatch如下改造)

4. redux如何处理异步（TODO）
 redux-thunk、redux-saga 

5. redux与mobx的区别?
redux将数据保存在单一的store中，mobx将数据保存在分散的多个store中
redux使用plain object保存数据，需要手动处理变化后的操作；mobx适用observable保存数据，数据变化后自动处理响应的操作
redux使用不可变状态，这意味着状态是只读的，不能直接去修改它，而是应该返回一个新的状态，同时使用纯函数；mobx中的状态是可变的，可以直接对其进行修改
mobx相对来说比较简单，在其中有很多的抽象，mobx更多的使用面向对象的编程思维；redux会比较复杂，因为其中的函数式编程思想掌握起来不是那么容易，同时需要借助一系列的中间件来处理异步和副作用
mobx中有更多的抽象和封装，调试会比较困难，同时结果也难以预测；而redux提供能够进行时间回溯的开发工具，同时其纯函数以及更少的抽象，让调试变得更加的容易


```js
let next = store.dispatch;
store.dispatch = function dispatchAndLog(action) {
  console.log('dispatching', action);
  next(action);
  console.log('next state', store.getState());
}
```
http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_two_async_operations.html


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



### react 优化
1 不可变数据结构 不可变数据结构优化的原理  如何实现不可变数据结构
2 服务器端渲染(ssr)
3 PureComponent componentShouldUpdate 代码分割  react.memo

shouldComponentUpdate => React.PureComponent/React.memo => 不可变数据结构(immutable/immer)
明确是否渲染        浅比较   深比较(浪费资源)    不可变数据(空间换时间)
https://juejin.cn/post/6846687604130185230#heading-5


## HTTP
1. http与https区别
https://www.zhihu.com/question/19577317

2. HTTPS的加密传输原理 **NICE**

 - https://zhuanlan.zhihu.com/p/43789231

> 首先需要理解对称加密与非对称加密 
  以及对称加密为什么不安全(如何保证秘钥被安全传输到服务器)
  以及非对称加密如何通过两对秘钥解决问题  但是要多次加密传输 耗费资源 性能
  刚好用非对称加密传输对称加密需要的秘钥就可以解决了  但是还是有一个问题 传输的秘钥被中间人掉包依然有问题（问题回归到如何保证收到的公钥的网站自己的）
  这就需要数字证书 那数字证书怎么防止被篡改呢  这就需要数字签名

3. http2理解

  二进制编码 多路复用 服务器端推送 发送请求优先级 请求头部压缩
  https://www.zhihu.com/question/34074946
  https://developers.google.com/web/fundamentals/performance/http2?hl=zh-cn

4. tcp 和udp区别
- TCP 是面向连接的协议 。 UDP 是无连接的协议
- TCP需要建立连接， UDP不需要
	         UDP	               TCP
是否连接	无连接	面向连接
是否可靠	不可靠传输，不使用流量控制和拥塞控制	可靠传输，使用流量控制和拥塞控制
连接对象个数	支持一对一，一对多，多对一和多对多交互通信	只能是一对一通信
传输方式	面向报文	面向字节流
首部开销	首部开销小，仅8字节	首部最小20字节，最大60字节
适用场景	适用于实时应用（IP电话、视频会议、直播等）	适用于要求可靠传输的应用，例如文件传输

5. http缓存

第一次请求后会把响应数据和缓存规则存入缓存系统，第二次及以后的请求先进入缓存系统 根据缓存规则查看是否支持缓存 
https://juejin.cn/post/6844903801778864136

## 其他  
worker处理密集计算

浏览器缓存
强缓存
expires 设置过期时间 缺点是服务时间可能和客服端时间不一致
cache-control 设置过期时间长度（http1.1) cache-control 优先级比expires高

弱缓存
last-modified/if-modified-since 
etag/if-none-match

四种缓存的优先级：cache-control > expires > etag > last-modified

- react vs vue
相同点  都是数据驱动
 react 有很多开创性的概念  因此 上手要难一些
 dom变化的检测不一样 vue是通过属性代理自动检测 react是手动用diff算法对比
 https://www.zhihu.com/question/301860721
 
- 如何code review 
https://jimmysong.io/eng-practices/


## 设计模式

### 创建型
- 单例
```js
class SingleInstance {
  static getSingleInstance () {
    if (!SingleInstance.instance) {
      SingleInstance.instance = new SingleInstance()
    }

    return SingleInstance.instance;
  }
}

- 工厂模式
- 原型模式


### 结构型

- 代理模式

- 装饰器模式
  动态的为函数或者类添加功能 而不修改原来的功能
  https://codesandbox.io/s/decorator-o02s1

- 适配器模式

- 组合模式
```


### 行为型
- 观察者模式
```js
class Subject {
  constructor() {
    this.observers = []; // 观察者列表
  }

  add(observer) {
    this.observers.push(observer);
  }

  remove(observer) {
    let index = this.observers.findIndex(item => item === observer);
    index > -1 && this.observers.splice(index, 1);
  }

  notidy() {
    for (let observer of this.observers) {
      observer.update();
    }
  }
}

class Observer {
  constructor(name) {
    this.name = name;
  }

  update() {
    console.log(`目标者通知我更新了，我是：${this.name}`);
  }
}


let obs1 = new Observer('前端开发者');
let obs2 = new Observer('后端开发者');

// 向目标者添加观察者
subject.add(obs1);
subject.add(obs2);

// 目标者通知更新
subject.notify()
```

- 发布订阅模式
```js
// 事件中心
let pubSub = {
  list: {},
  subscribe: function (key, fn) {   // 订阅
    if (!this.list[key]) {
      this.list[key] = [];
    }
    this.list[key].push(fn);
  },
  publish: function(key, ...arg) {  // 发布
    for(let fn of this.list[key]) {
      fn.call(this, ...arg);
    }
  },
  unSubscribe: function (key, fn) {     // 取消订阅
    let fnList = this.list[key];
    if (!fnList) return false;

    if (!fn) {
      // 不传入指定取消的订阅方法，则清空所有key下的订阅
      fnList && (fnList.length = 0);
    } else {
      fnList.forEach((item, index) => {
        if (item === fn) {
          fnList.splice(index, 1);
        }
      })
    }
  }
}

// 订阅
pubSub.subscribe('onwork', time => {
  console.log(`上班了：${time}`);
})
pubSub.subscribe('offwork', time => {
  console.log(`下班了：${time}`);
})
pubSub.subscribe('launch', time => {
  console.log(`吃饭了：${time}`);
})

// 发布
pubSub.publish('offwork', '18:00:00'); 
pubSub.publish('launch', '12:00:00');

// 取消订阅
pubSub.unSubscribe('onwork');
// https://segmentfault.com/a/1190000019722065
```

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


## web安全
### CSRF
CSRF 攻击之所以能够成功，是因为黑客可以完全伪造用户的请求，该请求中所有的用户验证信息都是存在于cookie中，因此黑客可以在不知道这些验证信息的情况下直接利用用户自己的cookie 来通过安全验证。要抵御 CSRF，关键在于在请求中放入黑客所不能伪造的信息，并且该信息不存在于 cookie 之中
- HTTP头中带上token验证的方案来防御CSFR

## 质量
1.如何提高代码质量
- 执行编码规范
- lint检测
- code review
- 单元测试


## tencent interview
- react生命周期
- 高阶组件 
- ref 自定义组件如何处理Ref(forwordref)
- Portals
- 箭头函数与普通函数区别(this)
- react实践绑定在啥时候
- useEffect useMemo useCallback理解
- https如何实现数据安全传输  具体数据传输过程
  说了主要是通过数字证书  数据加密  完整性校验保证安全
  问了下能否说下数据加密的具体过程
- http缓存
   
- redux数据流 redux用过的中间件  Provider的理解
  数据流  说了下 action  reducer  store 各自的职责和数据流的处理
  使用过redux-ation redux-promise redux-persist reselector
  是否自己写过中间件  以前学的时候写过  现在忘记了
  关于中间件（http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_two_async_operations.html）
  Proviver理解  放在react app 跟组件下面 用于与view层单项数据流绑定  主要就是封装了store的几个api  比如getState(不是很记得)
- 对安全了解么  说下前端安全（xss CSRF)及防御 CSRF原理
   说了下xss 以及通过字符串转义等方式对特殊字符处理
   说了下csrf以及通过token方式防御（但是他问了token原理 没回答出来）
- 项目中遇到过哪些比如复杂的问题及如何处理
   提到了组件化思想处理多个手势  以及采用适配器模式 分层分模块的思维解决多协议在数据结构的差异  但是其实这里面漏掉了我认为项目组最大的亮点 就是我们处理多套协议数据思路（所有的redux数据不再是按照后端给数据结构数据  而是根据前端定义的不同的表去存贮）
- node和php熟悉么
- 后端接触多不 linux和nginx熟悉不
- 最后一个大题
  实现一个多图上传功能，假设我现在有n张图片，浏览器同时最多支持三个连接，如何实现（实现一个请求队列，队列中是三个发送出去还未响应的请求，根据响应更新队列 使用promise实现异步串行）

- useMemo useCallback理解
- hooks为什么不能放在条件表达式里面
- onClick事件和addlistenEvent区别
- react事件系统
- 简单请求和复杂请求 简单请求为什么不需要预检请求（没回答出来）
- http2的特性 头部压缩具体(这个说了只知道用了某种压缩算法然后二进制编码传输)
- 跨域方案 jsop cors jsop原理   script 和img 跨域区别（这个没回答处理）
- node的掌握么
- 对内存回收的理解
- object和map区别 weakmap什么时候回收（没回答出来）
- 最近看什么书（贫穷的本质 和一些股票的书
- 为什么看这本书  是别人推荐还是自己找的
- 一般怎么学习（看别人源码和别人沟通 然后自己写项目实践 
- 最近有学什么新技术么  （slvete  go)

  















# 后端
 1.DNS域名解析具体过程



# 新前端框架
## Solid.js
  
createSignal === useState
createEffect == useEffect
createMemo  === useMemo

jsx
Control Flow / Show
<Show
      when={loggedIn()}
      fallback={<button onClick={toggle}>Log in</button>}
    >
      <button onClick={toggle}>Log out</button>
    </Show>
    react直接用原生三元表达式

Control Flow / For
```jsx
<For each={cats()}>{(cat, i) =>
  <li>
    <a target="_blank" href={`https://www.youtube.com/watch?v=${cat.id}`}>
      {i() + 1}: {cat.name}
    </a>
  </li>
}</For>
```
这和svelte语法就差不多了

Control Flow / Index
```jsx
<Index each={cats()}>{(cat, i) =>
    <li>
      <a target="_blank" href={`https://www.youtube.com/watch?v=${cat().id}`}>
        {i + 1}: {cat().name}
      </a>
    </li>
  }</Index>
  ```
  解决key问题


Control Flow / Switch 
> 超过两个分支的条件渲染  类似原生的switch ... case
```jsx
<Switch fallback={<p>{x()} is between 5 and 10</p>}>
  <Match when={x() > 10}>
    <p>{x()} is greater than 10</p>
  </Match>
  <Match when={5 > x()}>
    <p>{x()} is less than 5</p>
  </Match>
</Switch>
```

Control Flow / Dynamic
```jsx
<Dynamic component={options[selected()]} />
```
这个不太理解使用场景 就是mapping render

Control Flow / Portal
> 和React.createPortal差不多

Control Flow / Dynamic

3. LifeCycles (ssr不支持)
 onMount
 createEffect
 onCleanup

4. Bindings / Events
和react 一样的 on 开头的事件命名  然后都是自动委托绑定到document上

5. Bindings / Style
和react差不多  区别在于属性名不需要是驼峰方式命名 原生css属性名是什么就写什么 

6. Bindings / ClassList
 class className都支持  还有一个二选一的时候classList
 ```js
 <div classList={{ active: isActive() }} />
 ```

7. Bindings / Refs Forwarding Refs
 和react差不多 同时提供了回调函数形式

8. Bindings / Spreads
这东西其实react也是有的 只是没有单独提出来说

9. Bindings / Directives 
  自定义指令  类似与vue里头吧 暂时不深入

10. Bindings / Defaults Props  Splitting Props
这个有点意思有mergeProps来处理 相当于使用原生Object.assign

11. Props / Children
 处理children这部分还是有些不一样
12. Stores / Nested Reactivity Create Stores
精准更新  这个确实叼（得益于proxies

13. Stores / Mutation
这个提供不可变数据结构  和immer.js差不多 提供了一个produce接口 主要是方便提供回放  时间旅行等功能

14. Stores / Context
一样哈 提供了 不依赖props 垮组件传递数据

15. Reactivity / Batching Updates
提供batch 批量更新 相当于合并的action 减少渲染 忘记redux 怎么处理了

16. Reactivity / Untrack
提供了不跟踪响应系统的api

17. Reactivity / On
类似于Effect 里面的第一个参数依赖数组  只有依赖更新 才跟踪对应状态

18. Async /Lazy
代码分割

19. Async / Resources
这个有点意思 react官方没有  但是就等同于第三方实现的useRequest


20. Async / SUspense Suspense List
和react差不多 渲染处理





### 优势
1. 精准更新 没有多余的渲染
https://www.solidjs.com/tutorial/stores_nested_reactivity



## 感想
突然理解到面试面大家的心里预差  如果你回答超过他的预期  印象就越好

## 第二遍 
这东西是响应式编程  所以和这种通过比对然后渲染更新有本质的区别
createSignal 并不会导致整个组件重新渲染  只是改变值
createEffect 只是订阅数据  监听到变化的值


recoil xstate redux mobx  context 对比
0. 是否支持处理副作用
1. 是否支持异步
2. 是否支持基于缓存计算衍生值
3. 是否支持ts


## 工程化
### babel

[the-super-tiny-compiler ](https://github.com/jamiebuilds/the-super-tiny-compiler/blob/master/the-super-tiny-compiler.js)

## babel
- babel 相当于一个js的编译器 主要要个阶段  parse transform generate
- 大概流程如下  或许es6代码 => 通过@babel/parse解析成Ast(词法分析 语法分析) => 插件通过@babel/traverse 遍历Ast得到新的Ast => 通过@babel/generator把ast生成新的es5
- 核心包  @babel/core @babel/parse @babel/traverse 
[参考](https://github.com/willson-wang/Blog/issues/67) 这篇博客写的很细很深入
https://github.com/jamiebuilds/the-super-tiny-compiler/blob/master/the-super-tiny-compiler.js












