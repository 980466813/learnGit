Git is a version control system.
Git is free software.

# Git使用

## Git 命令

> **git status**

- 作用

用于掌握工作区的状态

- 使用

```
[root@localhost learngit]# git status
# 位于分支 master
# 尚未暂存以备提交的变更：
#   （使用 "git add <file>..." 更新要提交的内容）
#   （使用 "git checkout -- <file>..." 丢弃工作区的改动）
#
#	修改：      readme.txt
#

```

> **git diff file**

- 作用

用于查看修改内容

- 使用

```
[root@localhost learngit]# git diff readme.txt
// 此时无修改内容，则不会有任何显示
```

> **git log 以及 git log -pretty=oneline**

- 作用

用于查看过去提交历史，以及格式化输出

- 代码

```
# git log
[root@localhost learngit]# git log
commit dc2f6fe594055b7d271186299bc7b02c0db8dd7c
Author: lning <980466813@qq.com>
Date:   Tue Nov 13 14:16:26 2018 +0800

    修改readme文件，增添git status与git diff命令

commit 5b253c4099dab9deae30b2e993b12bcd556dc75f
Author: lning <980466813@qq.com>
Date:   Tue Nov 13 14:10:34 2018 +0800

    wrote a readme file

# git log -pretty=oneline
[root@localhost learngit]# git log --pretty=oneline
95490bfcd92e6461aaa4735376d8c966e14087b3 修改readme文件，增添git log与git reset命令
dc2f6fe594055b7d271186299bc7b02c0db8dd7c 修改readme文件，增添git status与git diff命令
5b253c4099dab9deae30b2e993b12bcd556dc75f wrote a readme file
```

> **git reset --hard HEAD^**

- 作用

用于回退到上个版本 HEAD^代表上个版本，同理上上个版本就是HEAD^^,往前n个版本则可以写为HEAD~100,同样也可以通过每个版本前6位字符回到回到之前的版本

- 使用

```
# 当前的历史版本
[root@localhost learngit]# git log --pretty=oneline
95490bfcd92e6461aaa4735376d8c966e14087b3 修改readme文件，增添git log与git reset命令
dc2f6fe594055b7d271186299bc7b02c0db8dd7c 修改readme文件，增添git status与git diff命令
5b253c4099dab9deae30b2e993b12bcd556dc75f wrote a readme file
[root@localhost learngit]# git reset --hard HEAD^
HEAD 现在位于 dc2f6fe 修改readme文件，增添git status与git diff命令
[root@localhost learngit]# git log
commit dc2f6fe594055b7d271186299bc7b02c0db8dd7c
Author: lning <980466813@qq.com>
Date:   Tue Nov 13 14:16:26 2018 +0800

    修改readme文件，增添git status与git diff命令

commit 5b253c4099dab9deae30b2e993b12bcd556dc75f
Author: lning <980466813@qq.com>
Date:   Tue Nov 13 14:10:34 2018 +0800

    wrote a readme file

[root@localhost learngit]# git reflog
95490bf HEAD@{0}: reset: moving to 95490b
dc2f6fe HEAD@{1}: reset: moving to HEAD^
95490bf HEAD@{2}: commit: 修改readme文件，增添git log与git reset命令
dc2f6fe HEAD@{3}: commit: 修改readme文件，增添git status与git diff命令
5b253c4 HEAD@{4}: commit (initial): wrote a readme file


[root@localhost learngit]# git reset --hard 95490b
HEAD 现在位于 95490bf 修改readme文件，增添git log与git reset命令

```

> **git reflog**

- 作用

用于查看每一次操作命令

- 使用

```
[root@localhost learngit]# git reflog
95490bf HEAD@{0}: reset: moving to 95490b
dc2f6fe HEAD@{1}: reset: moving to HEAD^
95490bf HEAD@{2}: commit: 修改readme文件，增添git log与git reset命令
dc2f6fe HEAD@{3}: commit: 修改readme文件，增添git status与git diff命令
5b253c4 HEAD@{4}: commit (initial): wrote a readme file

```

> **git checkout --file**

- 作用

用于丢弃某个文件在工作区的修改，以下存在两种情况

一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit或git add时的状态。

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

- 代码
```
[root@localhost learngit]# git checkout --readme.txt

```

> **删除操作**

- 场景1. 需要删除一个已经提交给版本库的文件

```
[root@localhost learngit]# git add test.txt
[root@localhost learngit]# git commit -m '测试文件'
[master b675ec3] 测试文件
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt

// 直接删除文件

[root@localhost learngit]# rm test.txt 
rm：是否删除普通文件 "test.txt"？y
[root@localhost learngit]#


// 删除版本库中所提交的test文件

[root@localhost learngit]# git rm test.txt
rm 'test.txt'
[root@localhost learngit]# git commit -m 'remove test.txt'
[master 6fd9a57] remove test.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt
```

- 场景2. 误删文件，需要使用git checkout -- file进行恢复

```
[root@localhost learngit]# git checkout -- test.txt
[root@localhost learngit]# ls
readme.txt  test.txt
```

- 场景3. 误删版本库中所提交的文件，需要使用git reset --hard xxx进行跳转版本
```
[root@localhost learngit]# git reset --hard HEAD^
HEAD 现在位于 b675ec3 测试文件
[root@localhost learngit]# ls
readme.txt  test.txt

```

> **远程仓库**

- 代码
```
[root@localhost learngit]# git remote add origin https://github.com/980466813/learngit.git
[root@localhost learngit]# git push -u origin master
Username for 'https://github.com': 980466813@qq.com
Password for 'https://980466813@qq.com@github.com':
Counting objects: 24, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (17/17), done.
Writing objects: 100% (24/24), 3.82 KiB | 0 bytes/s, done.
Total 24 (delta 6), reused 0 (delta 0)
remote: Resolving deltas: 100% (6/6), done.
remote: 
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/980466813/learngit/pull/new/master
remote: 
To https://github.com/980466813/learngit.git
 * [new branch]      master -> master
分支 master 设置为跟踪来自 origin 的远程分支 master。
```

> **git clone**

- 作用

从远程服务器克隆项目到本地

- 代码

```
[root@localhost learngit]# git clone https://github.com/980466813/gitkills.git
正克隆到 'gitkills'...
remote: Enumerating objects: 6, done.
remote: Counting objects: 100% (6/6), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 6 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (6/6), done.
[root@localhost learngit]# ls
gitkills  readme.txt  test.txt
[root@localhost learngit]# cd gitkills/
[root@localhost gitkills]# ls
NewText.txt  README.md

```

> **分支操作**

- 分支作用

在不影响master分支的前提下，完成其他的任务，或者在修复master分支上的BUG与团队开发模块式用处极大

- 创建分支

```
[root@localhost learngit]# git checkout -b dev
切换到一个新分支 'dev'

// 相当于使用以下两条语句
[root@localhost learngit]# git branch dev   // 创建当前分支
[root@localhost learngit]# git checkout dev // 切换当前分支
```

- 查看当前分支
```
[root@localhost learngit]# git branch
* dev
  master
```

- 合并分支
```
// 合并分支前，分支上的操作是不会影响master分支
[root@localhost learngit]# git add readme.txt
[root@localhost learngit]# git commit -m "分支上的操作"
[dev 13d5b65] 分支上的操作
 1 file changed, 21 insertions(+)
[root@localhost learngit]# git checkout master
切换到分支 'master'
您的分支领先 'origin/master' 共 1 个提交。
  （使用 "git push" 来发布您的本地提交）
[root@localhost learngit]# vim readme.txt 
[root@localhost learngit]# git merge dev
更新 c7a82b4..13d5b65
Fast-forward
 readme.txt | 21 +++++++++++++++++++++
 1 file changed, 21 insertions(+)

```

- 删除分支
```
[root@localhost learngit]# git branch -d dev
已删除分支 dev（曾为 13d5b65）。
[root@localhost learngit]# git branch
* master
```

