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

### React 源码参考文章
- [图解React原理系列](https://7kms.github.io/react-illustration-series/)
- [React技术揭秘](https://react.iamkasong.com/)

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

### render commit 主要做了哪些事情（这个非常非常非常重要的）
1. render阶段分为beginWork和completeWork, commit阶段分为before mutation和mutation阶段以及layout阶段
2. **beginWork:** 深度向下遍历 生成或者更新workInProgress 的fiber节点
3. **completeWork:** 生成fiber节点对应的dom节点（stateNode) 以及处理相关是事件注册 style props
4. **before mutation:** 处理blur 和focus逻辑  getSnapshotBeforeUpdate(类组件)  调度useEffect(函数组件))
5. **mutation:**  便利effectList 根据flags操作  然后把workInProgress 切换为current(真正实现界面变化的一步)
6. **layout:** 调用componentDidUpdate componentDidMount以及setState回调函数 以及ref相关处理



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
3. 这个调度中 剩余时间能渲染多少内容是怎么计算的？
4. 为什么函数组件通过Hooks可以保存state
  > 因为state不是保存在函数上 而是保存在fiber节点上
5. 对应生命周期 hooks在源码中的哪些阶段调用？
  > render constructor render shouldComponentUpdate 以及由于会多次触发而移除的（componentWillMount ComponentWillReceiveProps componentWillUpdate)
  > commit componentDidUpdate componentWillUnMount componentDidCatch 还有useEffect
6. getSnapshotBeforeUpdate作用
  > getSnapshotBeforeUpdate是为了解决异步调用过程中的多次调用问题，我们在代码中应该尽量使用getSnapshotBeforeUpdate来代替原来的生命周期

## Diff 算法细节
  1. 单节点 先比较key 在比较type 如果都相同 则复用
  2. 多节点()
    整体来说数组类型会遍历两遍，只有特殊情况才会遍历一遍。
    第一遍先遍历newChild，然后判断是否可以复用（源码是通过updateSlot函数判断），如果不能复用就跳出当前遍历，如果可以复用，继续向下遍历
    第一轮遍历结束有三种结果：
    - newChild遍历完
    - oldFiber遍历完
    - newChild和oldFiber都没遍历完
    第一种 第二种情况都比较好处理 第一种情况移除oldFiber剩余节点 第二种情况对newChild剩余节点都是的新建操作，
    这里有个问题 为什么需要第二次遍历  两次遍历区别是啥 第二次遍历目的是啥
    试想一下我们如何比对两个数据，第一步比对长度  如果长度相同再比较 长度相同我们可以for循环遍历 然后判断相同索引的的数组元素是否相同，当时如果我们需要找出两个数组之间的差异，而不是只是简单的判断是否相等，就需要判断数组元素是否有移动这种情况了，这时候我们就需要把其中一个数组转换为map（去重） 然后遍历另一个数组判断
    很明显我们这里的第一遍遍历就是判断两个数组的相同索引的元素是否相同 这输入简单场景
    第二遍遍历就是判断数组元素有移动的场景， 同时在还做了一个关于位置移动的优化 即入oldIndex > lastPlaceIndex（表示当前最后一个可复用的节点， 对应oldFiber上一次更新中所在位置索引）时候不需要移动， 这个优化提示我们尽量避免将节点从后面移动到前面

## setState细节
https://zhuanlan.zhihu.com/p/372275423


## fiber
- [fiber设计文档](https://github.com/acdlite/react-fiber-architecture)

[React源码揭秘3 Diff算法详解](https://juejin.cn/post/6844904167472005134#heading-12)
