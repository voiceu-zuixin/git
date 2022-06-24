# 安装 git

# 链接到 github，设置 ssh 等

# 基本流程

git init：新建一个 git 库
git status：查看目前状态
git add <文件名>：添加文件从工作区到暂存区
git commit -m “提示信息”：从暂存区提交到代码仓库
git log：查看提交 commit 的信息
git remote add origin https://github.com/try-git/try_git.git : 添加远程指针
git push -u origin master：将本地的 master 分支推送到远程 origin 主机，-u 参数表示记住对应关系，下次可以直接 git push 推送。
git pull origin master：将远程主机 origin 的代码取回本地，与本地的 master 分支合并
git diff HEAD：查看与上一次 commit 的区别

# 暂存区（index）

## 添加到暂存区

`git add <文件名>`：添加文件从工作区到暂存区，比如`git add 1.js 2.js`，中间用空格隔开

`git add .`：添加所有改变的文件从工作区到暂存区

`-u` 参数表示只添加暂存区已有的文件（包括删除操作），但不添加新增的文件。

- `git add -u`

比如暂存区有 1.js，此时我修改了 1.js 和 2.js，我可以用该命令将 1.js 放入暂存区，修改后的 2.js 无影响

## 撤销添加到暂存区的文件

`git reset HEAD -- .` 一次性撤销所有放入暂存区的文件
`git reset HEAD -- filename` 撤销指定目标文件
`git rm --cached filename` 撤销指定目标文件，比如`git rm --cached 1.js 2.js`

# 代码仓库（Repository）

`git commit -m "提交信息"` 从暂存区提交到代码仓库
