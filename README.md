## Git

### 原理

![](images/git-command.jpg)



### 1. git推送

![](images/1352126739_7909.jpg)

工作流程：

- **工作区**：就是你在电脑里能看到的目录。

- **暂存区**：英文叫 stage 或 index。一般存放在 **.git** 目录下的 index 文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。

- **本地版本库**：工作区有一个隐藏目录 **.git**，这个不算工作区，而是 Git 的版本库。

  

<br/>

git add .  #会创建一个.git文件夹，用于版本跟踪记录，**config记录远程跟踪**

git status | git diff

git  commit  - m  "first commit"

<br/>

git config --list

git config -e  #编辑当前项目信息配置

`git config可搭配--global配置全局/默认信息`

git config --global  --list 相关配置信息保存在c盘用户目录下的.gitconfig里面


<br/>

**关联远程**

git remote -v 

git remote add origin  https://gitee.com/jxnuxyh/git-study.git

git push -u origin master  #推送

**git push origin <branch-name>**



若失败：git pull origin master --allow-unrelated-histories


<br/>

**修改**

1.  直接修改.git目录下的config配置文件

2.  git  remote  set-url --add / --delete origin git@gitee.com:jxnuxyh/git-study.git

    <br/>

### 2. git clone下载

相当于svn的checkout

git clone https://gitee.com/jxnuxyh/git-study.git

<br/>

### 3. git pull同步

提交代码前需要先同步

git pull  更新远程代码到本地库

更新操作： `git pull`

**若失败**： 原因是没有指定本地`dev`分支与远程`origin/dev`分支的链接

1）将远程主机 origin 的 master 分支拉取过来，与本地的 brantest 分支合并: `git pull origin master:brantest`

2）根据提示，设置`dev`和`origin/dev`的链接：

​	**git branch --set-upstream-to=origin/dev dev**
​	或
​	**git branch --set-upstream branch-name origin/branch-name**

<br/>

### 4. git branch

执行 **git init** 的时候，默认情况下 Git 就会为你创建 **master** 分支

查看所有分支：**git branch**

创建分支：**git branch  [branchName]  /   git checkout  -b  [branchName]**

切换分支：**git checkout [branchName] / git switch [branchName]**

删除分支：**git branch -d  [branchName]**

合并分支：**git merge**

用`git log --graph`命令可以看到分支合并图

 `git log --graph --pretty=oneline --abbrev-commit`

<br/>


### 5. git  reset

HEAD指向的版本就是当前版本，使用命令`git reset --hard commit_id`

穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。

要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本


<br/>

### 6. gitignore

Java.gitignore:https://github.com/github/gitignore

```xml
# Compiled class file
*.class

# Log file
*.log

# BlueJ files
*.ctxt

# Mobile Tools for Java (J2ME)
.mtj.tmp/

# Package Files #
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar
*.iml

# virtual machine crash logs, see http://www.java.com/en/download/help/error_hotspot.xml
hs_err_pid*

.classpath
.project
.settings
target
.gitignore
.idea
```

全局配置，一劳永益，在~/.gitconfig 文件中引入上述文件, 这样每个项目都可以不创
建.gitignore忽略文件

```xml
 [core] 
	excludesfile = C:/Users/24667/Java.gitignore
```

如果在已push过的项目，想要更改.gitignore，需要执行清除缓存操作
```xml
> git rm -r --cached .
> git add .
> git ...
```