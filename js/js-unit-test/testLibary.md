# Base

### 查询分类
  get用于查询 query用于断言  find用于异步

### [事件交互](https://testing-library.com/docs/user-event/utility)

   - 推荐使用@testing-library/user-event 而不是 fire-event, user-event还额外支持[这些更细的交互事件](https://github.com/testing-library/user-event/blob/main/src/setup/api.ts)
    ```js
      click,
      dblClick,
      tripleClick,
      hover,
      unhover,
      tab, userEvent.tab(); userEvent.tab({ shift: true });
      keyboard, userEvent.keyboard('{arrowup}');
      copy,
      cut,
      paste, userEvent.paste(screen.getByTestId('input'), '89er12-/.,');
      pointer,
      clear,  userEvent.clear(screen.getByTestId('input'));
      deselectOptions,
      selectOptions,
      type,  userEvent.type(screen.getByTestId('input'), '01234qw'),
      upload
    ```
   - [fireEvent支持事件列表](https://github.com/testing-library/dom-testing-library/blob/main/src/event-map.js)
   - [键盘code工具](https://www.toptal.com/developers/keycode)

### 异步
  - findBy Queries(queries work when you 
    > expect an element to appear but the change to the DOM might not happen immediately.)
  
  - waitFor
  
    > When in need to wait for any period of time you can use waitFor

  - waitForElementToBeRemoved
    > o wait for the removal of element(s) from the DOM you can use waitForElementToBeRemoved

   - [act](https://legacy.reactjs.org/docs/  testing-recipes.html#act)
    > 一般是异步更新组件状态的操作地方使用 但是要注意 尽量避免使用act 同时推荐使用@testing-library/react 导入act 为了保持一致性

## renderHook
 测试hooks

## 遇到一些问题

1. Error: Uncaught [TypeError: Cannot read properties of undefined (reading 'white')]

> 和颜色有关的一般是和theme提供的相关包裹组件有关系 如下操作就行
```jsx
  import { ThemeProvider } from '@chakra-ui/react';
  import activeTheme from '@payment/theme';

  <ThemeProvider theme={activeTheme}>
    <Test />
  </ThemeProvider>
```

2. Error: Uncaught [Error: Invariant failed: You should not use <Link> outside a <Router>]
  
> 需要在测试组件上面包裹 BrowserRouter 组件 ， Before using {Route} from 'react-router-dom' library, just make sure you put <Route> inside of <BrowserRouter>. If not you will get the same Error.
[reference](https://github.com/marmelab/react-admin/issues/3078)

3. Error: Uncaught [TypeError: history.createLocation is not a function]
> 一般是使用了router高阶组件 然后没有相应的mock模块导致  比如Redirect
```jsx
  // 添加如下mock
  jest.mock('history', () => ({
    ...jest.requireActual('history'),
    createLocation: jest.fn,
  }));
```
4. Fixing React Testing Library 'test was not wrapped in act' warning
   refer to https://chrisboakes.com/fixing-act-error-react-testing-library/

### 推荐
1. 使用 screen 的好处是：在添加/删除 DOM Query 时，不需要实时地解构 render 的返回值来获取内容。输入 screen，你的编辑器就能自动补全它里面的 API 
2. 建议：用 @testing-library/jest-dom 这个库
3. 建议：去了解什么时候应该用 act，别把啥东西都往 act 里放
4. 使用错误的 Query（参考： https://testing-library.com/docs/queries/about/#priority）
5. 不建议使用 container.querySelector 来查询元素
6. 多数情况下没有使用 *ByRole role list mdn https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles
7. 没有使用 @testing-library/user-event
8. 没有用 query* 来断言元素不存在
9. 建议：当查询那些不能立马能访问到的元素时，使用 find*, 而不是用 waitFor 等待 find* 的查询结果
10. 建议：把副作用放在 waitFor 回调的外面，回调里只能有断言

refer to [使用 React Testing Library 的 15 个常见错误](https://mp.weixin.qq.com/s/pgdcDNjDGPgNq76Zh_dZxg)

## 相关文章
- [Common mistakes with React Testing Library](https://kentcdodds.com/blog/common-mistakes-with-react-testing-library#wrapping-things-in-act-unnecessarily)
- [Write fewer, longer tests](https://kentcdodds.com/blog/write-fewer-longer-tests)
- [Fix the "not wrapped in act(...)" warning](https://kentcdodds.com/blog/fix-the-not-wrapped-in-act-warning)
