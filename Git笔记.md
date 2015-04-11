# 创建版本库

## 创建工作区
```
mkdir folder
```

## 初始化一个Git仓库
```    
cd folder && git init
```

---

# 版本控制

## 添加文件到Git仓库

从工作区添加到暂存区：
```
git add <file>  -可反复多次使用，添加多个文件
```

从暂存区提交到分支：
```
git commit -m "comment"
```

## 查看仓库当前状态
```
git status
```

## 查看修改内容
```
git diff <file>
```

## 查看历史记录
```
git log [--pretty=oneline] [--graph]
```
*`--graph`查看分支合并图*

## 查看命令历史
```
git reflog
```

## 版本重置
```
git reset --hard commit_id
```
**commit_id:** 
+ **HEAD**: 当前版本
+ **HEAD^**: 上一版本
+ **HEAD~100**: 往上100个版本

## 撤销修改
+ 还未add到暂存区：
*直接撤销工作区所做的修改*
```
git checkout -- file
```
+ 已经add到了暂存区，撤销分两步：
**第一步，** *撤销暂存区得修改（unstage）,重新放回工作区：*

```
git reset HEAD file
```
**第二步，** *撤销工作区修改：*

```
git checkout -- file
```
+ 已经commit到分支：
*回退到上一版本：*

```
git reset --hard HEAD^
```

## 删除文件
```
git rm file && git commit -m ""
```

*如果从文件管理器中误删了文件：*
```
rm file
```

*想要恢复，则：*
```
git checkout -- file
```
---

# 远程仓库

## 创建SSH Key
查看 **~/.ssh目录**下有无`id_rsa`和`id_rsa.pub`两个文件，
若没有，则：
```
ssh-keygen -t rsa -C "youremail@example.com"
```
*`id_rsa`： 私钥，`id_rsa.pub`：公钥*

## 添加远程库
关联一个远程库：
```
git remote add <remote-repo-name> git@server-name:path/repo-name.git
```
第一次推送master分支的所有内容到远程库：
```
git push -u <remote-repo-name> master
```

之后，本次本地提交后，推送最新修改：
```
git push <remote-repo-name> master
```

## 从远程库克隆
```
git clone git@server-name:path/repo-name.git
```

---

# 分支管理

## 创建与合并分支
**查看**分支：
```bash
git branch
```
**创建**分支：
```bash
git branch <branch-name>
```
**切换**分支：
```bash
git checkout <branch-name>
```
**创建**并**切换**分支：*`-b`参数表示创建并切换*
```bash
git checkout -b <branch-name>
```
**合并**分支到当前分支：
```bash
git merge [--no-ff] <-m "comment"> <branch-name>
```
*通常合并分支时，Git会用`Fast forward`模式，该模式在分支删除后，会丢掉分支信息，看不出曾做过合并。`--no-ff`参数表示禁用`Fast forward`，这样合并后的历史有分支，能看出曾做过合并。*

**删除**分支：
```bash
git branch -d <branch-name>
```

## 贮存当前分支工作状态
```
git stash
```
查看贮存状态：
```
git stash list
```
恢复贮存内容：
```
git stash apply
```
删除贮存内容：
```
git stash drop
```
恢复并删除：
```
git stash pop
```

# 多人协作

查看远程库信息
```bash
git remote [-v]
```
*`-v` 查看更详细的信息*

**创建远程分支**到本地：
```bash
git checkout -b <remote-repo-name/branch-name>
```
推送自己的修改：
```
git push <remote-repo-name> <branch-name>
```
如果推送失败，则说明远程分支比本地更新，试图合并：
```
git pull
```
如果合并提示`no tracking information`，则说明本地分支和远程分支的链接关系没创建，创建链接关系：
```
git branch <--set-upstream> <branch-name> <remote-repo-name/branch-name> 
```
最后，合并冲突解决冲突，在本地提交之后再次推送。

# 标签管理
查看所有标签：
```bash
git tag
```
创建标签：
```bash
git tag <tag-name> [commit-id]
```
*`commit-id`为空则直接为标签打在最新提交的commit上*

创建带有说明的标签
```bash
git tag -a <tag-name> -m "comment" [commit-id]
```
*`-a`指定标签名，`-m`指定说明文字*

查看说明文字：
```bash
git show <tag-name>
```
删除标签
```bash
git tag -d <tag-name>
```
推送本地标签到远程
```bash
git push <remote-repo-name> <tag-name>
```
推送尚未推送的全部本地标签
```bash
git push <remote-repo-name> --tags
```
删除远程标签：
```bash
git tag -d <tab-name>
git push <remote-repo-name> :refs/tags/<tag-name>
```

