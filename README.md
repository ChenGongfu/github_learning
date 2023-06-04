### 1. 首先第一次使用 git 需要做一些配置

```bash
git config --global user.name "chengongfu"
```

```bash
git config --global user.email gfchen196@foxmail.com
```

上述的配置是说明性的，可以任设

### 2. 我们新建一个项目目录，开始往里面添加代码或者文档，这个时候 git 还没有开始管理我们的代码

```bash
mkdir github_learning
cd github_learning
touch test_git.txt
```

```bash
cgf@Early2Bed:~/Projects/Creations/github_learning$ git status

fatal: 不是 git 仓库（或者直至挂载点 / 的任何父目录）
停止在文件系统边界（未设置 GIT_DISCOVERY_ACROSS_FILESYSTEM）。
```

### 3. 我们通过 `git init` 命令来初始化仓库，使得目录下的代码可以被 git 管理，同时目录下当前的所有文件都会被跟踪，这样 git 才能记录文件的状态。

```bash
cgf@Early2Bed:~/Projects/Creations/github_learning$ git init

提示：使用 'master' 作为初始分支的名称。这个默认分支名称可能会更改。要在新仓库中
提示：配置使用初始分支名，并消除这条警告，请执行：
提示：
提示：	git config --global init.defaultBranch <名称>
提示：
提示：除了 'master' 之外，通常选定的名字有 'main'、'trunk' 和 'development'。
提示：可以通过以下命令重命名刚创建的分支：
提示：
提示：	git branch -m <name>
已初始化空的 Git 仓库于 /home/cgf/Projects/Creations/github_learning/.git/
```

### 通过 `git status` 查看文件的状态，可以看到文件是红色的

文件的状态有这么几种：

未跟踪  （git status 文件为红色）

(已跟踪且)已修改，未暂存 （git status 文件为红色）

(已跟踪且)已暂存（git status 文件为绿色）

(已跟踪且)已提交

<img src="/home/cgf/Projects/Creations/github_learning/typora_images/image-20230604191952660.png" alt="image-20230604191952660" style="zoom: 50%;" />

### 通过 `git add <文件> ` 命令将文件改为暂存状态

<img src="/home/cgf/Projects/Creations/github_learning/typora_images/image-20230604194932005.png" alt="image-20230604194932005" style="zoom:50%;" />

```bash
cp README.md README.md.bak # README.md 是未被跟踪的
```

```bash
git add README.md.bak # 暂存
```

<img src="/home/cgf/Projects/Creations/github_learning/typora_images/image-20230604200811174.png" alt="image-20230604200811174" style="zoom:50%;" />

Q : 假设在 `git commit` 之前，我手抽把重要文件的暂存文件通过 `sudo rm` 删除了，还可以通过 git 恢复吗

A : 不可以。操做系统方面的操作，git 不会记录操作系统的删除，但 `git diff` 会比较暂存文件与当前修改的差异，也许可以通过保存 `git diff` 的报告来恢复，所以要避免 sudo 操作

<img src="/home/cgf/Projects/Creations/github_learning/typora_images/image-20230604202906699.png" alt="image-20230604202906699" style="zoom:50%;" />



Q : 假设在 `git commit` 之前，我把已暂存未提交的文件通过 `git rm` 删除了，还可以通过 git 恢复吗

A : 我使用的 git 版本不支持这个文件的`git rm` 不加参数

<img src="/home/cgf/Projects/Creations/github_learning/typora_images/image-20230604204131246.png" alt="image-20230604204131246" style="zoom:50%;" />

`git rm -f` 会从暂存区和工作目录彻底删除，git 不会保留被删除文件的历史记录，`git diff` 也不会报告。

`git rm --cached <文件>` 会从暂存区删除文件，但保留在本地目录，`git diff` 只管暂存区，所以没有报告。

<img src="/home/cgf/Projects/Creations/github_learning/typora_images/image-20230604204730224.png" alt="image-20230604204730224" style="zoom:50%;" />

Q: 对一个已暂存文件暂存两次但未提交，可以恢复到倒数第二次暂存前的状态吗

A:不可以。只能恢复到最后一次暂存前的状态，通过

<img src="/home/cgf/Projects/Creations/github_learning/typora_images/image-20230604210737010.png" alt="image-20230604210737010" style="zoom:50%;" />

