## 调试
- git clone 拉取源码
- 安装依赖
- 执行打包命令 yarn build react/index,react/jsx,react-dom/index,scheduler, react-reconciler --type=NODE
  打包react、scheduler、react-dom三个包为dev环境可以使用的cjs包。

- 通过yarn link可以改变项目中依赖包的目录指向
  cd build/node_modules/react
   # 申明react指向
   yarn link
   cd build/node_modules/react-dom
   # 申明react-dom指向
   yarn link

- 创建项目
   yarn link react react-dom （将项目内的react react-dom指向之前申明的包
- 关于更新
  需要重新执行打包命令 执行打包命令  并且测试项目有需要重新运行  其他不变

参考： https://react.iamkasong.com/preparation/source.html#%E6%8B%89%E5%8F%96%E6%BA%90%E7%A0%81

### 开启concurrent 模式
```js
import ReactDOM from 'react-dom';

// 如果你之前的代码是：
//
// ReactDOM.render(<App />, document.getElementById('root'));
//
// 你可以用下面的代码引入 concurrent 模式：

ReactDOM.unstable_createRoot(
  document.getElementById('root')
).render(<App />);
```
[参考](https://zh-hans.reactjs.org/docs/concurrent-mode-adoption.html)


## 查看react 的fiber结构
this._reactInternals [参考](https://codesandbox.io/s/busy-jang-b26hy?file=/src/App.js:179-199)



### render

  performSyncWorkOnRoot
  performConcurrentWorkOnRoot(异步)

    workLoopConcurrent

      performUnitOfWork(两个阶段 )
        
        beginWork
          reconcileChildren
            ChildReconciler(diff算法)
        
        completeUnitOfWork
          completeWork


### 状态更新(至此 状态更新就和我们所熟知的render阶段连接上了。)
  触发状态更新（根据场景调用不同方法）

      |
      |
      v

  创建Update对象（接下来三节详解）

      |
      |
      v

  从fiber到root（`markUpdateLaneFromFiberToRoot`）

      |
      |
      v

  调度更新（`ensureRootIsScheduled`）

      |
      |
      v

  render阶段（`performSyncWorkOnRoot` 或 `performConcurrentWorkOnRoot`）

      |
      |
      v

  commit阶段（`commitRoot`）

  1. 出发状态更新的几种方式
    - setState
    - render
    - useState
    - useReducer
    - forceUpdate


## reconciler 工作流程
1. 输入 scheduleUpdateOnFiber
      ||
      V
2. 注册调度任务 ensureRootIsScheduled





3. 执行任务回调  在内存中构造fiber树       
   
performSyncWorkOnRoot
                             =>    performUnitOfWork   =>  （  beginWork： 通过Schedule调度递归向下的构造fiber节点（氛围update mount阶段）
                                                              completeWork： 递归向上处理fiber节点的props ref 并处理带有effect tag节点生成effectList 供commit 阶段使用
performConcurrentWorkOnRoot



4. 提交输出 commitRoot

## hooks 

1. hooks数据结构
   ```js
   const hook: Hook = {
    memoizedState: null,
    baseState: null,
    baseQueue: null,
    queue: null,
    next: null,
  };
   ```


## react启动(三个模式 三个全局对象)
  1. render
   
  2. legacyRenderSubtreeIntoContainer
    if (first) {
     legacyCreateRootFromDOMContainer
    }

    updateContainer
  
  3. updateContainer => scheduleUpdateOnFiber


### QS
1. 如何把stateNote打印到页面上
2. 初始构建的时候 既然在beginWork是递归构建Fiber 那此时是地归谁来得到fiber
