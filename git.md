# Git

## Git是什么

Git是一个`分布式版本控制`软件

`分布式版本控制`：是一种版本控制的方式，它允许软件开发者可以共同参与一个软件开发专案，但是不必在共同的网络系统下工作。不需要服务器端软件就可以运作版本控制。

## 数据结构

![](.gitbook/assets/git_operations.svg.png)  
Git中的数据流和存储级别

## Git的三种状态

Git有三种状态：

`已修改`（modified）：修改了文件，但还没保存到本地数据库中  
`已暂存`（staged）：对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。  
`已提交`（committed）：数据已经保存到本地数据库中  
![](.gitbook/assets/git-de-san-ge-gong-zuo-qu-yu.png)

Git的工作流程：  
1. 在工作目录中修改文件  
2. 暂存文件，将文件的快照放入暂存区域  
3. 提交更新，找到暂存区域的文件，将快照永久性存储到Git仓库目录

## Git文件的生命周期

工作目录下的文件状态：已跟踪、未跟踪。已跟踪的文件就是那些被纳入了版本控制的文件，工作目录中除已跟踪文件以外的所有其它文件都属于未跟踪文件。

Git文件的生命周期如下：  
![](.gitbook/assets/git-wen-jian-de-sheng-ming-zhou-qi.png)

## Git常用命令

**帮助文档**

```text
git help <command> #查看相关命令的帮助文档
```

**创建（Init）**

```text
git init //创建git仓库
```

**状态（Status）**

```text
git status //查看仓库状态（当前所在分支、内容更改和提交状态）
```

**添加（Adding）**  
添加更改到暂存区，此时改动还没有提交到仓库。  
提交到仓库之前，改动还可以从暂存区中移除，可以指定文件，也可以使用通配符\*指定一个类型的文件

```text
git add <file> #添加单个文件
git add '*.txt' #添加一类文件
git add . #添加所有文件
```

**提交（Committing）**

```text
git commit -m "修改日志" //提交修改，并添加修改日志
```

**历史（History）**

```text
git log #打印提交日志
```

**远程仓库（Remote Repositories）**

```text
git remote add origin 远程仓库地址
```

**推送（Pushing Remotely）**  
推送本地修改到远程仓库

```text
git push -u origin master
git push #自动推送到当前所在分支的远程分支
```

**拉取（Pulling Remotely）**  
检查远程仓库的修改并拉取

```text
git pull origin master
```

**差异（Differences）**  
检查更改

```text
git diff #查看尚未暂存的文件修改了哪些内容
git diff HEAD #
git diff --staged #
```

**重设Stage（Resetting the Stage）**  
把文件从Stage中移除

```text
git reset 文件名 #
```

**回滚（Undo）**

```text
git checkout -- <target> #将target文件的修改回滚到上次提交
```

**分支（Branches）**

```text
git branch clean_up #本地新建名为clean_up的分支
git branch #查看本地的所有分支
git checkout clean_up #切换到clean_up分支
git checkout master #切回到master分支
```

**删除（Removing All The Things）**  
git rm：移除本地文件并add文件的删除到Stage

```text
git rm <要删除的文件> #删除文件
```

**合并（Merge）**

```text
git merge clean_up #合并clean_up分支到master分支（在master分支下执行命令）
```

**清除（Clen）**

```text
git branch -d <branch name> #删除分支
```

**移除版本控制**

将文件或文件夹移除版本控制

```text
git rm -r -n --cached "bin/" #-n：加上这个参数，执行命令时，是不会删除任何文件，而是展示此命令要删除的bin/文件夹下的文件列表预览。
git rm -r --cached  "bin/" #最终执行命令. 删除bin/文件夹
git commit -m "remove bin folder all file out of control"    #提交
git push #提交到远程服务器
```

_参考文章：_

[独孤九剑 - git的设计思想揭秘](http://outofmemory.cn/wiki/git-design-secret)

