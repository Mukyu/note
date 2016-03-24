# 一些命令的理解与使用
 在下文中工作区用workspace表示，暂存区用index表示。

## 常见的几个命令

- `$ git checout -- <file>...` 撤销文件在workspace上但还没有放进index里的修改，也可以理解为把指定文件变成在当前index上的状态。

- `$ git reset HEAD <file>...` 撤销文件在index上的暂存。

- `$ git reset HEAD` 撤销所有文件在index上的暂存。

- `$ git reset HEAD~n` 把版本回退到前n个版本。

- `$ git diff` 查看工作区与暂存区之间的差异。（我的哪些操作还没有add进暂存区？）

- `$ git diff --staged` 查看暂存区与上次提交之后的差异。（自上次commit以来，我改了哪些东西并把放进暂存区了？）

- `$ git diff HEAD` 或 `git diff master` 查看工作区与上一次commit之后的差异。（上一次commit之后，我在工作区改了哪些内容？）

- `$ git diff <branch-a>...<branch-b>` 该命令会显示自b分支与a分支的共同祖先起，b分支中的工作。

- `$ git merge <branch-name>` 将指定的分支把自上一次共同祖先后所做的修改（也就是commit）重新应用到当前的分支（若发现两个分支都同时修改了同一个文件，git会在冲突的文件里做标记，并创建一个临时的分支去指向，直到用户解决了冲突并commit后，才会继续后面的工作），并以重新应用后的分支创建一次新的commit让当前分支指向它。例如在master分支上运行 `git merge topic`的效果：

```
  A---B---C topic         merge        A---B---C topic
 /                      --------->    /         \
D---E---F---G master                 D---E---F---G---H master
```

- `$ git remote add <remote-name> <remote-url>` 添加一个远程库。

- `$ git push <remote> <local-branch>:<remote-branch>` 把本地分支推送到远程分支上。

- `$ git checkout -b <new-branch> <remote>/<remote-branch>` 可以创建以一个远程为起点的本地分支。


## 我要...，该怎么做？

- 我要撤销`git add`操作，且不能影响到workspace的文件：
  - `$ git reset HEAD <file>...` 撤销指定文件的暂存。
  - 或者`$ git reset HEAD` 撤销所有文件的暂存。

- 我要撤销文件在workspace上的修改，恢复到上一次`git add`操作后的状态：
  - `$ git checout -- <file>...` 撤销文件在workspace上但还没有放进index里的修改，也可以理解为把指定文件变成在当前index上的状态。

- 我要撤销文件在workspace上的修改，恢复到上一次`git commit`后的状态：
  - 先用`$ git reset HEAD <file>...`撤销文件在index上的暂存。
  - 再运行`$ git checkout -- <file>...`撤销文件在workspace但还没有放进index里的操作。
  - 或者`$ git reset --hard HEAD` 撤销所有在workspace上的操作，以及他们在index上的暂存。