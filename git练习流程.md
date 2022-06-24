# 安装 git

# 链接到 github，设置 ssh 等

# 基本流程

git init：新建一个 git 库
git status：查看目前状态
git add <文件名>：添加文件从工作区到暂存区
git commit -m “提示信息”：从暂存区提交到代码仓库
git log：查看提交 commit 的信息，注意顺序，最新的提交记录在最前面
git remote add origin https://github.com/try-git/try_git.git : 添加远程指针
git push -u origin master：将本地的 master 分支推送到远程 origin 主机，-u 参数表示记住对应关系，下次可以直接 git push 推送。
git pull origin master：将远程主机 origin 的代码取回本地，与本地的 master 分支合并
git diff HEAD：查看与上一次 commit 的区别

# 暂存区（index）

## 添加到暂存区

`git add <filename>`：添加文件从工作区到暂存区，比如`git add 1.js 2.js`，中间用空格隔开

`git add .`：添加所有改变的文件从工作区到暂存区

`-u` 参数表示只添加暂存区已有的文件（包括删除操作），但不添加新增的文件。

- `git add -u`

比如暂存区有 1.js，此时我修改了 1.js 和 2.js，我可以用该命令将 1.js 放入暂存区，修改后的 2.js 无影响

## 撤销添加到暂存区的文件

`git reset HEAD -- .` 一次性撤销所有放入暂存区的文件，`git reset HEAD .`也行

`git reset HEAD -- <filename>` 撤销指定目标文件，`git reset HEAD <filename>`也行，所以不知道这个加上`--`有什么用

`git rm --cached <filename>` 撤销指定目标文件，比如`git rm --cached 1.js 2.js`，但是这里的`--`不能省

# 代码仓库（Repository）

`git commit -m "提交信息"` 从暂存区提交到代码仓库

`git commit <filename> -m "message"` 命令可以跳过暂存区，直接将文件从工作区提交到仓库区。

`git log` 可以查看所有 commit 记录

# 分支（branch）

分清 HEAD，master，main 等，比如 HEAD，在上方的撤销添加到暂存区的文件命令里面也提到过（`git reset HEAD -- <filename>`）， HEAD 是一个指针，指向当前的本地分支，比如此时是 master，那么通过`git log`可以看到 HEAD -> master

## 新建分支

`git branch` 列出所有本地分支

`git branch -a` 列出所有本地分支和远程分支

`git branch <branchName>` 新建分支

例如：我新建分支`develop`，但此时仍处于`master`，此时新建的分支，有着当前所有的 commit，并且 HEAD 指向 develop 和 master 分支，相当于有着三个指针指向当前的该节点，如果我此时继续在 master 上修改代码并提交，HEAD 会随着 master 不断的向后移动更新，但是 develop 则是会保持在这个地方，相当于备份。此时再去`git log`，就会发现，HEAD 只指向了 master。

## `git stash`

注意此时可以不用 commit 暂存区的更改到仓库，使用 `git stash` 命令，可以实现这一操作。并且此时甚至可以不用添加到暂存区，ide 中 git 都会跟踪那些改变了的文件，切回来的时候再用`git stash apply`就可以恢复了，

https://juejin.cn/post/7071780876501123085#heading-1

`git stash list` 列出 stash 的所有记录

`git stash clear` 删除 stash 的所有记录

`git stash pop` 应用最近一次的 stash，随后删除该记录

`git stash drop` 删除最近的一次 stash

## 新建分支并切换

`git checkout -b NewBranch <MyBranch>` 在新建 NewBranch 分支的同时切换到新分支，后面的 MyBranch 基于某个分支，可以是当前的分支，比如 master，并且如果是当前分支，则可以省略，可以直接写成`git checkout -b NewBranch`

## 删除分支

`git branch -d <分支名>`-d 参数用来删除一个分支，前提是该分支没有未合并的变动。

`git branch -D <分支名>` 强制删除一个分支，不管有没有未合并变化。

## 分支改名

`git branch -m <newName>` 为当前分支改名

`git branch -m <target_branch> <newName>` 为指定分支改名

注意改名时，大小写不区分，所以用上面的命令要把 NewBranch 改成 newBranch，是不行的，因为在命令中，NewBranch 就是 newBranch，甚至可以是 newbranch ，要强制改名，使用下面的命令 `-M`

`git branch -M <target_branch> <newName>` 为指定分支强制改名

分支改名的思路还可以是，在当前节点创建一个新分支，并切换到该新分支，删除旧分支，新分支的名称就是想要改的名字

`git checkout -b feature NewBranch` 基于 NewBranch 新建一个 feature 分支，并切换到该新分支

`git branch -d NewBranch` 删除 NewBranch 分支

## 查看 merge 情况

`git branch --merged` Shows branches that are all merged in to your current branch

`git branch --no-merged` Shows branches that are not merged in to your current branch

