Git教程&日志

1. 创建版本库
```
git init                        命令把当前目录变成Git管理的仓库
git add <file>                  修改txt文件后添加至仓库
git commit -m "introduction"    给对应的文件版本添加说明
git status                      查看工作区的状态
```
PS：必须要将对应文件放到Git仓库目录内

2. 时光机穿梭
2.1 版本回退
```
git log                 查看提交历史，Head指针指向当前版本
git reset --hard HEAD~n 回退n个版本，注意用commit id区分不同版本
git reflog              查看之前版本改动命令历史
```

2.2 工作区和暂存区
工作区 自己创建的目录
版本库 .git
暂存区 stage/index
分支   branch master，及master指向的HEAD指针
`git add`     将工作区的文件添加至暂存区中
`git commit`  将暂存区全部提交至分支

2.3 管理修改
我们可以多次修改，最终上传至版本库中，而git管理的是修改而不是文件
`git diff` 可以查看工作区和版本库中Head指向的版本之间的区别

2.4 撤销修改
`git checkout -- <file>`
两种情况：
1 工作区修改后未add至暂存区中，因此只改回版本库中最新版
2 已经添加至暂存区，又在工作区修改，撤销回到暂存区的状态
若错误修改已add至暂存区？`git reset HEAD <file>` 将暂存区的修改撤销
若错误修改已提交至版本库？则回退一节！

2.5 删除文件
```
rm <file> 删除文件
git rm <file>
git commit -m "remove introduction" 从版本库中删除
git restore --staged <file> 恢复删除的文件
```

3. 远程仓库
创建ssh，若有rsa则不用设置，否则：
`ssh-keygen -t rsa -C "youremail@example.com"`
`id_rsa`      秘钥
`id_rsa.pub`  公钥

`git remote add origin git@github.com:user/.git` 在本地关联github仓库
这里可能存在一些问题，因为自己使用了github反代，因此
`ssh -T git@github.com` 无法直接成功
需要将反代关闭，才能连接到端口，并成功push
`git push -u origin main` 将repo中的commit同步至远程库origin中
`git clone git@github.com:user/.git` 克隆一个库

4. 分支管理
4.1 创建与合并分支
```
git checkout -b dev 创建并切换dev分支
git branch          查看当前分支
git checkout master 切换到master分支
git merge dev       将当前分支合并到dev分支上
git branch -d dev   删除dev分支

git switch -c dev   创建并切换
git switch master   切换
```

4.2 解决冲突
多个分支对同一文件进行了修改
git log 可以查看分支的合并情况
需要手动编辑以保持一致

4.3 分支管理策略
通常合并分支采用`Fast Forward`模式，但这样删除后会丢失分支信息。因此，我们可以使用`--no-ff`方式的`git merge`。

e.g. `git merge --no-ff -m "merge with no-ff" dev`

分支策略
master分支是稳定的，用于发布新版本
dev分支是不稳定的，用来干活，个人的分支往dev上合并
加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

4.4 bug分支
```
git stash                   储存工作现场
git stash list              查看工作现场
git stash apply             恢复但内容不删除
git stash drop              删除
git stash pop               恢复并删除
git stash apply stash@{n}   恢复指定的stash
git cherry-pick             复制特定的提交到当前分支
```

4.5 feature分支
用于添加实验性质的代码
若要丢弃一个没有合并过的分支，需要`git branch -D <name>`

4.6 多人协作
推送分支
`git push origin <branch>`
哪些分支需要同步推送？master、dev都需要
抓取分支
若要抓取dev分支，则可以用命令`git checkout -b dev origin/dev`，创建远程origin的dev分支到本地
`git pull`    抓取最新提交

因此，多人协作的工作模式通常是这样：
   1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
   2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
   3. 如果合并有冲突，则解决冲突，并在本地提交；
   4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！
如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

4.7 rebase
`git rebase`    将提交历史变成一条直线
小结：
* rebase操作可以把本地未push的分叉提交历史整理成直线；
* rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

5. 标签管理
```
git branch
git tag <name>
git tag -a <name> -m "introduction" commit id
git show <tagname>  查看说明文字
git tag -d
git push origin <tagname>
git push origin :refs/tags/<tagname>
```

6. 总结
[关于git的常用命令](https://cloud.tsinghua.edu.cn/f/8ca40762ab384741a9fe/)