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
- [基于浏览器的单线程调度算法](https://github.com/xxn520/react-fiber-architecture-cn)
- [完全理解React Fiber](http://www.ayqy.net/blog/dive-into-react-fiber/)
- [由浅入深快速掌握React Fiber](https://www.jianshu.com/p/37d7de212df1)
- [React Fiber 架构学习](https://zhuanlan.zhihu.com/p/44942360)

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

## react18

### createRoot 替换 render
  - [react 官网](https://github.com/reactwg/react-18/discussions/5)
  - [中文版](https://juejin.cn/post/6992435557456412709)
