## 调试
- git clone 拉取源码
- 安装依赖
- 执行打包命令 yarn build react/index,react/jsx,react-dom/index,scheduler --type=NODE
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

参考： https://react.iamkasong.com/preparation/source.html#%E6%8B%89%E5%8F%96%E6%BA%90%E7%A0%81



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


### 状态更新
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
