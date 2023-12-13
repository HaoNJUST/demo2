# Git使用

**git的文件状态**

```
工作区：已修改
暂存区：已暂存
Git目录：已提交
```

**快捷键**：

```
清屏：Ctrl+L   clear+E
```

**初始化本地库**

```
在自己的本地项目中，右击空白处打开git的命令行窗口，然后输入：此操作相当于给git操作这个目录下文件的权限
git init
```

**本地库内的查看、提交**

```
git status	查看本地库状态
git add hello.txt 提交到缓存区
git commit -m "第一次提交" hello.txt  将文件提交到本地库,-m是为了输入日志信息

git reflog //ref+log查看日志信息，显示如下：f45792e是版本号
f45792e (HEAD -> master) HEAD@{0}: commit (initial): 第一次提交

git log //查看更详细的日志信息
```

**取消暂存文件**

```
git r
```

**穿梭到历史版本**（在分支内部）：git的本地项目中，只会存一个版本，低层通过指针实现，可以在各个版本之间切换。

```
先查看所有版本日志
git reflog
复制要穿梭的版本号
git reset --hard 版本号
此时可以用cat 文件名查看当前版本的内容
```

**创建一个分支：**

```
当前仓库中存在的分支,并且会在当前使用的分支前面标记一个星号（*)
git branch
查看远程仓库中的分支:
git branch -r
查看所有分支，并显示当前在哪个分支
git branch -v
创建分支:增加一个热修分支
git branch hot-fix
再次查看发现多了一个分支
切换到其他分支
git checkout 分支名
git checkout hot-fix
然后就可以在这个分支上，修改之前的文件，并添加到缓存区，提交到本地库
```

**合并分支：**

```
git merge 分支名 ：将指定分支合并到当前分支
比如当前指向的是masetr分支，然后使用命令 :
git merge hot-fix
合并之后，两个分支就是一模一样的了
```

 **合并冲突：**当在一个分支（hot-fix)修改某个文件之后，添加到缓存区、提交到本地库；然后再另一个分支也对文件进行了修改（而且这两处修改不一样），然后也添加到缓存区、提交到本地库；这时想把这两个库合并就会出现冲突，需要自己打开这个文件，手动决定最终修改的样子

```
手动修改之后，依然需要添加到缓存区、提交到本地库，这时候注意，提交到本地库时，命令后面不要再添加文件名；
git commit -m "merge test" 
而不是：
git commit -m "merge test"  hello.txt
```

**创建远程仓库**：

* push 推送：将本地库的代码推送到远程库中；
* clone 克隆：将远程库的代码完整地下载到自己的本地库中；
* pull  拉取：将远程库的代码（通常是更新过的），再拉取到自己的本地库，让自己的本地库也有最新版本；

```
在github上，创建的仓库会生成一个远程库链接；创建远程库别名：链接太长，给链接起别名；
git remote add 别名 链接
git remote add git-demo https://github.com/HaoNJUST/demo01.git
查看给远程库的（本地库）的别名；
git remote -v
```

**将本地仓库所有修改过的文件提交到暂存区，再提交到工作区**

```

git status
# 文件是红色

git add .
# 再次git status，文件变绿色

git commit -m '提交说明'
#
```

**将本地库项目推送到远程库中**：按分支推送，需要指定推送哪个分支

推送的最小单位是分支，把本地库的哪个分支推送过去

```
git push 目标远程库的别名（或者链接） 本地库的分支
git push git-demo master
```

**拉取远程库到本地**：远程库的代码被更新了，为了保证自己的本地库和远程库内容一致

```
git pull 目标远程库的别名（或者链接）  本地库的分支
```

**克隆远程库到本地**

```
git clone 远程库的链接
完成了三件事：拉取代码、初始化本地库、创建别名；别名默认是o
```

**一些问题**

```
git的默认分支是master，github仓库的默认分支是main，所以等于提交的时候，远程仓库上有了两个分支，而且还合并不了。
所以想要远程仓库只有一个main分支的话，就在git里新建一个叫main的分支，然后切换到这个分支，对文件进行提交到暂存区，工作区，然后推送到远程库。
```

上传.md文件

```
echo "# demo2" >> README.md
  git init
  git add README.md
  git commit -m "first commit"
  git branch -M main
  git remote add origin https://github.com/HaoNJUST/demo2.git
  git push -u origin main
  
  
  在 `git push -u origin main` 命令中，`-u` 参数的含义是将远程分支和本地分支关联起来，并设置远程分支为默认上游分支。

具体来说，`-u` 参数的作用是将本地的 `main` 分支推送到远程仓库的 `origin` 主机上，并且将本地的 `main` 分支与远程的 `main` 分支关联起来。这样一来，以后在使用 `git push` 命令时，Git 就会默认将本地的 `main` 分支推送到远程的 `main` 分支，而不需要再指定远程分支的名称。

因此，使用 `-u` 参数可以简化后续的推送操作，使得 Git 能够更智能地处理默认的推送行为。
```

```

```

