# git 技巧

## 查看本机的ssh秘钥

### 基本语法

ls -al ~/.ssh 检查目录列表是否存在已有的公共ssh秘钥

cd ~/.ssh 转换到该目录下

ls 查看目录下的文件

cat id_rsa.pub 查看本机的公共秘钥

# git 基本命令

## git 本地结构

```shell
#工作区 -> 暂存区
git add  单个文件  |  git  add  文件 文件  | git  add  正则表达式
#暂存区 -> 本地库
git commit  格式同add相同
#本地库 --> 远端
git push    #如果本地库主分支比远端文件少，需要git pull,之后需要 python manage.py migrate 一下，然后接着push就可以
#远端 -->本地库
git pull 
```

### git log 显示日志

```shell
# git log --oneline   只显示主题行
# git shortlog  显示作者和主题行
# 显示提交的改动
git log -p
```

## git restore 撤销

```shell
#文件在暂存区
git restore --staged <file> 撤销git add 操作，文件会在工作区出现，并且所作修改不被撤销
#文件在工作区
git restore <file> 撤销文件的修改
```

## git  stash

将本地没提交的内容(`git commit`的内容不会被缓存 但`git add`的内容会被缓存)进行缓存并从当前分支移除，缓存的[数据结构](https://so.csdn.net/so/search?q=数据结构&spm=1001.2101.3001.7020)为堆栈，先进后出

```shell
#将本地没提交内容缓存，并从当前分支移除
git stash  
#查看git stash 堆栈
git stash list
#查看stash的改动
git stash show [stash]
#查看stash的具体改动
git stash show -p [stash]
#基于进度创建分支
git stash branch <branch_name> <stash>
#删除一个存储的进度。默认为删除最新的进度
git stash drop [<stash>]
#删除所有存储的进度
git stash clear
#将堆栈中最新的内容pop出来应用到当前的分支，并从列表中删除
git stash pop
#将堆栈中指定的stash pop 出来到当前的分支，并从列表中删除
git stash pop <stash>
#除了不删除恢复的进度外，其他跟git stash pop 相同
git stash apply <stash>
```

## git reset  

当代码提交comit后会生成记录，如果需要回退代码，可以使用git reset

```shell
#本地库回退到目的代码，暂存区和工作区不变
git reset --soft HEAD~1
#本地库和暂存区回退到目的代码，工作区不变
git reset --mixed HEAD~1
#本地库和暂存区和工作区都回退到目的代码
git reset --hard HEAD~1
```

## git rm

git 用来删除文件的命令

```shell
#把工作区的文件删除，并将删除指令上传到暂存区
git rm  <文件名>
#撤回已暂存的删除命令
git reset HEAD 文件名 
git checkout 文件名
#将删除指令提交，删除本地库的文件
git commit -m ""
```

## git mv

git文件重命名

```shell
#将git 文件 重命名
git mv file_from file_to
# 例如
git mv test1.txt test.txt
```

# git 分支

```shell
#创建并切换分支
git checkout -b 分支名称
#查看分支
git branch
#切换分支
git branch 分支名称
#删除分支
git branch -d 分支名称
```

# git cherry-pick  

### 作用

- 将指定的提交(commit)应用于其他分支。

### 基本作用

-  git  cherry-pick  <commitHash>
-  git   cherry-pick   A..B  提交A到B的commit号，不包括A
- git  cherry-pick  A^..B  提交包括A到B的commit号





