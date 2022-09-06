# Git


# Git

## git bash 命令

~~~txt
基本Linux命令行使用
1）、cd : 改变目录。
2）、cd . . 回退到上一个目录，直接cd进入默认目录
3）、pwd : 显示当前所在的目录路径。
4）、ls(ll): 都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细。
5）、touch : 新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件。
6）、rm: 删除一个文件, rm index.js 就会把index.js文件删除。
7）、mkdir: 新建一个目录,就是新建一个文件夹。
8）、rm -r : 删除一个文件夹, rm -r src 删除src目录
9）、mv 移动文件, mv index.html src index.html 是我们要移动的文件, src 是目标文件夹,当然, 这样写,
必须保证文件和目标文件夹在同一目录下。
10）、reset 重新初始化终端/清屏。
11）、clear 清屏。
12）、history 查看命令历史。
13）、help 帮助。
14）、exit 退出。
15）、#表示注释
~~~

## Git 配置

```markdown
查看配置 git config -l

# 查看系统config
git config --system --list
# 查看当前用户（global）配置
git config --global --list
```

```markdown
*# 设置用户名与邮箱（用户标识，必要）
```

```markdown
git config --global user.name "用户名称" #名称
git config --global user.email 888888@qq.com #邮箱
```

## Git理论

Git本地有三个工作区域：工作目录（Working Directory）、暂存区(Stage/Index)、资源库(Repository或Git Directory)。如果在加上远程的git仓库(Remote Directory)就可以分为四个工作区域。文件在这四个区域之间的转换关系如下：

![image-20220512204804576](/assets/image-20220512204804576.png)

- Workspace：工作区，就是平时存放项目代码的地方
- Index / Stage：暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息
- Repository：仓库区（或本地仓库），就是安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本
- Remote：远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换

```txt
git的工作流程一般是这样的：
１、在工作目录中添加、修改文件；
２、将需要进行版本管理的文件放入暂存区域；
３、将暂存区域的文件提交到git仓库。
因此，git管理的文件有三种状态：已修改（modified）,已暂存（staged）,已提交(committed)

```

![image-20220512205229355](/assets/image-20220512205229355.png)

## Git 项目搭建

**本地仓库搭建**
创建本地仓库的方法有两种：一种是创建全新的仓库，另一种是克隆远程仓库。
1、创建全新的仓库，需要用GIT管理的项目的根目录执行：

```markdown
# 在当前目录新建一个Git代码库
$ git init
```

2、执行后可以看到，仅仅在项目目录多出了一个.git目录，关于版本等的所有信息都在这个目录里面。

**克隆远程仓库**
1、另一种方式是克隆远程目录，由于是将远程服务器上的仓库完全镜像一份至本地！
2、去 gitee 或者 github 上克隆一个测试！

```markdown
# 克隆一个项目和它的整个代码历史(版本信息)
$ git clone [url]
eg: git clone  https://github.com/Yhai-Young/LiveChat.git
```

## Git文件操作

- **Untracked**: 未跟踪, 此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过**git add**状态变为**Staged **
- **Unmodify**: 文件已经入库, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为**Modified** . 如果使用**git rm** 移出版本库, 则成为**Untracked** 文件
- **Modified**: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过**git add** 可进入暂存**Staged** 状态, 使用**git checkout** 则丢弃修改过, 返回到**unmodify** 状态,这个**git checkout** 即从库中取出文件, 覆盖当前修改 
- **Staged**: 暂存状态. 执行**git commit** 则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为**Unmodify** 状态. 执行**git reset HEAD filename** 取消暂存, 文件状态为**Modified**

```markdown
# 查看文件状态
git status [filename]

# 查看所有文件状态
git status
```

```markdown
# 忽略文件

有些时候我们不想把某些文件纳入版本控制中，比如数据库文件，临时文件，设计文件等
在主目录下建立".gitignore"文件，此文件有如下规则：
1. 忽略文件中的空行或以井号（#）开始的行将会被忽略。
2. 可以使用Linux通配符。例如：星号（*）代表任意多个字符，问号（？）代表一个字符，方括号（[abc]）代表可选字符范围，大括（{string1,string2,...}）代表可选的字符串等。
3. 如果名称的最前面有一个感叹号（!），表示例外规则，将不被忽略。
4. 如果名称的最前面是一个路径分隔符（/），表示要忽略的文件在此目录下，而子目录中的文件不忽略。
5. 如果名称的最后面是一个路径分隔符（/），表示要忽略的是此目录下该名称的子目录，而非文件（默认文件或目录都忽略）。


# 为注释
*.txt #忽略所有 .txt结尾的文件
!lib.txt #但lib.txt除外
/temp #仅忽略项目根目录下的TODO文件,不包括其它目录temp
build/ #忽略build/目录下的所有文件
doc/*.txt #会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```

## Intel 集成Git

```markdown
# 列出所有本地分支
git branch
# 列出所有远程分支
git branch -r
# 新建一个分支，但依然停留在当前分支
git branch [branch-name]
# 新建一个分支，并切换到该分支
git checkout -b [branch]
# 合并指定分支到当前分支
$ git merge [branch]
# 删除分支
$ git branch -d [branch-name]
# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```






