## 写在前面
git命令繁杂，不怎么常用的又记不住，自己去百度又太麻烦了，现根据git的功能对git命令做一个分类文档，方便查阅（当然你也可以通过搜索某个关键词来查找你想要的信息，比如搜索tag，你就会找到所有与tag相关的命令）。如果你熟悉了本文档，那对你也是大有裨益。该文档或许不完善，但会持续更新....
> 如有建议欢迎提出  
> 本文档github地址[gitDoc](https://github.com/moyoha/gitDoc)

在开始前，我们先做出如下约定：  
`<localBranch>`  指本地分支  
`<originBranch>` 指远程分支  
`<branchName>` 指分支名称  
`<repoAddress>` 指仓库地址  
`<commit>`  指某个commit记录  
`<tagName>`  指标签名  
## 设置命令别名
```git
git config --global alias.st status                 // git status ==> git st
git config --global alias.ci commit                 // git commit ==> git ci
git config --global alias.co checkout             	// git checkout ==> git co
git config --global alias.br branch                 // git barnch ==> git br
git config --global alias.sh stash                  // git stash ==> git sh
git config --global alias.pop "stash pop"           // git stash pop ==> git pop
```
## 查看
```git
# 查看git版本
git --version
# 查看用户配置
git config --global  --list
# 查看当前分支信息
git status
# 查看本地提交历史
git log
# 查看本地最后n次提交
git log -n
# 查看本地分支
git branch
# 查看远程分支
git branch -r
# 查看所有分支
git branch -a
# 查看本地分支与的远程分支的关联情况
git branch -vv
# 查看标签
git tag
# 查看标签与之对应的提交信息
git show <tagName>
```
## 新建
```git
# 新建一个本地分支，但不会切换到该分支上
git branch <localBranch>
# 为某个commit记录创建一个分支
git branch <brancName> <commit>
# 从某个分支新建一个分支
git branch <brancName> <localBranch>
# 新建一个本地分支，并切到该分支
git checkout -b <brancName>
# 新建一个本地分支，同时切换到该分支，并且关联该远程分支
git checkout -b <branchName> origin/<originBranch>
# 新建一个和远程同名的分支，同时切换到该分支，并且关联该远程分支
git checkout --track origin/<originBranch>
# 新建一个附注标签，并添加标签信息
git tag -a <tagName> -m "some message"
# 新建一个轻量标签
git tag <tagName>
# 给某一个commit他标签
git tag <tagName> <commit>
```
## 切换
```git
# 切换到本地的另一个分支
git checkout <localBranch>
# 强制切换到本地的另一个分支，该操作会丢失在当前分支所做的修改，慎用
git checkout <localBranch> -f
# 新建一个本地分支，并切到该分支
git checkout -b <localBranch>
# 新建一个本地分支，同时切换到该分支，并且关联该远程分支
git checkout -b <branchName> origin/<originBranch>
# 切换到某个tag
git checkout <tagName>
```
## 删除
```git
# 删除(一个或多个)本地该分支（不能删除当前所在的分支，不能删除没有合并到master上的分支）
git branch -d <localBranch> ...
# 删除(一个或多个)本地该分支（不能删除当前所在的分支，可以删除没有合并到master上的分支）
git branch -D <localBranch> ...
# 删除远程分支
git push -d origin <originBranch>
# 删除远程分支
git push origin -d <originBranch>
# 删除最新提交，只能删除本地的提交记录
git reset --hard HEAD^
# 删除本地tag
git tag -d <tagName>
# 删除远程tag
git push origin --delete <tagName>
```
## 拉取
```git
# 拉取与当前分支关联的远程分支代码并进行合并
git pull
# 拉取与当前分支关联的远程分支代码并通过变基进行合并
git pull --rebase
# 拉取远程某个分支的代码并与当前分支进行合并
git pull origin <originBranch>
# 拉取远程某个分支的代码并与本地分支进行合并
git pull origin <originBranch>:<localBranch>
```
## 推送
```git
# 推送到已关联的远程分支
git push
# 推送当前分支到指定远程分支
git push origin <originBranch>
# 推送某个本地分支到某个远程分支
git push origin <localBranch>:<originBranch>
# 推送指定tag到远程
git push origin <tagName>
# 推送所有不在远程的tag到远程
git push --tags
```
## 关联
```git
# 推送并与远程分支建立联系，若远程不存在该分支则自动创建
git push --set-upstream origin <originBranch>
# 与远程分支建立关系，远程必须存在该分支
git branch --set-upstream-to=origin/<originBranch> <localBranch>
# 被废弃的方式 与远程分支建立关系
git branch --set-upstream <localBranch> origin/<originBranch>
# 将本地仓库与远程仓库关联
git remote add origin <repoAddress>
# 新建一个本地分支，同时切换到该分支，并且关联该远程分支
git checkout -b <branchName> origin/<originBranch>
```
## 暂存
```git
# 贮存当前改动
git stash
# 查看贮存列表
git stash list
# 应用某个贮存（默认第一个），即git stash pop stash@{0} 
# 可修改最后的数字，来指定应用某个贮存，该命令同时会将应用的贮存删除
git stash pop
# 应用某个贮存（默认第一个），即 git stash apply stash@{0}
# 可修改最后的数字，来指定应用某个贮存，该不会删除贮存
git stash apply
# 删除某个贮存（默认第一个），即git stash drop stash@{0} 
# 可修改最后的数字，来指定删除某个贮存
git stash drop
# 查看某个贮存（默认第一个）做了那些改动，即 git stash show stash@{0} 
# 可修改最后的数字，来指定查看某个贮存
git stash show
# 删除所有贮存
git stash clear
```
## 克隆
```git
# 克隆master分支代码
git clone <repoAddress>		
# 克隆某个分支的代码
git clone -b <originBranch> <repoAddress>
```
## 修改
```git
# 修改分支名称 <oldBranch>原始分支名称 <newBranch>新分支名称
git branch -m <oldBranch> <newBranch>
```
## 合并
```git
# 将某个分支合并到当前分支
git merge <branchName>
# 将当前分支变基到某分支
git rebase <branchName>
```

