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