# 一些常见的工作流程

## 什么？已发布的产品里有BUG？
情况喵述：已经发布的产品分支上（通常是master分支）发现有bug需要紧急修复并发布！

1. 检查当前的工作状态，若当前有尚未提交的修改，则缓存当前的工作状态，以免在这些修改在切换分支后覆盖到所切换的分支上。在当前的工作分支上运行`git stash -a`将当前的工作状态暂时保存起来。保证当前的工作环境的‘干净’。
2. 切换到需要解决bug的分支，例如用于正式发布产品的分支，一般为master分支。`git checkout master`。
3. 新建bug修复分支，`git checkout -b issue-001`。
4. 修复bug并测试通过。
5. 将修复合并到master分支上。在一般情况下，master分支在bug修复期间没有被更新过的话，只要切换到master分支并将bug修复的分支合并即可，运行`git checkout master` `git merge issue-001`。若在bug修复期间，master有重新发布了一个新的版本。且在该版本上没有修复该bug，这时依旧可以切换到master分支上并将issue-001分支上的修改合并进来。或者用rebase命令将issue-001上的修改重新应用到master分支的最新版本上，在测试通过后，切换到master分支上与issue-001合并，操作如下，`git rebase master` `git checkout master` `git merge issue-001`。rebase的好处是可以使master分支相对线性。使master上面只有来自dev分支的合并。
6. 发布完毕。现在可以删除issue-001分支。
