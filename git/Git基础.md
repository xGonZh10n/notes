# Git基础

## 创建Git仓库

- 创建新的仓库

  首先需要创建一个工作目录`test`，然后在终端切换至该目录并输入：
  
    ```ruby
  $ git init
    ```
  
- 克隆现有仓库

  如果想获得一份`test`仓库的拷贝，可以在终端输入：

    ```ruby
  $ git clone https://github.com/xGonZh10n/test.git
    ```

  或者

    ```ruby
  $ git clone git@github.com:xGonZh10n/test.git
    ```

## 记录每次更新到仓库

工作目录下的文件主要有以下两种状态：

- 已跟踪：指那些被纳入版本控制的文件，它们的状态又可细分为未修改，已修改或已暂存。
- 未跟踪：工作目录中除了已跟踪文件以外的所有其它文件。

初次创建或克隆某个仓库时，工作目录中的所有文件都属于已跟踪文件，并处于未修改状态。编辑某些文件后，Git会将它们标记为已修改文件。我们逐步将这些修改过的文件放入暂存区，然后提交所有暂存的修改，如此反复。所以，使用Git时文件的生命周期如下：

![](./images/Git_Basics/lifecycle.png)

### 查看文件状态

```ruby
$ git status
```

如果不需要查看详细状态，可在命令后面加上 `-s` 参数。

### 添加文件到暂存区

```ruby
$ git add <file>
```

该命令使用文件或目录路径作为参数，如果参数是目录路径，则递归跟踪该目录下所有文件；同时，每一次修改文件都需要运行该命令把文件最新版本重新暂存。

### 忽略文件

如果有文件无需纳入Git管理，我们可以创建.gitignore文件，并在其中列出需要忽略的文件模式。该文件的格式规范如下：

- 所有空行或者以`#`开头的行都会被Git忽略；
- 可以使用标准的glob模式匹配；
- 匹配模式可以以（`/`）开头防止递归；
- 匹配模式可以以（`/`）结尾指定目录；
- 要忽略指定模式以外的文件或目录，可以在模式前加上感叹号（`!`）取反。

GitHub上有一个十分详细的针对数十种项目及语言的[.gitignore文件列表](https://github.com/github/gitignore)，可以作为参考。

### 查看已暂存或未暂存的修改

如果你想知道当前做的哪些更新还没有暂存，哪些更新已经暂存起来准备提交，可以使用`git diff`命令。尽管`git status`命令可以简单的列出修改过的文件名，但是`git diff`命令将会更详细的显示文件具体哪些行发生了改变。

- 查看尚未暂存的文件更新了哪些部分：

    ```ruby
  $ git diff
  ```

  此命令比较的是工作目录中当前文件和暂存区域快照之间的差异，也就是修改之后还没有暂存起来的变化。

- 查看已暂存的将要添加到下次提交里的内容：

    ```ruby
  $ git diff --cached
  ```

### 提交更新

每次提交前，先用`git status`看一下文件是不是都已经暂存起来，然后再进行提交：

```ruby
$ git commit -m "<message>"
```

### 移除文件

从暂存区域移除，并连带从工作目录中删除指定的文件，可以使用以下命令：

```ruby
$ git rm <file>
```

如果删除之前修改过并且已经放到暂存区域，则必须要用强制删除选项`-f`。

如果想把文件从Git仓库删除，但仍希望保留在当前工作目录中，则需要使用`--cached`选项。

### 移动或重命名文件

```ruby
$ git mv <from> <to>
```

## 查看提交历史

```ruby
$ git log
```

默认不用任何参数，该命令会按提交时间列出所有的更新，最近的更新排在最上面。

如果需要显示每次提交的内容差异，可以使用选项`-p`。你也可以在选项后面加上`-2`来仅显示最近两次提交。

如果需要查看每次提交的简略统计信息，可以使用选项`--stat`。在每次提交下面列出所有被修改过的文件、有多少文件被修改以及被修改过的文件的哪些行被添加或移除。

如果需要使用其它格式展示提交历史，可以使用选项`--pretty`。

## 撤销操作

如果提交完成后发现漏掉几个文件没有添加，或者提交信息写错。可以运行以下命令尝试重新提交：

```ruby
$ git commit --amend
```

该命令会将暂存区中的文件提交。如果自上次提交以来还未做任何修改，那么快照会保持不变，修改的只是提交信息。而且最终只会有一个提交，第二次提交将代替第一次提交的结果。

### 取消暂存的文件

```ruby
$ git reset HEAD <file>
```

### 撤销对文件的修改

```ruby
$ git checkout -- <file>
```

### 版本切换

```ruby
$ git reset --hard <commit_id>
```

想要切换到的commit_id可通过`git reflog`命令查看，此外，上一个版本的commit_id也可使用HEAD^表示。

## 远程仓库的使用

### 查看远程仓库

```ruby
$ git remote <-v>
```

该命令会列出你指定的每一个远程服务器的简写。如果加上选项`-v`，则会显示需要读写远程仓库使用的Git保存的简写与其对应的URL。

### 添加远程仓库

```ruby
$ git remote add <remote-name> <url>
```

该命令添加一个新的远程Git仓库，同时指定一个名字简写。

### 从远程仓库中抓取

```ruby
$ git fetch <remote-name>
```

该命令会访问远程仓库，并从中拉取你还没有的数据到本地仓库，但它并不会自动合并或修改你当前的工作，必须手动将其合并。如果想要自动抓取数据然后合并到当前分支，你可以使用`git pull`命令。

### 推送到远程仓库

```ruby
$ git push <remote-name> <branch-name>
```

### 查看某个远程仓库

```ruby
$ git remote show <remote-name>
```

### 重命名某个远程仓库

```ruby
$ git remote rename <from> <to>
```

### 移除某个远程仓库

```ruby
$ git remote rm <remote-name>
```

## 打标签

### 列出标签

```ruby
$ git tag
```

### 附注标签

```ruby
$ git tag -a <tag-name> -m "<message>"
```

其中，选项`-m`指定了一条将会存储在标签中的信息。通过使用`git show`命令，可以看到标签信息与对应的提交信息。

### 轻量标签

```ruby
$ git tag <tag-name>
```

通过使用`git show`命令，不会看到额外的标签信息，只会显示出提交信息。

### 查看标签信息

```ruby
$ git show <tag-name>
```

### 后期打标签

在打标签命令后面指定提交的校验和或部分校验和。

### 共享标签

默认情况下，`git push` 命令并不会传送标签到远程仓库服务器上。 在创建完标签后你必须显式地推送标签到共享服务器上。

- 推送单个标签

    ```ruby
  $ git push origin <tag-name>
  ```

- 推送多个标签

    ```ruby
  $ git push origin --tags
  ```

### 删除标签

删除本地仓库上的标签，可以使用命令：

```ruby
$ git tag -d <tag-name>
```

但是，上述命令并不会从任何远程仓库中移除这个标签，必须使用以下命令来更新远程仓库：

```ruby
$ git push origin :refs/tags/<tag-name>
```

## Git别名

可以通过`git config`为每个命令设置一个别名。例如：

```ruby
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
```

为了解决取消暂存文件命令的易用性问题，可以添加自己的取消暂存别名：

```ruby
$ git config --global alias.unstage 'reset HEAD'
```

这会使以下两个命令等价：

```ruby
$ git unstage <file>
$ git reset HEAD <file>
```

## 参考资料

- [Pro Git 第二版](https://git-scm.com/book/zh/v2)
- [廖雪峰的Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)
- [RUNOOB.COM的Git教程](https://www.runoob.com/git/git-tutorial.html)