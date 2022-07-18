## 一、什么是Git？

Git是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。



## 二、SVN与Git的区别

1.SVN是集中式版本控制系统，版本库是集中放在中央服务器的。

2.Git是分布式版本控制系统，那么它就没有中央服务器的。



## 三、Git的安装

安装下载地址:

```http
https://git-scm.com/download
```

在Windows上面安装好之后在任一文件夹下点击鼠标右键，会有如下图标：

![image-20220718004231803](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718004231803.png)

其中GUI为用户界面模式，Bash为命令行模式（常用），后面的使用基本上用的都是Bash模式。



## 四、工作区与暂存区的区别

**工作区：** 就是你在电脑上看到的目录，比如目录下test1.txt里的文件(.git隐藏目录版本库除外)。或者以后需要再新建的目录文件等等都属于工作区范畴。

**版本库(Repository)：** 工作区有一个隐藏目录.git,这个不属于工作区，这是版本库。其中版本库里面存了很多东西，其中最重要的就是stage(暂存区)，还有Git为我们自动创建了第一个分支master,以及指向master的一个指针HEAD。

使用Git提交文件到版本库有两步：

第一步：是使用 git add 把文件添加进去，实际上就是把文件添加到暂存区。

第二步：使用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支上。



## 五、Git基本操作



### 1、创建版本库

版本库又名仓库，英文名repository,你可以简单的理解一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改，删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻还可以将文件”还原”。



我在Windows系统桌面新建一个文件夹名为GitTest,然后进入此文件夹，点击鼠标右键然后选择Git Bash Here。选择此文件夹作为仓库。

![image-20220718004837687](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718004837687.png)



### 2、初始化

通过git init把这个目录变成git可以管理的仓库。

![image-20220718005340081](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718005340081.png)

这个时候在GitTest目录下生成了一个.git文件夹，代表初始化成功。



### 3、添加与提交

**举个小例子：**
在版本库GitTest目录下新建一个test1.txt 文档 内容如下：11111
**第一步**：使用命令 git add test1.txt添加到暂存区里面去。（git add . 提交全部）
**第二步**：用命令 git commit -m 文件提交到仓库。(注意 -m 后面是提交时添加的注释)
**第三步**：用命令 git status来查看是否还有文件未提交。
**第四步**：用命令 git pull 更新 （命令用于从远程获取代码并合并本地的版本）。
**第五步**：用命令 git push 推送到远程仓库。

![image-20220718005728873](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718005728873.png)



### 4、git diff

在test1.txt中添加内容22222，没有进行git add add/or git commit 操作,也就是说修改后的test1.txt 还在工作区。这时执行git status 它会提示modified：test1.txt，意思是说，有一个修改的文件未提交。可以用 cat test1.txt 查看文件内容 。**（重点）** 在未提交的情况下 git diff 可以查看修改了什么内容

![image-20220718010239451](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718010239451.png)

如果执行了git add，则如下图

![image-20220718010354472](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718010354472.png)



### 5、版本回退

查看历史记录 git log， **git log – –pretty=oneline**信息简化

![image-20220718010519230](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718010519230.png)

版本回退：
第一种：git reset --hard HEAD^ ，如果要回退到上上个版本只需把HEAD^ 改成 HEAD^^ 以此类推，如果回退到更久的版本则命令操作：git reset --hard HEAD~100
如下图展示：

![image-20220718011054061](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718011054061.png)

第二种：通过版本号回退 git reset --hard 版本号。获取版本号：git reflog
如下图所示：

![image-20220718011410837](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718011410837.png)



### 6、撤销修改与删除文件

**撤销：** git checkout – file 可以撤销某个文件在工作区的修改

![image-20220718012340406](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718012340406.png)

![image-20220718012351063](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718012351063.png)



**删除：** rm 文件，看下图：

![image-20220718012854171](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718012854171.png)



## 六、远程仓库

### 1、把本地仓库的内容推送到GitHub仓库

先在GitHub上新建一个项目

![image-20220718013330685](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718013330685.png)



![image-20220718013343168](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718013343168.png)





创建完成后会跳转到如下界面，复制图中标注的信息，待会要使用。

![image-20220718013417256](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718013417256.png)

在本地的GitTest仓库下运行命令：

```http
git remote add origin https://github.com/dslyz/GitTest.git
```

然后把本地库的内容推送到远程，使用 git push origin master命令，实际上是把当前分支master推送到远程 。

**注意：** 第一次推送git push -u origin master，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令：git push origin master。

![image-20220718013951013](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718013951013.png)

从现在起，只要**本地作了提交**，就可以通过如下命令：

```http
git push origin master
```

把本地master分支的最新修改推送到github上了，现在你就拥有了真正的分布式版本库了。



### 2、如何从远程仓库克隆？

执行克隆命令：

```http
git clone https://github.com/dslyz/GitTest.git
```

如果在git clone 项目时报错OpenSSL SSL_read: Connection was reset, errno 10054 ，
**解决方法是：**

```http
 git config --global http.sslVerify “false”
```



## 七、创建与分支合并

创建于合并分支命令如下：

```markdown
查看分支：git branch

创建分支：git branch name

切换分支：git checkout name

创建+切换分支：git checkout –b name

合并某分支到当前分支：git merge name

删除分支：git branch –d name
```



在版本回退里，我们已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。

首先，我们来创建dev分支，然后切换到dev分支上。如下操作：
git checkout 命令加上 –b 参数表示**创建并切换**，相当于如下:
git branch dev + git checkout dev = git checkout –b dev

**查看分支：** git branch

![image-20220718094054031](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718094054031.png)



**查看分支：** git branch

![image-20220718094110072](Git%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.assets/image-20220718094110072.png)



**分支策略：** 首先master主分支应该是非常稳定的，也就是用来发布新版本，一般情况下不允许在上面干活，干活一般情况下在新建的dev分支上干活，干完后，比如上要发布，或者说dev分支代码稳定后可以合并到主分支master上来。



## 八、Git基本常用命令总结

mkdir： XX (创建一个空目录 XX指目录名)

pwd： 显示当前目录的路径。

git init 把当前的目录变成可以管理的git仓库，生成隐藏.git文件。

git add XX 把xx文件添加到暂存区去。

git commit –m “XX” 提交文件 –m 后面的是注释。

git pull 命令用于从远程获取代码并合并本地的版本。

git status 查看仓库状态

git diff XX 查看XX文件修改了那些内容

git log 查看历史记录

git reset --hard HEAD^ 或者 git reset --hard HEAD~ 回退到上一个版本(如果想回退到100个版本，使用git reset –hard HEAD~100 )

cat XX 查看XX文件内容

git reflog 查看历史记录的版本号id

git checkout – XX 把XX文件在工作区的修改全部撤销。

git rm XX  删除XX文件

git remote add origin URL 关联一个远程库

git push –u (第一次要用-u 以后不需要) origin master 把当前master分支推送到远程库

git clone URL 从远程库中克隆

git checkout –b dev 创建dev分支 并切换到dev分支上

git branch 查看当前所有的分支

git checkout master 切换回master分支

git merge dev 在当前的分支上合并dev分支

git branch –d dev 删除dev分支

git branch name 创建分支

git stash 把当前的工作隐藏起来 等以后恢复现场后继续工作

git stash list 查看所有被隐藏的文件列表

git stash apply 恢复被隐藏的文件，但是内容不删除

git stash drop 删除文件

git stash pop 恢复文件的同时 也删除文件

git remote 查看远程库的信息

git remote –v 查看远程库的详细信息

git push origin master Git会把master分支推送到远程库对应的远程分支上