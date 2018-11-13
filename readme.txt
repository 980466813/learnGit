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

- 代码
```
[root@localhost learngit]# git checkout --readme.txt

```



