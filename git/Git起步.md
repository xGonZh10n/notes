# Git起步

## 简介

Git是一个开源的分布式版本控制系统，可以对任何类型的文件进行版本控制。

## 特点

- 直接记录快照，而非差异比较

  大部分系统都是以文件变更列表的方式存储每个文件与初始版本的差异，

  ![](./images/Getting_Started/deltas.png)

  Git则把数据看作是对小型文件系统的一组快照，在文件发生变更时对当时的全部文件制作一个快照并保存这个快照的索引，形成一系列快照流；

  ![](./images/Getting_Started/snapshots.png)

- 近乎所有操作都是本地执行

  在Git中的绝大多数操作都只需访问本地文件和资源，一般不需要来自网络的其它信息，因为在本地磁盘上就有项目的完整历史；

- 保证完整性

  Git中所有数据在存储前都通过SHA-1哈希算法计算校验和，然后以校验和来引用，这意味着不可能在Git不知情的情况下更改任何文件内容；

- 一般只添加数据

  执行的Git操作几乎只往Git仓库中增加数据，很难让Git执行任何不可逆操作，或者让它以任何方式清除数据。

## 状态转换

Git有三种状态：

- 已修改：表示修改了文件，但还没保存至Git仓库；
- 已暂存：表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中；
- 已提交：表示文件已经安全的保存至Git仓库。

与之对应，Git项目具有以下三个工作区域：

- 工作目录：对项目某个版本独立提取出来的内容，放在磁盘以供修改与使用；
- 暂存区域：是一个文件，保存下次将提交的文件列表信息；
- Git仓库：Git用来保存项目元数据和文件对象的仓库。

![](./images/Getting_Started/areas.png)

## 工作流程

1. 在工作目录中修改文件；
2. 暂存文件，将文件快照放入暂存区域；
3. 提交更新，找到暂存区域的文件，将文件快照永久性存储到Git仓库。

## 安装

在Ubuntu系统中安装Git：

```ruby
$ sudo apt-get install git
```

## 配置

Git通过`git config`工具来帮助设置控制Git外观和行为的环境变量，这些变量保存在以下三个地方：

- /etc/gitconfig：包含系统上每一个用户及其仓库的通用配置，可使用`git config --system`读写配置变量；
- ~/.gitconfig：只针对当前用户，可使用`git config --global`读写配置变量；
- 当前仓库.git目录中的config文件：只针对该仓库，可使用`git config`读写配置变量。

上述文件，每一个级别都会覆盖上一个级别的配置。

设置当前用户的用户名与Email地址：

```ruby
$ git config --global user.name "username"
$ git config --global user.email "username@example.com"
```

查看配置信息：

```ruby
$ git config --list
```

## 参考资料

- [Pro Git 第二版](https://git-scm.com/book/zh/v2)
- [廖雪峰的Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)
- [RUNOOB.COM的Git教程](https://www.runoob.com/git/git-tutorial.html)

