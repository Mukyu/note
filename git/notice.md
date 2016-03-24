# 一些注意事项

## 我要切换分支了
在切换到其他分支前，必须确保当前的分支是clean的，若不是，则需要使用`git stash [-a|--all]`命令将当前的工作区(working)和暂存区(index)缓存起来，使当前分支为clean状态，否则会导致当前工作区的内容（包括未被add和未被commit的文件）覆盖将要切换的分支上。另外stash操作需要加上--all，否则将导致被ignore的文件无法被缓存，且会覆盖到将要切换的分支上！(这样子不吼吧？)若实在不小心忘记加的话，现在再切回去缓存，然后切回来，在切换后的分支上运行`git add -A`先将所有修改提交到暂存区(index)中，再运行`git reset --hard HEAD`恢复到当前分支最近commit的状态，也是我们所追求的状态。注意这样的操作会导致一个问题，若之前没有切回去那个切换分支之前的那个分支进行缓存的话会导致切换分支之前的那个分支所做的修改被全部删除！

稍微总结一下，切换分支时应注意的事情（如何保证干净的工作空间，使在切换分支时不会弄乱其他分支）
- 先运行`git stash -a`将当前的工作状态缓存起来，这句命令不仅会缓存被add或modified的文件还会将所有untracked和ignored的文件也缓存起来并从当前的工作环境中删去，是最“干净”的状态。
- 切换分支，并完成工作。
- 切回分支，运行`git stash apply`或其他导出stash的命令将刚才缓存的工作状态恢复。