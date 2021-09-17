## 优化工具
- React devtool

### 优化原则
1 减少重渲染


## 优化方式

### 传统类组件
1 shouldComponentUpdate
2 React.PureComponent
3 缓存衍生数据（Reselect)
4 使用不可变数据结构(immer)
  shouldComponentUpdate => React.PureComponent/React.memo => 不可变数据结构(immutable/immer)
  明确是否渲染        浅比较   深比较(浪费资源)    不可变数据(空间换时间)
  https://juejin.cn/post/6846687604130185230#heading-5
5 代码切割
6 服务器端渲染(ssr)
7 worker处理密集计算
8 有状态组件上下文最小化

### React Hooks
- React.memo
- useCallback
- useMemo
- useEffect + 依赖
- useReducer  +  [dispatch 不变回调函数](https://react.docschina.org/docs/hooks-faq.html#how-to-avoid-passing-callbacks-down)


## 参考
- [Optimizing Performance](https://react.docschina.org/docs/optimizing-performance.html)
- [React Hooks性能优化](https://react.docschina.org/docs/hooks-faq.html#can-i-skip-an-effect-on-updates)


