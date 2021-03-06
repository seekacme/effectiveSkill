sh-keygen -t rsa
=======================================================================
标准操流程
git clone ssh://vcs-user@lfz212.imwork.net:2222/source/all_in_one.git
git checkout -b develop origin/develop
git checkout -b gjs_feature develop
do something

git pull    |- git fetch origin
            |- git merge origin/当前分支的对应分支
            
git add .
git commit -m 'some commit'
git checkout develop
git merge gjs_feature

**resolving conflict**
git diff branch1 branch2 >>~/coflict.diff

git push develop
=======================================================================

# install git
sudo apt-get install git

# config
git config --global user.name kaku
git config --global user.email scugjs@163.com

# initial example
git init
git status
git add readme.md
git commit -m 'update readme.md'
git checkout -b develop origin/develop
git branch -D dev
git stash #隐藏工作状态
git stash apply & git stash drop

# git remote
git clone ssh://vcs-user@lfz212.imwork.net:2222/source/all_in_one.git  
git clone -b development ssh://vcs-user@lfz212.imwork.net:2222/source/all_in_one.git  
git clone -o oth_origin ssh://vcs-user@lfz212.imwork.net:2222/source/all_in_one.git  
git remote [-v]  
git remote show <主机名>  
git remote add <主机名> <地址>  
git remote rm <主机名>  
git remote rename <原主机名> <新主机名>  
eg:  
git remote add origin git@github.com/kakuchange/learnPython.git  

# git fetch
git fetch <远程主机名> <分支名>
git fetch origin master
取回远程更新后，可在本地主机上新创建分支
git checkout -b newbranch origin/master
或在本地分支上合并远程分支
git merge origin/master
git rebase origin/master

# pull远程指定分支并与当前分支融合
git pull <远程主机名> <远程分支名>:<本地分支名>
git pull
git pull origin develop  # 与当前分支merge
git pull origin develop:develop
git push --force origin强制推送
git pull相当于 -p 在本地删除远程已经删除的分支

# 查看工作区和版本库里面的区别
git diff readme.md
git log
git log --pretty=oneline
git reflog
git log --oneline --graph

# 版本回退 HEAD指当前版本，HEAD^指前一版本
git reset --hard HEAD^
git reset --hard HEAD~100
git reset --hard 6fcfc89

# 丢弃工作区改动（回到最近一次commit或add后的状态）
git checkout -- file
git checkout -- readme.md 回到暂存区或库中版本！
git rm --cached readme.md 从缓存区撤回
# 丢弃暂存区改动（与版本库同步）
git reset HEAD file
# 隐藏工作现场
git stash
git stash list
git stash pop
git stash apply stash@{0}

# push local master 
git push <远程主机名> <本地分支名>:<远程分支名>
git push -u origin master #指定默认主机
git push origin master：master
git push 默认push当前分支

# 查看远程分支
git branch -a

# 删除远程分支
git push origin :branch-name

# 建立追踪关系
git branch --set-upstream development origin/development

# tag
git tag v0.1
git push --tags
git push origin :refs/tags/ver0.1

# 各种取消操作
git rm –cached filename#add之后取消！
git command --amend #重新编辑提交message！合并提交！
git checkout -- readme.md #撤销本地修改
git reset --hard <commit_ish> #commit后修改回到某个ish位置，连同硬盘（本地修改）
git reset --mixed <commit_ish> #修改HEAD，提交记录变，但文件变（本地未修改）默认！
git reset --soft <commit_ish> #相当于mixed方法后再git add
soft (commit) < mixed (commit + add) < hard (commit + add + local working)

# rebase
如果是对local 私有的临时性质的分支，则直接git rebase -i master(梳理历史信息比
如合并成一个commit)+git merge产生一个fast forward,最终以一个commit展示在master分支上

# merge
marge 特点：自动创建一个新的commit
如果合并的时候遇到冲突，仅需要修改后重新commit
优点：记录了真实的commit情况，包括每个分支的详情
缺点：因为每次merge会自动产生一个merge commit，所以在使用一些git 的GUI tools，特别是commit比较频繁时，看到分支很杂乱。

合并时如果出现冲突需要按照如下步骤解决
1.修改冲突部分
2.git add
3.git rebase --cotinue
4.（如果第三步无效可以执行  git rebase --skip）
5.不要在git add 之后习惯性的执行 git commit命令
