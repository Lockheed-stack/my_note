# Git

#### 1.版本控制

> 即版本迭代
>
> * 实现跨区域的多人协同开发
> * 追踪和记载一个或多个文件的历史记录
> * 组织和保护你的源代码和文档
> * 统计工作量
> * 并行开发，提高开发效率
> * 跟踪记录整个软件的开发过程
> * 减轻开发人员的负担，节省时间

##### 版本控制分类

> 本地版本控制

![image-20211109150306963](https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/image-20211109150306963.png)

> 集中版本控制（代表：SVN）

![image-20211109150641349](https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/image-20211109150641349.png)

> 分布式版本控制（代表：Git）

![image-20211109150909621](https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/image-20211109150909621.png)

> Git与SVN最主要的区别

<img src="https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/image-20211109151317797.png" alt="image-20211109151317797"  />



#### 2.Git基本理论（核心）

> 工作区域

Git本地有三个工作区域：

1. 工作目录（working directory）

2. 暂存区（stage/index）

3. 资源库（repository or Git directory）。


如果加上远程的git仓库（remote directory）就可以分为四个工作区域。文件在这四个区域之间的转换关系如下：

![image-20211109160634273](https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/image-20211109160634273.png)



本地的三个区域确切的说应该是git仓库中HEAD指向的版本：

![image-20211109161204664](https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/image-20211109161204664.png)



> 工作流程

1. 在工作目录中添加、修改文件。
2. 将需要进行版本管理的文件放入暂存区域。（git add）
3. 将暂存区域的文件提交到git仓库。

git管理的文件有三种状态：已修改（modified）、已暂存（staged）、已提交（committed）。





#### 3.Git项目搭建



![image-20211109161959055](https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/image-20211109161959055.png)

> 本地仓库搭建

```bash
# 在当前目录新建一个Git代码库
$ git init 
```

执行后在项目目录会多出一个 ".git"目录。



```bash
# 克隆远程仓库
$ git clone [url]
```

执行后将远程服务器上的仓库完全镜像一份至本地。





#### 4.Git文件操作

> 文件的4中状态

![The lifecycle of the status of your files](https://git-scm.com/book/en/v2/images/lifecycle.png)

* **Untracked**：未跟踪。此文件在文件夹中，但没有加入到git库中，不参与版本控制。可通过==git add==将状态变为==Staged==。
* **Unmodified**：文件已入库，未修改。这类型文件有两种去处：
  1. 如果它被修改，则变为==Modified==。
  2. 如果使用==git rm==移出版本库，则变为==Untracked==文件。
* **Modified**：文件已修改，但仅仅是修改，还没进行其他操作。这类型文件有两种去处：
  1. 通过==git add==变为==Staged==暂存状态
  2. 使用==git checkout==，从库中取出文件，覆盖当前修改，返回到==Unmodified==状态。

* **Staged**：暂存状态。有两种操作：
  1. 执行==git commit==将修改同步到库中，此时库中文件和本地文件变为一致，文件为==Unmodified==状态。
  2. 执行==git reset HEAD filename==取消暂存，文件变为==Modified==状态。



> 查看文件状态

```bash
# 查看指定文件状态
$ git status [filename]

# 查看所有文件状态
$ git status

# 提交暂存区中文件到本地仓库
$ git commit -m # -m 表示附加消息
```



> 忽略文件

不想将某些文件纳入版本控制中，如数据库文件、临时文件等。在主目录下建立 ".gitignore" 文件，规则如下：

1. 忽略文件中的空行或以"#"开始的行将被忽略。(就是注释)
2. 可使用Linux通配符。“ * ”表示任意字符；“ ？”表示一个字符；"[abc]"方括号代表可选字符范围；"{string1,string2,...}"大括号代表可选字符串等。
3. 如果名称**最前面**有一个 ” ！“，表示例外规则，将不被忽略。
4. 如果名称**最前面**是一个路径分隔符 ” / “，表示要忽略的文件在此目录下，而子目录中的文件不忽略。
5. 如果名称**最后面**是一个路径分隔符 ” / “，表示要忽略的是此目录下该名称的子目录，而非文件。

```bash
*.txt		#忽略所有 .txt 结尾的文件
!lib.txt	#但lib.txt除外
/temp		#仅忽略项目根目录下的文件，不包括其他目录temp
build/		#忽略build/目录下所有文件
doc/*.txt	#忽略 doc/*.txt ，但不包括doc/server/arch.txt
```







#### 5.Git分支

![image-20211109214149704](https://raw.githubusercontent.com/Lockheed-stack/typora_image/main/images/image-20211109214149704.png)

```bash
# 列出所有本地分支
git branch

# 列出所有远程分支
git branch -r

# 新建一个分支，但依然停留在当前分支
git branch [branch-name]

# 新建一个分支，并切换到该分支
git checkout -b [branch]

# 合并指定分支到当前分支
git merge [branch]

# 删除分支
git branch -d [branch-name]

# 删除远程分支
git push origin --delete [branch-name]
git branch -dr [remote/branch]
```

#### 6.Q&A
>Git中的origin到底是什么？

  Answer：就是远程仓库链接的别名，github默认叫origin，即使用命令 git remote add [\<option>]\<name>\<url> 时，对应的name，叫阿猫，阿狗都行。

<br></br>

>命令“git branch --set-upstream master origin/next”中的选项“--set-upstream”是什么意思？

Answer：在某些场合，Git会自动在本地分支与远程分支之间，建立一种追踪关系(tracking)。比如，在git clone的时候，所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的master分支自动”追踪”origin/master分支。

Git也允许手动建立追踪关系。上面命令指定master分支追踪origin/next分支。如果当前分支与远程分支存在追踪关系，git pull就可以省略远程分支名。

在使用命令“git pull origin"时，可能会出现"xxxx --set-upstream"的错误提示，就是在告诉你需要设置"追踪关系"，本地的当前分支无法自动与对应的origin主机”追踪分支”(remote-tracking branch)进行合并。
