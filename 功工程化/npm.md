


## 发布一个NPM包
### 相关常用命令
- npm who am i
  判断是否有登录账户

- npm login
  npm 登录

- npm publish
- npm link 使用npm link命令，将npm 模块链接到对应的运行项目中去，方便地对模块进行调试和测试，需要两步
  1. 在依赖项目 目录使用 npm link 创建全局的软连接
  2. 在调试项目使用 npm link deps-package-name 告诉应用程序使用全局软链 
- npm unlink 取消软连接
- 版本修改：
npm version patch：1.0.0会变成1.0.1
npm version major：1.0.0会变成2.0.0
npm version minor：1.0.0会变成1.1.0

### package.json 文件
 1. name 包名 需要保证唯一性
 2. version  版本号
 3. main 入口文件
 4. scripts 脚本
 5. keywords 关键词
 6. author 作者
 7. license 证书

### 发布流程
1. npm 源管理
   npm发包必须使用npm的源镜像，不能使用淘宝之类的镜像

   ```shell
    # 查看npm源
    npm config get registry

    # 设置npm源镜像
    npm config set registry https://registry.npmjs.org
   ```
2. 注册npm账号
3. 创建NPM包
   注意需要在NPM官网查看想设置的包名是否已经被使用

- [npm 发布 参考](https://blog.csdn.net/m0_62982672/article/details/126701718)
- [NPM 发包](https://www.jianshu.com/p/1789471a92e1)

## 常见错误
1. npm ERR! you do not have permission to publish “your module name”. Are you logged in as the correct user?
  包名被占用，改个包名即可。最好在官网查一下是否有包名被占用，之后再重命名

2. 需要考虑添加证书
   [license](https://license.md/)