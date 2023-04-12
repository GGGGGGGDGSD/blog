


- [参考](https://zhuanlan.zhihu.com/p/35237759)
- [掘金](https://juejin.im/entry/5c26d0db6fb9a04a0e2d45a4)
- [1](https://juejin.im/post/5a989fb451882555731b88c2)

## lerna 介绍
Lerna 是一个用来优化托管在git\npm上的多package代码库的工作流的一个管理工具,可以让你在主项目下管理多个子项目，从而解决了多个包互相依赖，且发布时需要手动维护多个包的问题。目前babel、react都使用了lerna的多包管理。
主要解决多包依赖 手动维护版本号等麻烦问题

## 特征
1. 代码复用高 方便本地在多项目中调试 引用
2. 依赖管理方便 因为在同一个仓库 多项目之间的依赖管理比较方便

[lerna维护状态](https://zhuanlan.zhihu.com/p/398080866)

## 基本命令
- lerna init
  lerna repo 初始化或者将已经存在的repo转化为lerna管理

- lerna create
  创建一个公共包

- lerna bootstrap
  在当前 Lerna 仓库中执行引导流程（bootstrap）。安装所有 依赖项并链接任何交叉依赖

- lerna add
  增加本地或者远程package做为当前项目packages里面的依赖

- lerna changed
  检测自上次发布后被修改过的软件包

- lerna diff [package]
  列出软件包的修改细节

- lerna list
  列出当前repo中的所有公共软件包

- lerna import 
  导入本地已经存在的公共包

- lerna clean
  删除所有包的node_modules目录 

- lerna run
  运行公共包下面的脚本指令
  ```shell
  # 执行公共包@payment/front-desk里面的start指令
  "lerna --scope=@payment/front-desk run start",
  ```

- lerna exec
  执行命令在每个包

- lerna publish
  为已经更新过的软件包创建一个新版本。提示 输入新版本号并更新 git 和 npm 上的所有软件包


