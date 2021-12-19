## git 常用命令记录

### git 同步远程仓库(远程有新分支，本地没有)
```shell
git fetch
git branch -a
git checkout -b 远程分支名 origin/远程分支名
```

参考 git同步远程仓库[https://www.jianshu.com/p/811b07b129e8]


## Git 多平台换行符问题(LF or CRLF)
 autocrlf 配置项
 true: 提交时转换为 LF，检出时转换为 CRLF
  false: 提交检出均不转换
  input: 提交时转换为LF，检出时不转换
  
[refference](https://blog.konghy.cn/2017/03/19/git-lf-or-crlf/)
