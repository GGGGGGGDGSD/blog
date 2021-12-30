## vue
1. 组件通信
父子组件通信: props; $parent / $children; provide / inject ; ref ; $attrs / $listeners
兄弟组件通信: eventBus ; vuex
跨级通信: eventBus；Vuex；provide / inject 、$attrs / $listeners
https://segmentfault.com/a/1190000020053344

https://juejin.cn/post/6844903918753808398#heading-30

vue react 对比
功能模块                      react                        vue

表单状态管理                受控表单                  双向绑定
更新机制                   setState useState       响应式系统
响应式数据相关操作          useMemo useEffect       computed watch
HTML表单模板               jsx                      类angular指令模板
事件机制                  委托到挂载节点 合成事件
跨组件传递                 context                    Provide/Inject
逻辑复用                   高阶组件/hooks             setup   


## 深入响应式原理
- Object.defineProperty
- proxy
- 数组 修改数组原型做到监听
