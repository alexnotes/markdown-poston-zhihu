[TOC]

> 在自学的过程中，发现太多教程又长又浅显，作者估计也没有掌握重点。学习应该是学习后实践，遵循「趁热打铁」的至理名言。我在写这篇教程中会大量使用各种实践例子，并且例子是来自实际工作过程中，你在工作中可以直接套用。

版本控制在我们的生活中无处不在，比如你的毕业论文，由于你写得不规范或是老师不满意，你的老师可能会让你改了又改，于是就会出现下面这种情况：

![点击查看源网页](./Git/src=http%3A%2F%2F5b0988e595225.cdn.sohucs.com%2Fimages%2F20200417%2F1e63ac0f4d8442cb8c9ab1cb73f510c4.jpeg&refer=http%3A%2F%2F5b0988e595225.cdn.sohucs-20230101184614972.jpeg)

我们手里的论文可能会经过多次版本迭代，最终我们会选取一个最好的版本作为最终提交的论文。使用版本控制不仅仅是为了去记录版本迭代历史，更是为了能够随时回退到之前的版本，实现时间回溯。同时，可能我们的论文是多个人一同完成，那么多个人如何去实现同步，如何保证每个人提交的更改都能够正常汇总，如何解决冲突，这些问题都需要一个优秀的版本控制系统来解决。

# 什么是Git？

我们开发的项目，也需要一个合适的版本控制系统来协助我们更好地管理版本迭代，而Git正是因此而诞生的（有关Git的历史，这里就不多做阐述了，感兴趣的小伙伴可以自行了解，是一位顶级大佬在一怒之下只花了2周时间用C语言开发的，之后的章节还会遇到他）

首先我们来了解一下Git是如何工作的：

![点击查看源网页](./Git/src=http%3A%2F%2Fimg2020.cnblogs.com%2Fblog%2F932856%2F202004%2F932856-20200423143251346-796113044.jpg&refer=http%3A%2F%2Fimg2020.cnblogs-20230101184614448.jpeg)

可以看到，它大致分为4个板块：

* 工作目录：存放我们正在写的代码（当我们新版本开发完成之后，就可以进行新版本的提交）
* 暂存区：暂时保存待提交的内容（新版本提交后会存放到本地仓库）
* 本地仓库：位于我们电脑上的一个版本控制仓库（存放的就是当前项目各个版本代码的增删信息）
* 远程仓库：位于服务器上的版本控制仓库（服务器上的版本信息可以由本地仓库推送上去，也可以从服务器抓取到本地仓库）

它是一个分布式的控制系统，因此一般情况下我们每个人的电脑上都有一个本地仓库，由大家共同向远程仓库去推送版本迭代信息。

通过这一系列操作，我们就可以实现每开发完一个版本或是一个功能，就提交一次新版本，这样，我们就可以很好地控制项目的版本迭代，想回退到之前的版本随时都可以回退，想查看新版本添加或是删除了什么代码，随时都可以查看。

# 安装Git

## 命令行软件（推荐）

Git官网去下载最新的安装包：https://git-scm.com/download/

安装完成后，需要设定用户名和邮箱来区分不同的用户：

```shell
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
# 查看是否配置成功
git config --list
```

## GUI 软件

1. [GitKraken Legendary Git Tools | GitKraken](https://www.gitkraken.com/) :+1:
2. SourceTree

## IDEA内集成的Git

IDEA开发几乎人人都用。命令行有些不直观，开发时会直接使用IDEA集成的Git进行版本控制。IDEA内部集成了git模块，它可以让我们的git版本管理图形化显示。

我通常只用来看看代码变更记录，其他操作都是代码。建议你也都是命令行操作，不要GUI操作。

# Git 常用命令

<!-- ![Git常用命令速查表](../Material/Image/Git常用命令速查表.png) -->

![image-20220901201751514](./Git/image-20220901201751514-2569971.png)

## 很好的资料

> 入门：[Git + GitHub 10分钟完全入门](https://www.bilibili.com/video/BV1KD4y1S7FL?spm_id_from=333.999.0.0&vd_source=23282fd525a72ec1a62d8dea0fc2a30b)
>
> 进阶：[Git + GitHub 10分钟完全入门 (进阶)](https://www.bilibili.com/video/BV1hA411v7qX?spm_id_from=333.999.0.0&vd_source=23282fd525a72ec1a62d8dea0fc2a30b)
>
> https://github.com/doggy8088/Learn-Git-in-30-days/blob/master/zh-cn/README.md

## git init：初始化仓库

我们可以将任意一个文件夹作为一个本地仓库，输入：

```shell
git init
```

输入后，会自动生成一个`.git`目录，注意这个目录是一个隐藏目录，而当前目录就是我们的工作目录。

创建成功后，我们可以查看一下当前的一个状态，输入：

```shell
git status
```

如果已经成功配置为Git本地仓库，那么输入后可以看到：

```shell
On branch master

No commits yet
```

这表示我们还没有向仓库中提交任何内容，也就是一个空的状态。

## git status：显示版本状态

![Screen Shot 2019-07-28 at 21.13.16](./Git/Screen Shot 2019-07-28 at 21.13.16-2569971.png)

## git add 和 git commit

git add：将变更的文件添加到Git中

git commit：提交变更

接着我们来看看，如何使用git来管理我们文档的版本，我们创建一个文本文档，随便写入一点内容，接着输入：

```shell
git status
```

我们会得到如下提示：

```shell
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	hello.txt

nothing added to commit but untracked files present (use "git add" to track)
```

其中Untracked files是未追踪文件的意思，也就是说，如果一个文件处于未追踪状态，那么git不会记录它的变化，始终将其当做一个新创建的文件，这里我们将其添加到暂存区，那么它会自动变为被追踪状态：

```shell
git add hello.txt #也可以 add . 一次性添加目录下所有的
```

再次查看当前状态：

```sh
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   hello.txt
```

现在文件名称的颜色变成了绿色，并且是处于Changes to be committed下面，因此，我们的hello.txt现在已经被添加到暂存区了。

接着我们来尝试将其提交到Git本地仓库中，注意需要输入提交的描述以便后续查看，比如你这次提交修改了或是新增了哪些内容：

```sh
git commit -m 'Hello World'
```

接着我们可以查看我们的提交记录：

```sh
git log
git log --graph
```

我们还可以查看最近一次变更的详细内容：

```sh
git show [也可以加上commit ID查看指定的提交记录]
```

再次查看当前状态，已经是清空状态了：

```sh
On branch master
nothing to commit, working tree clean
```

接着我们可以尝试修改一下我们的文本文档，由于当前文件已经是被追踪状态，那么git会去跟踪它的变化，如果说文件发生了修改，那么我们再次查看状态会得到下面的结果：

```sh
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   hello.txt
```

也就是说现在此文件是处于已修改状态，我们如果修改好了，就可以提交我们的新版本到本地仓库中：

```sh
git add .
git commit -m 'Modify Text'
```

接着我们来查询一下提交记录，可以看到一共有两次提交记录。

我们可以创建一个`.gitignore`文件来确定一个文件忽略列表，如果忽略列表中的文件存在且不是被追踪状态，那么git不会对其进行任何检查：

```yaml
# 这样就会匹配所有以txt结尾的文件
*.txt
# 虽然上面排除了所有txt结尾的文件，但是这个不排除
!666.txt
# 也可以直接指定一个文件夹，文件夹下的所有文件将全部忽略
test/
# 目录中所有以txt结尾的文件，但不包括子目录
xxx/*.txt
# 目录中所有以txt结尾的文件，包括子目录
xxx/**/*.txt
```

创建后，我们来看看是否还会检测到我们忽略的文件。

## git push

> 如果你还不知道远程仓库是什么，那跳过本章节。

命令是：

```shell
git push origin 本地分支:远端希望创建的分支
```

### git push -u

问题场景

​	一般将本地仓库推送到远程仓库的时候一般会使用 `git push` 命令。而作为新手，在网上看到一些教程有的会在 `git push` 的时候带上一个 `-u` 参数，而有的则没有。而推送的实际结果没有什么区别。就很好奇 `-u` 参数的作用到底是什么？

带上`-u` 参数其实就相当于记录了push到远端分支的默认值，这样当下次我们还想要继续push的这个远端分支的时候推送命令就可以简写成`git push`即可。

### git 里面的 origin 到底代表啥意思?

origin 用来代表“远程仓库”

>  [Git 里面的 origin 到底代表啥意思? - 知乎 (zhihu.com)](https://www.zhihu.com/question/27712995)

## git reset：回滚

当我们想要回退到过去的版本时，就可以执行回滚操作，执行后，可以将工作空间的内容恢复到指定提交的状态：

```sh
git reset --hard commitID
```

执行后，会直接重置为那个时候的状态。再次查看提交日志，我们发现之后的日志全部消失了。

那么要是现在我又想回去呢？我们可以通过查看所有分支的所有操作记录：

```sh
git reflog
```

这样就能找到之前的commitID，再次重置即可。

## 分支

分支就像我们树上的一个树枝一样，它们可能一开始的时候是同一根树枝，但是长着长着就开始分道扬镳了，这就是分支。我们的代码也是这样，可能一开始写基础功能的时候使用的是单个分支，但是某一天我们希望基于这些基础的功能，把我们的项目做成两个不同方向的项目，比如一个方向做Web网站，另一个方向做游戏服务端。

因此，我们可以在一个主干上分出N个分支，分别对多个分支的代码进行维护。

### 创建分支

我们可以通过以下命令来查看当前仓库中存在的分支：

```sh
git branch
```

我们发现，默认情况下是有一个master分支的，并且我们使用的也是master分支，一般情况下master分支都是正式版本的更新，而其他分支一般是开发中才频繁更新的。我们接着来基于当前分支创建一个新的分支：

```sh
git branch test
# 对应的删除分支是
git branch -d yyds
```

现在我们修改一下文件，提交，再查看一下提交日志：

```sh
git commit -a -m 'branch master commit'
```

通过添加-a来自动将未放入暂存区的已修改文件放入暂存区并执行提交操作。查看日志，我们发现现在我们的提交只生效于master分支，而新创建的分支并没有发生修改。

我们将分支切换到另一个分支：

```sh
git checkout test
```

我们会发现，文件变成了此分支创建的时的状态，也就是说，在不同分支下我们的文件内容是相互隔离的。

我们现在再来提交一次变更，会发现它只生效在yyds分支上。我们可以看看当前的分支状态：

```sh
git log --all --graph
```

### 合并分支

我们也可以将两个分支更新的内容最终合并到同一个分支上，我们先切换回主分支：

```sh
git checkout master
```

接着使用分支合并命令：

```sh
git merge test
```

会得到如下提示：

```
Auto-merging hello.txt
CONFLICT (content): Merge conflict in hello.txt
Automatic merge failed; fix conflicts and then commit the result.
```

在合并过程中产生了冲突，因为两个分支都对hello.txt文件进行了修改，那么现在要合并在一起，到底保留谁的hello文件呢？

我们可以查看一下是哪里发生了冲突：

```sh
git diff
```

因此，现在我们将master分支的版本回退到修改hello.txt之前或是直接修改为最新版本的内容，这样就不会有冲突了，接着再执行一次合并操作，现在两个分支成功合并为同一个分支。

### 变基分支

除了直接合并分支以外，我们还可以进行变基操作，它跟合并不同，合并是分支回到主干的过程，而变基是直接修改分支开始的位置，比如我们希望将yyds变基到master上，那么yyds会将分支起点移动到master最后一次提交位置：

```sh
git rebase master
```

变基后，yyds分支相当于同步了此前master分支的全部提交。

### 优选

我们还可以选择其将他分支上的提交作用于当前分支上，这种操作称为cherrypick：

```sh
git cherry-pick <commit id>:单独合并一个提交
```

这里我们在master分支上创建一个新的文件，提交此次更新，接着通过cherry-pick的方式将此次更新作用于test分支上。

***

## 远程仓库

远程仓库实际上就是位于服务器上的仓库，它能在远端保存我们的版本历史，并且可以实现多人同时合作编写项目，每个人都能够同步他人的版本，能够看到他人的版本提交，相当于将我们的代码放在服务器上进行托管。

远程仓库有公有和私有的，公有的远程仓库有GitHub、码云、Coding等，他们都是对外开放的，我们注册账号之后就可以使用远程仓库进行版本控制，其中最大的就是GitHub，但是它服务器在国外，我们国内连接可能会有一点卡。私有的一般是GitLab这种自主搭建的远程仓库私服，在公司中比较常用，它只对公司内部开放，不对外开放。

这里我们以GitHub做讲解，官网：https://github.com，首先完成用户注册。

### 远程账户认证和推送

接着我们就可以创建一个自定义的远程仓库了。

创建仓库后，我们可以通过推送来将本地仓库中的内容推送到远程仓库。

```sh
git remote add 名称 远程仓库地址
git push 远程仓库名称 本地分支名称[:远端分支名称]
```

注意`push`后面两个参数，一个是远端名称，还有一个就是本地分支名称，但是如果本地分支名称和远端分支名称一致，那么不用指定远端分支名称，但是如果我们希望推送的分支在远端没有同名的，那么需要额外指定。推送前需要登陆账户，GitHub现在不允许使用用户名密码验证，只允许使用个人AccessToken来验证身份，所以我们需要先去生成一个Token才可以。

推送后，我们发现远程仓库中的内容已经与我们本地仓库中的内容保持一致了，注意，远程仓库也可以有很多个分支。

但是这样比较麻烦，我们每次都需要去输入用户名和密码，有没有一劳永逸的方法呢？当然，我们也可以使用SSH来实现一次性校验，我们可以在本地生成一个rsa公钥：

```sh
ssh-keygen -t rsa
cat ~/.ssh/github.pub
```

接着我们需要在GitHub上上传我们的公钥，当我们再次去访问GitHub时，会自动验证，就无需进行登录了，之后在Linux部分我们会详细讲解SSH的原理。

接着我们修改一下工作区的内容，提交到本地仓库后，再推送到远程仓库，提交的过程中我们注意观察提交记录：

```sh
git commit -a -m 'Modify files'
git log --all --oneline --graph
git push origin master 
git log --all --oneline --graph
```

我们可以将远端和本地的分支进行绑定，绑定后就不需要指定分支名称了：

```sh
git push --set-upstream origin master:master
git push origin
```

在一个本地仓库对应一个远程仓库的情况下，远程仓库基本上就是纯粹的代码托管了（云盘那种感觉，就纯粹是存你代码的）

## 克隆项目

如果我们已经存在一个远程仓库的情况下，我们需要在远程仓库的代码上继续编写代码，这个时候怎么办呢？

我们可以使用克隆操作来将远端仓库的内容全部复制到本地：

```sh
git clone 远程仓库地址
```

这样本地就能够直接与远程保持同步。

## 抓取、拉取和冲突解决

我们接着来看，如果这个时候，出现多个本地仓库对应一个远程仓库的情况下，比如一个团队里面，N个人都在使用同一个远程仓库，但是他们各自只负责编写和推送自己业务部分的代码，也就是我们常说的协同工作，那么这个时候，我们就需要协调。

比如程序员A完成了他的模块，那么他就可以提交代码并推送到远程仓库，这时程序员B也要开始写代码了，由于远程仓库有其他程序员的提交记录，因此程序员B的本地仓库和远程仓库不一致，这时就需要有先进行pull操作，获取远程仓库中最新的提交：

```sh
git fetch 远程仓库 #抓取：只获取但不合并远端分支，后面需要我们手动合并才能提交
git pull 远程仓库 #拉取：获取+合并
```

在程序员B拉取了最新的版本后，再编写自己的代码然后提交就可以实现多人合作编写项目了，并且在拉取过程中就能将别人提交的内容同步到本地，开发效率大大提升。

如果工作中存在不协调的地方，比如现在我们本地有两个仓库，一个仓库去修改hello.txt并直接提交，另一个仓库也修改hello.txt并直接提交，会得到如下错误：

```
To https://github.com/xx/xxx.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'https://github.com/xx/xxx.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

一旦一个本地仓库推送了代码，那么另一个本地仓库的推送会被拒绝，原因是当前文件已经被其他的推送给修改了，我们这边相当于是另一个版本，和之前两个分支合并一样，产生了冲突，因此我们只能去解决冲突问题。

如果远程仓库中的提交和本地仓库中的提交没有去编写同一个文件，那么就可以直接拉取：

```sh
git pull 远程仓库
```

拉取后会自动进行合并，合并完成之后我们再提交即可。

但是如果两次提交都修改了同一个文件，那么就会遇到和多分支合并一样的情况，在合并时会产生冲突，这时就需要我们自己去解决冲突了。

# 标签管理

## 用途

比如代码上线了，打一个标签，后续如果后回滚，直接回滚到这个标签版本

## 命令

![Screen Shot 2019-07-28 at 21.56.09](./Git/Screen Shot 2019-07-28 at 21.56.09-2569971.png)

## Tutorial：需求一，项目里程碑开发完成，打上Tag，标记版本号

![Screen Shot 2019-07-28 at 21.57.24](./Git/Screen Shot 2019-07-28 at 21.57.24-2569971.png)

![Screen Shot 2019-07-28 at 21.58.28](./Git/Screen Shot 2019-07-28 at 21.58.28-2569971.png)

![Screen Shot 2019-07-28 at 21.59.33](./Git/Screen Shot 2019-07-28 at 21.59.33-2569971.png)

## Tutorial：需求二，删除标签

![Screen Shot 2019-07-28 at 22.04.09](./Git/Screen Shot 2019-07-28 at 22.04.09-2569971.png)

# 分支管理

![Screen Shot 2019-07-28 at 22.07.08](./Git/Screen Shot 2019-07-28 at 22.07.08-2569971.png)

## 命令

切换分支使用checkout命令

可以通过 `git branch`中的 HEAD 查看当前的分支。HEAD 总是指向当前工作的分支。

## Tutorial：需求一，创建分支

![Screen Shot 2019-07-28 at 22.08.33](./Git/Screen Shot 2019-07-28 at 22.08.33-2569971.png)

![Screen Shot 2019-07-28 at 22.09.49](./Git/Screen Shot 2019-07-28 at 22.09.49-2569971.png)

![Screen Shot 2019-07-28 at 22.07.55](./Git/Screen Shot 2019-07-28 at 22.07.55-2569971.png)

上图中，切换分支使用checkout命令

![Screen Shot 2019-07-28 at 22.11.00](./Git/Screen Shot 2019-07-28 at 22.11.00-2569971.png)

## Tutorial：需求二，合并分支

合并分支，注意首先需要切换到主分支

![Screen Shot 2019-07-28 at 22.13.04](./Git/Screen Shot 2019-07-28 at 22.13.04-2569971.png)

## Tutorial：需求三，删除分支

合并后，删除分支

![Screen Shot 2019-07-28 at 22.14.18](./Git/Screen Shot 2019-07-28 at 22.14.18-2569971.png)

# Git amend：对已提交的文件或提交信息进行修改

## 功能/使用场景

提交后，发现提交错了，对文件进行修改，此时使用 git amend进行修改，**不会创建一个新的commit**，只会对上一个commit中的部分文件进行修改。这里的部分，就是指你本次新变更的文件。

## 注意点：Git amend 最好对本地的commit使用

如果你的commit已经推送到远程服务器，别人很可能已经pull了你的提交，这个时候进行git amend就会导致别人获取到的代码和你新修改的文件版本不一致。

# Git stash：暂存

## 功能/使用场景

比如你的develop进行开发，但是现在有紧急需求需要你切换到master进行开发。此时可以使用 git stash 将当前未提交的代码暂存起来。

## 与 git stage 的区别

通常，两者都被翻译成暂存。

# rebase: 变基

Rebase 前，分支如下图：

![image-20220901200632416](./Git/image-20220901200632416-2569971.png)

Rebase 后，如下图：

![image-20220901200534924](./Git/image-20220901200534924-2569971.png)

## git rebase 与 git merge 的区别

看下面的图即可。merge 是合并两个分支，rebase 是改变了**基底**。

![image-20220901200846841](./Git/image-20220901200846841-2569971.png)

merge 的另一个特点是：会保留全部的commit 历史。

# 撤销：git revert

`git revert 旧的提交hash`

## 使用场景

撤销之前的修改，但是会留下log。

Revert 的特点是：不会修改旧的提交历史，而是在工作树中生成与之前提交完全相反的修改。

# Tutorial

## 使用Git创建Github项目

### 第一步：绑定密钥到 Github

![Screen Shot 2019-07-28 at 21.21.28](./Git/Screen Shot 2019-07-28 at 21.21.28-2569971.png)

![Screen Shot 2019-07-28 at 21.22.42](./Git/Screen Shot 2019-07-28 at 21.22.42-2569971.png)

拷贝上面的Key，放到GitHub上

![Screen Shot 2019-07-28 at 21.23.43](./Git/Screen Shot 2019-07-28 at 21.23.43-2569971.png)

测试是否连通GitHub。不用关注上面的warning。

![Screen Shot 2019-07-28 at 21.24.52](./Git/Screen Shot 2019-07-28 at 21.24.52-2569971.png)

### 第二步：Github创建repository

![Screen Shot 2019-07-28 at 21.30.54](./Git/Screen Shot 2019-07-28 at 21.30.54-2569971.png)

![Screen Shot 2019-07-28 at 21.31.57](./Git/Screen Shot 2019-07-28 at 21.31.57-2569971.png)

### 提交到Github上

![Screen Shot 2019-07-28 at 21.33.56](./Git/Screen Shot 2019-07-28 at 21.33.56-2569971.png)

1. 上面push命令使用-u选项，表示本地master和远程的master关联上
2. 修改README.md后，重新提交

![Screen Shot 2019-07-28 at 21.36.56](./Git/Screen Shot 2019-07-28 at 21.36.56-2569971.png)

第二次提交时，不用再使用push -u 选项，第一次已经指定了

![Screen Shot 2019-07-28 at 20.52.34](./Git/Screen Shot 2019-07-28 at 20.52.34-2569971.png)

![Screen Shot 2019-07-28 at 20.53.59](./Git/Screen Shot 2019-07-28 at 20.53.59-2569971.png)

![Screen Shot 2019-07-28 at 20.54.47](./Git/Screen Shot 2019-07-28 at 20.54.47-2569971.png)

## 克隆远程仓库代码，进行本地开发

![Screen Shot 2019-07-28 at 21.48.53](./Git/Screen Shot 2019-07-28 at 21.48.53-2569971.png)

![Screen Shot 2019-07-28 at 21.49.50](./Git/Screen Shot 2019-07-28 at 21.49.50-2569971.png)

![Screen Shot 2019-07-28 at 21.51.54](./Git/Screen Shot 2019-07-28 at 21.51.54-2569971.png)

上图中，最后一行不需要使用push -u 选项，因为clone时已经绑定了分支。

## 需求一：修改bash_demo.txt文件后，需要回滚成上一个版本

```shell
git reset HEAD 文件名
git checkout -- 文件名
```

![Screen Shot 2019-07-28 at 20.56.19](./Git/Screen Shot 2019-07-28 at 20.56.19-2569971.png)

回滚

![Screen Shot 2019-07-28 at 21.00.24](./Git/Screen Shot 2019-07-28 at 21.00.24-2569971.png)

执行上面的回滚命令后，文件还没有实际变更成上一个版本，需要清理工作区

![Screen Shot 2019-07-28 at 21.02.36](./Git/Screen Shot 2019-07-28 at 21.02.36-2569971.png)

## 需求二：又有了新的需求，修改bash_demo.txt文件，提交

```shell
git commit -m "本次提交的备注"
```

![Screen Shot 2019-07-28 at 21.05.12](./Git/Screen Shot 2019-07-28 at 21.05.12-2569971.png)

## 需求三：现在，第二次提交的内容不需要，需要回滚到第一次的内容

### 第一步：使用 git log 拿到第一次提交的Commit号

![Screen Shot 2019-07-28 at 21.06.08](./Git/Screen Shot 2019-07-28 at 21.06.08-2569971.png)

### 第二步：回滚

--hard 表示最终仓库和暂存序列文件都回滚到第一次提交

![Screen Shot 2019-07-28 at 21.10.07](./Git/Screen Shot 2019-07-28 at 21.10.07-2569971.png)

现在清空bash_demo.txt文件

![Screen Shot 2019-07-28 at 21.12.18](./Git/Screen Shot 2019-07-28 at 21.12.18-2569971.png)

## 撤销已经commit但是未push的操作

```shell
# 查看commit的版本
$ git log
 
回退命令：
 
# 回退到上个版本
$ git reset HEAD^ 
 
# 回退到前3次提交之前，以此类推，回退到n次提交之前
$ git reset HEAD~3  
    
# 回退到指定commit的版本
$ git reset commit_id

```

> [取消已经commit但是未push的操作](https://blog.csdn.net/fenglongmiao/article/details/81546199)

## 撤销已经push到远端的代码

其实是没有直接让远端代码回复到某次的指令，实现撤销push的思路如下：

> 1.先让代码恢复到想要恢复的前一次提交记录 2.重新提交代码，覆盖端上的代码，就相当于撤销了push 的提交

实现方式如下：

1.首先使用`git log`找到要回退版本的commit版本号；

2.`git reset --hard <版本号>`，撤回到需要的版本; 注意在执行命令之前先把当前工作拷贝一份，不然--hard会将修改全部丢失

3.使用`git push --force`覆盖之前的提交

> [Git 撤销已经push到远端的代码_LoveIT的博客—EasyBlog博客](https://www.easyblog.top/article/details/314)

## 将当前修改的内容提交到新的分支上

使用场景：

参加一个项目时，执行clone得到master分支， 一开始只是想看看源码或者忘记了自己没有新建分支，结果后面自己根据需求添加了代码【添加后没有执行commit】, 但是此时的修改都在master分支， 提交必然是不可以的，还是要新建分支【所有修改都要在新建分支上进行】，最后在分支执行通过后，才能合并到master分支。
那么，这时候如何力挽狂澜，如何在保存这些修改的前提下，新建分支并提交呢？

```shell
//步骤1：在当前的develop分支上的修改暂存起来
git stash
//步骤2：暂存修改后，在本地新建分支（develop_backup为新分支的名字）
git checkout -b develop_backup
//步骤3：将暂存的修改放到新建分支中
git stash pop
//步骤4：使用命令进行常规的add、commit步骤
git add.
git commit -m "修改内容"
//步骤5：将提交的内容push到远程服务器(在远程也同步新建分支develop_backup)
# 最后的两个字段分别是：本地分支:远端希望创建的分支
git push origin develop_backup:develop_backup
```

> [Git：将当前修改的内容提交到新的分支上 - CodeAntenna](https://codeantenna.com/a/mRUx21Y1aI)

## push代码到远程新分支

获取远程代码修改后,想要push到远端与原来不同的新分支，可以使用下面的命令实现：
`git push origin 本地分支:远端希望创建的分支`

> [git push代码到远程新分支_hitrjj的博客-CSDN博客_push分支](https://blog.csdn.net/u014636245/article/details/83382907)

## 撤销多个文件/整个文件夹

> git checkout <folder-name>/
>
> git checkout -- <folder-name>
>
> 这样会把<fold-name>下所有的文件都撤销

## case：error: Your local changes to the following files would be overwritten by merge

> [git pull的时候发生冲突的解决方法之“error: Your local changes to the following files would be overwritten by merge” - 菜鸟学飞ing - 博客园 (cnblogs.com)](https://www.cnblogs.com/nebie/p/10830838.html)

## 将 本地仓库推送到远程仓库上

> 需求：本地仓库没有绑定 git，将本地仓库推送到远端已有仓库的某个分支上

```shell
# 1.首先在项目目录下初始化本地仓库
git init
# 2.添加所有文件( . 表示所有)
git add .
# 3.提交所有文件到本地仓库
git commit -m "备注信息"
# 4.连接到远程仓库，origin 不要动
git remote add origin 你的远程仓库地址
# 5.将项目推送到远程仓库
# 远端的分支，不用是已有的
git push origin HEAD:远端的分支
```

```shell
命令行指引
Git 全局设置
git config --global user.name "alex"
git config --global user.email "abc@alibaba-inc.com"
克隆仓库
git clone git@gitlab.alibaba-inc.com:banma-QueryMatching/EntityLinking.git
cd EntityLinking
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
对于已存放的文件夹或仓库
cd EntityLinking
git init
git remote add origin git@gitlab.alibaba-inc.com:banma-QueryMatching/EntityLinking.git
git add .
git commit
git push -u origin master
```

## 删除远程分支

```shell
# 可以删除远程分支Chapater6   
git push origin --delete Chapater6
# 再次使用命令 git branch -a   可以发现，远程分支Chapater6已经被删除。
```

## 删除本地分支

```shell
# 切换到主分支
git checkout  master
# 删除本地分支（在主分支中）
git branch -d Chapater8
```

## `git add .` 之后想撤回该如何操作？

使用 `git reset `即可。

## 修改了一个文件，现在想撤销全部修改，该如何操作？

```shell
git checkout HEAD 文件名
```

## 只添加修改过的文件，但忽略新创建的文件或未追踪的文件，该如何操作？

> [git add -u 仅添加 modified file_冬日and暖阳的博客-CSDN博客](https://blog.csdn.net/qq_29007291/article/details/88344768)

使用 `git add -u` 命令。add modified files and deleted files， don’t care about new created files

## 列出你需要取消跟踪的文件

```shell
# 列出你需要取消跟踪的文件，可以查看列表，检查下是否有误操作导致一些不应该被取消的文件取消了，是为了再次确认的。-r 表示递归，-n 表示先不删除，只是列出文件。
git rm -r -n --cached 文件或目录
```

## 取消对某个文件的跟踪

```shell
# 取消对某个文件的跟踪
git rm -r --cached 文件
```

# References

1. https://mp.weixin.qq.com/s/_w7FsD2VoJzpFd9tTkDC3A

## 撤销已经commit但是未push的操作

```shell
# 查看commit的版本
$ git log
 
回退命令：
 
# 回退到上个版本
$ git reset HEAD^ 
 
# 回退到前3次提交之前，以此类推，回退到n次提交之前
$ git reset HEAD~3  
    
# 回退到指定commit的版本
$ git reset commit_id

```

> [取消已经commit但是未push的操作](https://blog.csdn.net/fenglongmiao/article/details/81546199)

## 撤销已经push到远端的代码

其实是没有直接让远端代码回复到某次的指令，实现撤销push的思路如下：

> 1.先让代码恢复到想要恢复的前一次提交记录 2.重新提交代码，覆盖端上的代码，就相当于撤销了push 的提交

实现方式如下：

1.首先使用`git log`找到要回退版本的commit版本号；

2.`git reset --hard <版本号>`，撤回到需要的版本; 注意在执行命令之前先把当前工作拷贝一份，不然--hard会将修改全部丢失

3.使用`git push --force`覆盖之前的提交

> [Git 撤销已经push到远端的代码_LoveIT的博客—EasyBlog博客](https://www.easyblog.top/article/details/314)

## 将当前修改的内容提交到新的分支上

使用场景：

参加一个项目时，执行clone得到master分支， 一开始只是想看看源码或者忘记了自己没有新建分支，结果后面自己根据需求添加了代码【添加后没有执行commit】, 但是此时的修改都在master分支， 提交必然是不可以的，还是要新建分支【所有修改都要在新建分支上进行】，最后在分支执行通过后，才能合并到master分支。
那么，这时候如何力挽狂澜，如何在保存这些修改的前提下，新建分支并提交呢？

```shell
//步骤1：在当前的develop分支上的修改暂存起来
git stash
//步骤2：暂存修改后，在本地新建分支（develop_backup为新分支的名字）
git checkout -b develop_backup
//步骤3：将暂存的修改放到新建分支中
git stash pop
//步骤4：使用命令进行常规的add、commit步骤
git add.
git commit -m "修改内容"
//步骤5：将提交的内容push到远程服务器(在远程也同步新建分支develop_backup)
# 最后的两个字段分别是：本地分支:远端希望创建的分支
git push origin develop_backup:develop_backup
```

> [Git：将当前修改的内容提交到新的分支上 - CodeAntenna](https://codeantenna.com/a/mRUx21Y1aI)

## push代码到远程新分支

获取远程代码修改后,想要push到远端与原来不同的新分支，可以使用下面的命令实现：
`git push origin 本地分支:远端希望创建的分支`

> [git push代码到远程新分支_hitrjj的博客-CSDN博客_push分支](https://blog.csdn.net/u014636245/article/details/83382907)

## 撤销多个文件/整个文件夹

> git checkout <folder-name>/
>
> git checkout -- <folder-name>
>
> 这样会把<fold-name>下所有的文件都撤销

## case：error: Your local changes to the following files would be overwritten by merge

> [git pull的时候发生冲突的解决方法之“error: Your local changes to the following files would be overwritten by merge” - 菜鸟学飞ing - 博客园 (cnblogs.com)](https://www.cnblogs.com/nebie/p/10830838.html)

## 将 本地仓库推送到远程仓库上

> 需求：本地仓库没有绑定 git，将本地仓库推送到远端已有仓库的某个分支上

```shell
# 1.首先在项目目录下初始化本地仓库
git init
# 2.添加所有文件( . 表示所有)
git add .
# 3.提交所有文件到本地仓库
git commit -m "备注信息"
# 4.连接到远程仓库，origin 不要动
git remote add origin 你的远程仓库地址
# 5.将项目推送到远程仓库
# 远端的分支，不用是已有的
git push origin HEAD:远端的分支
```

```shell
命令行指引
Git 全局设置
git config --global user.name "alex"
git config --global user.email "abc@alibaba-inc.com"
克隆仓库
git clone git@gitlab.alibaba-inc.com:banma-QueryMatching/EntityLinking.git
cd EntityLinking
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
对于已存放的文件夹或仓库
cd EntityLinking
git init
git remote add origin git@gitlab.alibaba-inc.com:banma-QueryMatching/EntityLinking.git
git add .
git commit
git push -u origin master
```

## 删除远程分支

```shell
# 可以删除远程分支Chapater6   
git push origin --delete Chapater6
# 再次使用命令 git branch -a   可以发现，远程分支Chapater6已经被删除。
```

## 删除本地分支

```shell
# 切换到主分支
git checkout  master
# 删除本地分支（在主分支中）
git branch -d Chapater8
```

## `git add .` 之后想撤回该如何操作？

使用 `git reset `即可。

## 修改了一个文件，现在想撤销全部修改，该如何操作？

```shell
git checkout HEAD 文件名
```

## 只添加修改过的文件，但忽略新创建的文件或未追踪的文件，该如何操作？

> [git add -u 仅添加 modified file_冬日and暖阳的博客-CSDN博客](https://blog.csdn.net/qq_29007291/article/details/88344768)

使用 `git add -u` 命令。add modified files and deleted files， don’t care about new created files

## 列出你需要取消跟踪的文件

```shell
# 列出你需要取消跟踪的文件，可以查看列表，检查下是否有误操作导致一些不应该被取消的文件取消了，是为了再次确认的。-r 表示递归，-n 表示先不删除，只是列出文件。
git rm -r -n --cached 文件或目录
```

## 取消对某个文件的跟踪

```shell
# 取消对某个文件的跟踪
git rm -r --cached 文件
```

# References

1. https://mp.weixin.qq.com/s/_w7FsD2VoJzpFd9tTkDC3A
