# GitLearn

> 用来进行一些git常用命令的练习

#### 1.git仓库初始化
```git
 git init [directory]
 ```
 > 如果[directory]存在会将该目录初始化为一个仓库，如果不存在那就是将当前目录初始化为一个仓库
 
 #### 2.git将文件添加到缓存区
 ```git
 git add [file1 file2...]
 git add .
 ```
 > git add将编辑过的文件添加到缓存区，可以一次添加多个文件，如果是.的话意思是将当前目录下所有东西添加到缓存区
 > 这里扩充两个命令 git diff和git status
 > git diff用来展示工作区的文件和缓存区文件的差异
 > git status里面用来展示当前整个仓库的一些信息
 
 #### 3.git将缓存区内容提交
 ```git
 git commit -m '提交内容修饰'
 ```
 > 将第2步中add到缓存区的内容提交，-m用来指定本次提交的描述
 
 #### 4.git查看过往版本
```git
git log
commit eb7a7555af1d9c2b74853f63b176e0c2c78a1d50 (HEAD -> master, github_origin/master)
Author: Flandrelu <77132942+Flandrelu@users.noreply.github.com>
Date:   Tue Jul 26 17:50:23 2022 +0800

    Create README.md

commit bc5ed84aad11a2aff88897fa632a7669ce27eb71 (github_origin/dev, dev)
Author: Flandrelu <17862979279@163.com>
Date:   Tue Jul 26 17:08:06 2022 +0800

    pythontest-version1
```

#### 5.git查看过往操作
```git
git reflog
```
```text
┌─[momo@BJ204128] - [~/PycharmProjects/pythontest] - [2022-07-26 06:07:26]
└─[0] <git:(master eb7a755) > vim reflog.txt
┌─[momo@BJ204128] - [~/PycharmProjects/pythontest] - [2022-07-26 06:11:54]
└─[0] <git:(master eb7a755✈) > git add reflog.txt
┌─[momo@BJ204128] - [~/PycharmProjects/pythontest] - [2022-07-26 06:11:59]
└─[0] <git:(master eb7a755+) > git commit -m 'touch reflog.txt'
[master 04f25e8] touch reflog.txt
 1 file changed, 1 insertion(+)
 create mode 100644 reflog.txt
┌─[momo@BJ204128] - [~/PycharmProjects/pythontest] - [2022-07-26 06:12:39]
└─[0] <git:(master 04f25e8) > git reflog
04f25e8 (HEAD -> master) HEAD@{0}: commit: touch reflog.txt
eb7a755 (github_origin/master) HEAD@{1}: pull github_origin master: Fast-forward
```
#### 6.git版本回退[已经commit]
```git
git reset --hard [commit id]
```
> 我地4步加完文件之后我发现并不需要，除了删除文件这种方式之外，我还可以回退到添加这个版本之前
```git
git reset --hard eb7a755
HEAD 现在位于 eb7a755 Create README.md
```
> 上面--hard后面的eb7a755可以根据reflog进行查看

#### 7.git版本回退[尚未commit]
> 其实这里容易和第六步混淆，这里说版本回退其实是不太准确的，因为并没有commit也就没有形成新的版本,目前没有想到什么比较好的词暂且使用回退吧
```git
git restore --staged [file]
```
> 将缓存区的文件扔回工作区
```git
git restore [file]
```
> 如果已经将一个文件添加到了缓存区，但是尚未提交，这时候又在工作区对这个文件做了修改，如果想丢弃工作区的这一部分修改，继续使用缓存区的文件内容，可以使用restore,如果相连缓存里面的文件内容都不要了，那么可以使用restore --staged

#### 8.git分支
```git
git branch [branch name] && git switch [branch name]
```
> 当然创建分支的命令不唯一，因为我脑子不太好使所以我喜欢用简单的所以我就用了
> 如果想要合并一个分支到另一个分支需要用下面的命令
> 这里为了直观我直接使用实际的分支示例：将bugfix分支合并到dev，当然这个合并的前提就是bugfix要比dev新
```git
# 首先进入到dev分支下面
git switch dev
# 进行合并操作
git merge bugfix
更新 bc5ed84..82f120b
Fast-forward
 README.md | 83 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 83 insertions(+)
 create mode 100644 README.md
```

> 这里需要注意一点就是
