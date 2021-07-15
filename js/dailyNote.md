#### 2021=07-09

- 可选连语法
语法细节 https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Optional_chaining
如何搭配环境使用 https://juejin.cn/post/6844904002795077640

- git revert 
Revert some existing commits
删除某次commit  会产生新的提交记录， 不过确实很实用
revert 恢复会保持之前的提交记录并生成新的commit    reset 不会之前重置到制定的commit 没有任何记录

- 隐藏页面的方法
https://75.team/post/five-ways-to-hide-elements-in-css.html


### 2021-07-13
unit test

- jest 处理样式
https://jestjs.io/docs/configuration

- jest中测试被redux  connect 包裹的dump component
https://github.com/enzymejs/enzyme/issues/1002  我也好奇这个测试是否有意义
https://stackoverflow.com/questions/35131312/how-to-unit-test-react-redux-connected-components
http://www.recompile.in/2019/11/testing-redux-store-connected-react.html

- css.apply问题 这个问题根据调用栈直接指向React-Select 也就是这个第三方库有问题
对比了一下版本  发现版本差异不小  更新到最新版 居然解决了这个问题

unit test相关库
- [sinon](https://blog.kazaff.me/2016/11/11/%E8%AF%91--- Sinon%E5%85%A5%E9%97%A8%EF%BC%9A%E5%88%A9%E7%94%A8Mocks%EF%BC%8CSpies%E5%92%8CStubs%E5%AE%8C%E6%88%90javascript%E6%B5%8B%E8%AF%95/#Mocks)

- [redux-mock-store](https://github.com/reduxjs/redux-mock-store)

#### 工具
- Jest Runner

#### 参考
[[译] 测试 React & Redux 应用良心指南](https://juejin.cn/post/6844903569712234509)
[React单元测试策略及落地](https://insights.thoughtworks.cn/react-strategies-for-unit-testing/)



### 2021-07-14
学习了Solid.js

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

