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

![image-20211109150306963](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20211109150306963.png)

> 集中版本控制（代表：SVN）

![image-20211109150641349](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20211109150641349.png)

> 分布式版本控制（代表：Git）

![image-20211109150909621](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20211109150909621.png)

> Git与SVN最主要的区别

<img src="https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20211109151317797.png" alt="image-20211109151317797"  />



#### 2.Git基本理论（核心）

> 工作区域

Git本地有三个工作区域：

1. 工作目录（working directory）

2. 暂存区（stage/index）

3. 资源库（repository or Git directory）。


如果加上远程的git仓库（remote directory）就可以分为四个工作区域。文件在这四个区域之间的转换关系如下：

![image-20211109160634273](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20211109160634273.png)



本地的三个区域确切的说应该是git仓库中HEAD指向的版本：

![image-20211109161204664](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20211109161204664.png)



> 工作流程

1. 在工作目录中添加、修改文件。
2. 将需要进行版本管理的文件放入暂存区域。（git add）
3. 将暂存区域的文件提交到git仓库。

git管理的文件有三种状态：已修改（modified）、已暂存（staged）、已提交（committed）。





#### 3.Git项目搭建



![image-20211109161959055](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20211109161959055.png)

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

![image-20211109214149704](https://cdn.jsdelivr.net/gh/Lockheed-stack/typora_image@main/images/image-20211109214149704.png)

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

<br></br>

>git pull 与 git pull --rebase的联系、区别?

Answer: 这两个操作的区别
git pull = git fetch + git merge
git pull --rebase = git fetch + git rebase
rebase翻译为“变基”*(这翻译有点意思...)*。

具体示例:
* 假设你现在基于远程分支”origin“，创建一个叫”mywork“的分支。
```bash
$ git checkout -b mywork origin
```
结果如下所示 -
![](http://www.yiibai.com/uploads/images/201707/1307/842100748_44775.png)
* 现在我们在这个分支(mywork)做一些修改，然后生成两个提交(commit).
```bash
$ vi file.txt
$ git commit
$ vi otherfile.txt
$ git commit
... ...
```
但是与此同时，有些人也在”origin“分支上做了一些修改并且做了提交了，这就意味着”origin“和”mywork“这两个分支各自”前进”了，它们之间”分叉”了。
![](http://www.yiibai.com/uploads/images/201707/1307/810100749_17109.png)
此时如果直接提交，会发生冲突。解决方法如下： 
  1. **git merge**
  用`pull`命令把`origin`分支上的修改拉下来并且和你的修改合并； 结果看起来就像一个新的”合并的提交”(merge commit)。但这样会形成图中的菱形，让人很困惑。
  ![](http://www.yiibai.com/uploads/images/201707/1307/350100750_71786.png)
  2. **git rebase**
  如果你想让`mywork`分支历史看起来像没有经过任何合并一样，也可以用 `git rebase`，如下所示:
  ```bash
  $ git checkout mywork
  $ git rebase origin
  ```
  这些命令会把你的`mywork`分支里的每个提交(commit)取消掉，并且把它们临时 保存为补丁(patch)(这些补丁放到`.git/rebase`目录中),然后把`mywork`分支更新 到最新的`origin`分支，最后把保存的这些补丁应用到`mywork`分支上。
  ![](http://www.yiibai.com/uploads/images/201707/1307/845100751_76810.png)
  当`mywork`分支更新之后，它会指向这些新创建的提交(commit),而那些老的提交会被丢弃。 如果运行垃圾收集命令(pruning garbage collection), 这些被丢弃的提交就会删除.
  ![](http://www.yiibai.com/uploads/images/201707/1307/141100752_31232.png)



==稍微深入==
**多主题分支变基(git rebase --onto)**
只要你一直使用Git,早晚会遇到这样一种情况：从主干切出了某一分支issue1，进行了一些提交后，有另一个需求，我们在issue1分支切出新分支issue2，进行了提交，这期间其他成员对master主干分支进行了更新，结构图如下：
![](https://pic2.zhimg.com/80/v2-d1445858b3f221eeb17d18e528e4e275_720w.png)
现在，issue2分支开发完，我们需要将其变更并入主线，但是issue1分支的变更还是继续保持独立，如果直接进行简单变基，cec214,d4eb57也将被并入主线，这不是我们想要的结果，我们只希望将issue2分支上进行的变更和提交并入主线，即5f3776,ac5c08，这时需要使用git rebase --onto指令：
```bash
$ git rebase --onto master issue1 issue2
```

![](https://pic1.zhimg.com/80/v2-cdd1a9d516302f827a42f6d28b887cf8_720w.png)
可以看出，执行--onto变基后，在主线上复制了issue2分支的所有提交对象，此处所谓复制，是在主线创建新提交对象，而其提交内容及备注复制自issue2分支的提交对象
![](https://pic3.zhimg.com/80/v2-69e4a1e094a3cb553043b2a59718657a_720w.png)

上例使用了git rebase --onto 变基目标分支master 变基过渡分支issue1 变基当前分支issue2指令，此指令解释如下：

* 变基当前分支，即当前执行变基的分支issue2；
* 变基目标分支，即当前执行变基分支的变基指向分支master；
* 变基过渡分支，即当前执行变基分支过滤提交对象的目标分支issue1（当前分支从过渡分支切出）；
* 取出issue2分支上进行的所有提交对象，以补丁（patches）形式在主线master分支上重新应用，创建新提交对象，然后将分支指针移动到最后一个新创建的提交对象。

==最后注意一个原则==: 永远不要对已经推到主干分支服务器或者团队其他成员的提交进行变基，我们选择变基还是合并的范围应该在自己当前工作范围内。