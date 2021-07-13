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
