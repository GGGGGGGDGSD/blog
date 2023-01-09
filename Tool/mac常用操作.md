## 快捷键
- 截图
Shift + Command + F5

- 切换隐藏文件显示
Shift + Command + .


- 解压
unzip filename
https://blog.csdn.net/u012988591/article/details/76976808

- VS 
https://docs.microsoft.com/zh-cn/visualstudio/mac/keyboard-shortcuts?view=vsmac-2019




## java JDK setting
https://mkyong.com/java/how-to-set-java_home-environment-variable-on-mac-os-x/
https://stackoverflow.com/questions/22842743/how-to-set-java-home-environment-variable-on-mac-os-x-10-9

卸载jdk
https://cloud.tencent.com/developer/article/1813197

- 注意JDK与JRE区别
https://www.runoob.com/w3cnote/the-different-of-jre-and-jdk.html

## 软件
- hosts edit
[SwitchHosts](https://github.com/oldj/SwitchHosts)

## 环境问题
- Ivy UNRESOLVED dependencies
- https://stackoverflow.com/questions/28732127/ant-unresolved-dependencies-hsqldbhsqldb1-8-0-10-not-found-when-building-so

## Mac 包管理器 Homebrew
- [程序员 Homebrew 使用指北](https://sspai.com/post/56009)
### 安装brew
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

  参考 https://mac.install.guide/ruby/3.html

## 全局环境变量管理 profile 与 bash_profile文件来管理
.profile：系统级别的环境变量和启动程序，配置对所有用户生效
.bash_profile： 用户级别， 只对单一用户生效

- 如果没有这个文件（刚创建的新用户一般都没有） 可以用vim 或者touch 命令创建
  touch .bash_profile

- 立即生效执行
  source .bash_profile

- 查看配置是否成功
  echo $PATH（配置的环境路径名）