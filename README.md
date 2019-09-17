### GIT使用小册

文档版本：1.0.0   日期: 2019-08-22   lizheyao authored   

 

##  一．使用说明

#### 1. 在本地分支上创建一个分支并上传到远仓库

```
/**
*在本地分支上创建新的分支，并提交
*注意：创建新分支前，需要git pull 拉去最新代码，这样本地进行merge时，feature合并到
*develop分支时减少conflicts
*/
---->git checkout -b feature/2019/8/21(创建功能分支feature/2019/8/21)
---->做了些修改之后，通过命令提交到本地仓库后
---->git checkout develop (切换到develop分支上，推送分支之前，拉去远程分支最新的代码)
---->git pull 
---->git checkout feature/2019/8/21 
---->git merge develop(合并本地最新的develop分支到功能分支feature/2019/8/21上)
---->解决冲突问题 并add，commit
---->git push --setupstream origin[远程仓库名字] feature/2019/8/21[远程分支名]
```
#### 2. 在错误的分支上修改了代码
##### 1）已经提交代码
```
/**
*如果我们在错误的分支上提交了代码，可以切换到正确的分支上，
*使用git cherry-pick [commitid]把已经提交的内容添加到
*正确分支的提交历史中去，代替手工粘贴复制
*/
---->（errorBranch）git log
---->commitid 5c18e334dc41323f0377aece12d086080757b1fa
---->git checkout correctBranch
---->(correctBranch) git cherry-pick  5c18e334dc41323f0377aece12d086080757b1fa
```
##### 2）未提交代码
```
/**
*如果我们在错误的分支上进行了修改但未提交，可以先stash存储到本地库，
*然后再切换到正确的分支上，apply stash{0}恢复本地库变化
*可能出现冲突合并，需手动解决
*/
---->（errorBranch）git stash
---->git checkout correctBranch
---->(correctBranch) git stash apply  

###########stash############
git stash list  #查看本地储存
git stash drop #删除本地储存
git stash pop 这个命令也可以实现，和上面不同的是会自动删除本地储存，不过出现冲突则不会删除
#######################
```

