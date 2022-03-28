## redux常用第三方工具
- redux-persist  持久化
- redux-orm 处理数据相互之间关联性高
- reselect 处理衍生数据
- normalizr 处理嵌套和相关联的数据结构
- Redux Undo  撤销
- redux-thunk

## redux 源码理解
- compose实现（尼玛 最近居然被问到了
  [参考](https://segmentfault.com/a/1190000015801987)
- 


## 理解redux中间件
-  中间件干什么的
>  它其实是在action发起到到达reducer之前调用store的方法做你想做的事情

-  中间件如何实现的
```javaqscript
export default function applyMiddleware(...middlewares) { return (next)  => 

        (reducer, initialState) => { var store = next(reducer, initialState); var dispatch = store.dispatch; var chain = []; var middlewareAPI = {
                getState: store.getState,
                dispatch: (action) => dispatch(action)
              };

              chain = middlewares.map(middleware =>
                            middleware(middlewareAPI));

              dispatch = compose(...chain, store.dispatch); return {
                ...store,
                dispatch
              };
           };
}
```

- [参考](http://cn.redux.js.org//docs/advanced/Middleware.html)


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



### redux 竞品 recoil xstate redux mobx zustand 对比
1. 是否支持处理副作用
2. 是否支持异步
3. 是否支持基于缓存计算衍生值
4. 是否支持ts

### zustand
- 感觉更适合小项目
- 没有action这样的样板代码


## mobx