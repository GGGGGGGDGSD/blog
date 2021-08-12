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


## git chekcout 
- git checkout xxx
撤销对文件的修改，还原成上一次提交时的状态

- git checkout -b 分支
切换分支

## git revert 
Revert some existing commits
删除某次commit  会产生新的提交记录， 不过确实很实用
revert 恢复会保持之前的提交记录并生成新的commit    reset 不会之前重置到制定的commit 没有任何记录


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
git cherry-pick


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