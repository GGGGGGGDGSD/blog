## git 常用命令记录

## git diff
- 比较不同分支
git diff branch1 branch2

- 比较不同分支的文件
git diff --name-status branch1 branch2

- 比较不同分支的同一个文件
git diff br1 br2 file

## git reset
Revert some existing commits

- git reset xxx
从暂存区移动到工作区


- git reset HEAD xxx (同上)
取消文件的暂存  从暂存区移动到工作区 实现同效果命令  git restore --staged xxx

- get reset --hard xxx
回滚提交的文件到制定的  commit，并且不保留文件的


## git checkout 
- git checkout xxx
撤销对文件的修改，还原成上一次提交时的状态

- git checkout -b 分支
切换分支

## git revert 
Revert some existing commits
删除某次commit  会产生新的提交记录， 不过确实很实用
revert 恢复会保持之前的提交记录并生成新的commit    reset 不会之前重置到制定的commit 没有任何记录

## git stash
> 多分支切换操作

1. git stash apply 使用而不删除stash里面的记录
2. git stash pop 使用然后删除stash记录
3. git stash drop 删除记录
4. git stash -u 储存未跟踪的文件（这个很有用 因为默认是不是储存为跟踪的文件的
5. git stash save (使用git stash save命令取代git stash，给每次stash填写一个message作为标识
6. git stash show (查看指定 stash 的 diff
7. git stash push -m "test" src/ConfirmModal/ src/FloatAlert/ stash指定的文件 文件夹以及多个文件


## Administration
### git reflog 
Manage reflog information

## branch
- 删除远程分支
git push origin --delete branch

- 拉取远程分支到本地
git checkout -b branch  origin/branch

## 其他
- 查看当前分支commit但没有push的
git cherry -v

- 查看已经被合并的分支
git branch --merged

- 产前当前本地分支与远程分支的对应关系
git branch -vv

318133f9d54cc1d8d661cda66c8442d375eed32f

- Git合并特定commits 到另一个分支
git cherry-pick commit-id

- 多次commit如何合并成一个commit(修改PR时，如何只提交一个commit)
  1. git rebase -i [commitID]  git push -f git rebase --abort
  [参考](https://blog.csdn.net/mlz_2/article/details/124302900)

  2. 在自己独立开发的分支（已有commit）上需要合并master分支的最新代码，这种也可以使用 git rebase (变基)
1.  - git rebase master
2.  - git rebase --continue

  1. git reset [commitID]
   这也是一种方式


## 一些常见操作
- 撤销git push 
本地通过git  log 查看获取需要撤销到的commit节点
git reset --hard commitID
最后在 git push origin remote_branch --force 强制推送到远程覆盖

## 一些常见问题
fatal: unable to access 'https://github.com/edmodo/toolbox.git/': Failed to connect to github.com port 443: Timed out
fatal: unable to access ‘https://github.com/.......‘: OpenSSL SSL_read: Connection was reset

git config --global http.sslVerify "false"(https://blog.csdn.net/qq_40999917/article/details/116213557)

应该是需要给git 设置代理
git config --global http.proxy http://127.0.0.1:8118
git config --global https.proxy http://127.0.0.1:8118

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


## 相关问题
1. connect to host github.com port 22: Connection timed out
   https://www.silenceboy.com/2020/03/04/git-clone-%E5%87%BA%E7%8E%B0ssh-connect-to-host-github-com-port-22-Connection-timed-out%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88/index.html




## latest Personal access tokens (三个月)
- Support for password authentication was removed on August 13, 2021

token: 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
