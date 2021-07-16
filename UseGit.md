## 分支

#### 开发分支

#issue-描述

#### 目标分支

master

## 合并两个分支

开发分支只有自己在用的情况下使用 rebase 合并分支

1. master 分支拉取最新代码

```bash
git pull origin master
```

2. 回到开发分支

```bash
git checkout #issue-描述
```

3. 将开发分支多次的提交合并成一次

```bash
git rebase -i commitID
```

​	如果不知道哪个版本，可以使用 git log 查看,选择你要合并的提交的前一个提交的id，使用 q 退出。

​	1.除了第一个pick保留，其他的pick换成sqush。保存并关闭文件

​	2.修改合并提交的提交信息。保存并关闭文件

4. 合并分支

```bash
git rebase master 
```

​	此时很可能会产生冲突，解决冲突后

```bash
git rebase --continue
```

​	此时本地分支就已经合并完成了

5. 切到master

```bash
git checkout master
```

6. master合并本地分支代码并推送到远端

```bash
git merge #issue-描述
git push origin master
```

## 单纯合并commit

1. 查看需要合并哪几个分支

```bash
git log
```

​	复制主要合并的第一个commit的前一个commitID(就是第一个不需要合并的commitID)

2. 合并分支

```bash
git rebase -i commitID
```

3. 将pick除了第一个都改成sqush,保存文件、关闭文件
4. 此时合并可能会出现冲突，解决完冲突（不知道要不要add这些改变）然后继续rebase

```bash
git rebase --continue
```

	5. 修改合并提交的描述，保存文件、关闭文件。如果还有冲突重复第四步。直到成功。
 	6. 强制推送到远程，如果最后合并的代码没有什么问题了，就推送到远程分支，此时是推不上去的，会有冲突，但是我们可以强制推送

```bash
git push -f origin branchName
```

