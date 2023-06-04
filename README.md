1. 首先第一次使用 git 需要做一些配置

```bash
git config --global user.name "chengongfu"
```

```bash
git config --global user.email gfchen196@foxmail.com
```

上述的配置是说明性的，可以任设



2. 我们新建一个项目目录，开始往里面添加代码或者文档，这个时候 git 还没有开始管理我们的代码

   

3. 我们通过 `git init` 命令来初始化仓库，使得目录下的代码可以被 git 管理，同时目录下当前的所有文件都会被跟踪，这样 git 才能记录文件的状态。

   

4. 通过 `git status` 查看文件的状态，可以看到文件是红色的

   文件的状态有这么几种：

- 未跟踪  （git status 文件为红色）

- (已跟踪且)已修改，未暂存 （git status 文件为红色）

- (已跟踪且)已暂存（git status 文件为绿色）

- (已跟踪且)已提交

  

5. 通过 `git add <文件> ` 命令将文件改为暂存状态

   

6.  `get reset HEAD <file>` ，使暂存的文件取消暂存状态

   ```bash
   $ git reset HEAD test_git.txt
   
   fatal: 有歧义的参数 'HEAD'：未知的版本或路径不存在于工作区中。
   使用 '--' 来分隔版本和路径，例如：
   'git <命令> [<版本>...] -- [<文件>...]'
   ```

   这里是由于我们没有进行过任何提交。在其他情况也会引起，比如:

   - HEAD 引用丢失或损坏

   - 分支或提交不存在

   - 文件不在工作区

     

   ```bash
   $ git commit -m "第一次提交，添加了README.md和test_git.txt" #提交
   
   [master（根提交） 999e015] 第一次提交，添加了README.md和test_git.txt
    2 files changed, 98 insertions(+)
    create mode 100644 README.md
    create mode 100644 test_git.txt
   ```

   提示我们进行了根提交。

   

   ```bash
   $ git branch #查看分支列表
   * master
   ```

   这里 HEAD 引用指向 master 分支

   

   ```bash
   $ git reflog #查看引用日志
   999e015 (HEAD -> master) HEAD@{0}: commit (initial): 第一次提交，添加了README.md和test_git.txt
   ```

   

7.关于暂存区我的几个问题

Q1：假设在 `git commit` 之前，我手抽把重要文件的暂存文件通过 `sudo rm` 删除了，还可以通过 git 恢复吗

A1：不可以。操做系统方面的操作，git 不会记录操作系统的删除，但 `git diff` 会比较暂存文件与当前修改的差异，也许可以通过保存 `git diff` 的报告来恢复，所以要避免 sudo 操作。



Q2 : 假设在 `git commit` 之前，我把已暂存未提交的文件通过 `git rm` 删除了，还可以通过 git 恢复吗

A2: 我使用的 git 版本不支持这个文件的`git rm` 不加参数

`git rm -f` 会从暂存区和工作目录彻底删除，git 不会保留被删除文件的历史记录，`git diff` 也不会报告。

`git rm --cached <文件>` 会从暂存区删除文件，但保留在本地目录，`git diff` 只管暂存区，所以没有报告。



Q3:  对一个已暂存文件暂存两次但未提交，可以恢复到倒数第二次暂存前的状态吗

A3: 不可以。只能恢复到最后一次暂存前的状态，通过



# 上传到 github

1. ssh 鉴权

   ```bash
   cd ~/.ssh
   ssh-keygen -t rsa -b 4096 -C "gfchen196@foxmail.com"
   # 打开公钥复制
   gedit github.pub
   ```

   github 右上角用户头像下拉 >> setting >> SSH and GPG KEY

   把 github.pub里面的内容复制进去。

   

2. push 两次？

