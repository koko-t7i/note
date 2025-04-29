# Git

## Git 配置文件

> Git 配置文件：[初次运行 Git 前的配置](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%88%9D%E6%AC%A1%E8%BF%90%E8%A1%8C-Git-%E5%89%8D%E7%9A%84%E9%85%8D%E7%BD%AE)

### 用户信息配置

> 每一次 Git 提交都会用到这些信息

```shell
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
git config --global core.editor "vim" # 默认编辑器
git config --global init.defaultBranch main # 切换默认主分支为 main
```

查看所有配置信息，以及所在地址

```shell
git config --list --show-origin
```

## Git Basics

GIt 基本流程图: 

![image-20231210152307822](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210152307822.3k7sw4junn.webp)

在已存在的目录中初始化 Git 仓库

```shell
git init <filename>
```

克隆一个现有的仓库

```shell
git clone [url] <新的目录名>
```

跟踪新文件，添加到暂存区

```shell
git add <files>
```

从暂存区到工作区，和上条命令是逆操作

```shell
git reset <files>
```

提交文件到仓库

```shell
git commit -m <message>
```

从仓库到暂存区，和上条 commit 是逆操作

```shell
git rest --sort <files>
```

查看文件状态

```shell
git status
```

![文件状态变化周期示意图](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231201222041546.231nudfpwu.webp)

新建并切换到分支:

```shell
git checkout -b testing
```

等同于

```shell
git branch testing
git checkout testing
```

```shell
git branch # 查看分支列表
# output: 
# * master
#   testing
```

删除分支

```shell
git branch -d testing
```

## Git Example

1. 初始化仓库

```shell
git init git-exampel
```

![image-20231210152047472](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210152047472.7i06csuvan.webp)

2. 监测 .git 文件夹的变化，按照 0.5 秒的轮询频率

```shell
watch -n .5 tree .git
```

![监测 .git 文件状态](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210152743611.13lkh7cyr8.webp)

3. 在 git-example 下新建 1.txt 文件输入内容 1

```shell
echo 1 > 1.txt
```

4. 将 1.txt 添加进暂存区，查看 .git 文件变化

```shell
git add 1.txt
```

![image-20231210153509059](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210153509059.1lbm5secc7.webp)

5. 将 1.txt 添加到本地仓库，这里把 hook 文件夹删除了，方便我们观察 objects 文件

```shell
git commit -m "first commit"
```

![image-20231210154004529](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210154004529.8z6bejz01n.webp)

6. 我们观察 `git add` 和 `git commit` 命令下都发生了什么

`git cat-file -t` 查看该文件的类型（有前缀匹配不用全部输入，取前面几个字符就行）

我们先看 `git add` 命令下的文件

```shell
git cat-file -t d00491 # 查看类型 // 输出 blob
```

```shell
git cat-file -p d00491 # 查看文件内容 // 输出 1
```

查看 `git commit` 命令后生成的文件

```shell
git cat-file -t 38fd29
git cat-file -p 38fd29
git cat-file -t 89bec1
git cat-file -p 89bec1
```

![image-20231210162905465](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210162905465.9nzkykmj28.webp)

示意图：

![image-20231210164227195](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210164227195.26l9s38sn6.webp)

7. 分支

之前我们的操作都是在 master 分支上进行的，查看一下 master 分支的 head 指向，可以看到指向了最新的 commit object

![image-20231210170040621](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210170040621.4jnw9amltw.webp)

现在我们新建一个 testing 分支，并切换到 testing，查看其head指向

可以看到和 master 分支指向的 commit object 一样

```shell
git checkout -b testing
cat .git/refs/heads/testing
```

![image-20231210170452139](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210170452139.3d4l0oxp8l.webp)

在 testing 分支下进行 `git add` `git commit` 操作

![image-20231210172249356](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210172249356.3go6yeqryf.webp)

查看 testing 的 head 指向，可以看到testing 分支的 head 指向了最新的一个 commit object

```shell
cat .git/refs/heads/testing
git cat-file -p 7e2f6
```

![image-20231210174706442](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210174706442.pf4qc4nwp.webp)

多了以个指向前一个版本 commit object 的 parent 指针

![image-20231210175344281](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210175344281.4n7i70foju.webp)

8. 切换为 master 分支，进行第二次提交

```shell
git checkout master
echo 3 > 3.txt
git add 3.txt
git commit -m "third commit"
```

![image-20231210201558856](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210201558856.1756ex61hn.webp)

此时 master 和 testing 都在各自分支上进行了版本迭代

现在将 testing分支下的代码合并到 master

```shell
git merge testing
```

![image-20231210203426221](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210203426221.b8ozgwd1o.webp)

9. 遇到冲突时如何合并，如对同一个文件同一处地方进行了修改
   
   我们分别在 master 和 testing 分支 修改 1.txt 文件

```shell
echo 3 > 1.txt
git add 1.txt
git commit -m "fifth commit"

git checkout testing
echo 3_1 > 1.txt
git add 1.txt
git commit -m "sixth commit on testing"
```

这时我们在合并就会出现合并冲突

```shell
git merge testing 
# output:
# Auto-merging 1.txt
# CONFLICT (content): Merge conflict in 1.txt
# Automatic merge failed; fix conflicts and then commit the result.
```

![image-20231210205812489](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210205812489.3go6yeqryl.webp)

打开冲突文件手动修改文件，删除掉 <<<< ===== >>>> 等标记，手动修改成想要合并的代码

![image-20231210211234694](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210211234694.361d59bjta.webp)

修改成

![image-20231210212004029](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210212004029.5c0rr137kf.webp)

```shell
git add 1.txt
git commit -m "7 commit"
```

![image-20231210212123002](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210212123002.6pnav2e9ld.webp)

如果 testing 想要合并 master 同理即可

10. 变基

`git rebase` 是合并分支的另一种方式，是团队合作中更受推崇的方式

```shell
# master 中添加了 6.txt
git checkout -b rebase-branch
echo 7 > 7.txt
git add 7.txt
git commit -m "7.txt"
git rebase master
```

![image-20231210230728717](https://github.com/koko-t7i/picx-images-hosting/raw/master/markdown/image-20231210230728717.6pnav2e9lf.webp)

11. 远程 git remote

远程连接 github 仓库

```shell
git init
git add .
git commit -m "initial commit"
git remote add origin git@github.com:koko-t7i/Anitale-Vue.git
git push -u origin main
```

如果仓库上有文件可能会导致 push 报错：常见报错解决问题如下

[pull 分支报错 fatal: Need to specify how to reconcile divergent branches](https://blog.csdn.net/qq_45677671/article/details/122574671)
[fatal: The current branch master has no upstream branch.](https://blog.csdn.net/weixin_38080573/article/details/88077187)
[Git中fatal: refusing to merge unrelated histories](https://blog.csdn.net/wd2014610/article/details/80854807)

12. git stash