---
title: Git
date: 2023-01-30 00:21:54
tags:
---

## 1.git clone 仓库地址

克隆仓库

## 2.git remote -v

查看远程地址别名

[![image-20221213213529978](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202301300022308.png)](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202212132136989.png)

别名为o

## 3.git pull 仓库别名 分支名

更新仓库

 仓库别名默认origin，可使用git remote -v查看，分支名一般用master

 例： git pull origin master

## 4.上传文件三步：

* git add 文件名（*代表添加全部）
* git commit -m ‘message’ 此处必须写提交的注释，方便后期回溯版本
* git push 别名 分支名 推送到远端

## 5.git status 查看文件的状态

[![image-20221213214441804](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202301300022351.png)](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202212132144840.png)

Changes not staged for commit：指的是已经add但是没有提交的文件

no changes added to commit：指的是没有add的文件

[![image-20221213214849977](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202301300022389.png)](https://xiehangblog.oss-cn-beijing.aliyuncs.com/pic/202212132148015.png)

添加后文件颜色变为绿色，说明等待commit提交

## 6.git rm -r –cached

清空git 缓存

如果添加不了，查看git status查看没有







# 分支

使用git checkout -b参数来创建一个分支，创建完成分支后会自动切换过去

git checkout -b dev

等价于

```cpp
git branch dev
git checkout dev
```



然后我们在使用branch来查看当前属于哪个分支，也就是查看HEAD的指向

```bash
git branch
```



git合并分支：git merge
当我们新建分支并做完工作之后，想要把分支提交至master，只需要切换到master仓库，并执行git merge 分支名就可以了

如我们在分支中新建了一个f.c和test.c的文件

然后在使用git checkout master切换到master

在使用==git merge dev==将其合并

> 这里需要说一点，如果你在任何分支下创建文件，没有提交到仓库，那么它在所有仓库都是可见的，比如你在分支dev中创建了一个文件，没有使用git add和git commit提交，此时你切换到master，这个文件依旧存在的，因为你创建的文件在工作目录中，你切换仓库时git只会更新跟仓库有关的文件，无关的文件依然存放在工作区。



git删除本地分支:   git branch -D 分支名

git删除远程分支：git push origin --delete

> 注意这里的远程分支名不需要加origin，输入分支名就可以了



git修改分支名称：git branch

使用-m选项

git branch -m 分支名 新的分支名





我们可以使用git stash命令来保存当前工作状态

```bash
git stash
```

保存工作状态之后可以使用git stash list查看当前存储了多少工作状态

```bash
git stash list
```

当在别的分支做完事情之后，在切换回刚刚的分支，然后在刚刚的分支中将状态恢复

```bash
git stash pop
```





可以使用git fetch把远程全部分支拉取下来，同时也包括这些分支的仓库版本，log日志等，这个操作不会进行合并。

```bash
git fetch
```



#  回溯

## 撤销添加到暂存区的文件 （git add)

1. `git reset HEAD -- .` (注意最后的一个".",这条命令帮助我们一次性撤销所有放入暂存区的文件)
2. `git reset HEAD -- filename`(撤销指定目标文件)
3. `git rm --cached filename`(撤销指定目标文件)



> `git rm -f filename`命令，也能把文件从暂存区删除，但是此命令也同时删除了本地文件，回收站中也找不到了，提醒广大同胞，**慎重使用**此命令来撤销暂存区的文件。不用add相比普通rm



# 回滚版本

reset参数是重置命令

--hard是重置代码仓库版本

有三种模式

--soft 、--mixed以及--hard是三个恢复等级。

* 使用--soft就仅仅将头指针恢复，已经add的暂存区以及工作空间的所有东西都不变。
* 如果使用--mixed，就将头恢复掉，已经add的暂存区也会丢失掉，工作空间的代码什么的是不变的。
* 如果使用--hard，那么一切就全都恢复了，头变，aad的暂存区消失，代码什么的也恢复到以前状态。





git log 查看

git reset --hard 要回滚id

git reset --hard HEAD^  上一个版本

git reset --hard HEAD~3

后面的3，代表以当前版本为基数，回滚多少次。HEAD~3代表回滚master前三个版本





将文件撤销回到最近一次修改的状态：git checkout -- file 

恢复add后的文件，比如a文件add，修改a，写错了退回上次add的版本



查看单个文件可回滚版本：**git log filename**

当我们想回滚指定文件到指定版本时，需要查看该文件有多少个版本可以回滚时，可以使用git log filename命令

git reset 1a1e91bf37add6c3914ebf20428efc0a7cea33f3 min.c



查看提交历史：git reflog

git reflog可以查看当前版本库的提交历史，凡是对仓库版本进行迭代的都会出现在这个里面，包括你回滚版本都会出现在这个历史中
