# 二、Git使用教程----要用与github同样的邮箱和用户名
https://zhuanlan.zhihu.com/p/30044692
![GIT](\pic\img.png)

    Workspace：工作区
    Index / Stage：暂存区
    Repository：仓库区（或本地仓库）
    Remote：远程仓库

git config --global 参数，有了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然你也可以对某个仓库指定的不同的用户名和邮箱
![GIT_user](\pic\git_user.png)

在E盘uestc下，创建testgit版本库。—— 进入到目录后使用

    mkdir testgit

版本库又名仓库，英文名repository,你可以简单的理解一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改，删除，Git都能跟踪，以便还原

通过命令    

    git init

把这个目录变成git可以管理的仓库


这时当前testgit目录下会多了一个.git的目录，这个目录是Git来跟踪管理版本的，没事千万不要手动乱改这个目录里面的文件，否则，会把git仓库给破坏了。（是一个隐藏文件）

在版本库testgit目录下新建一个记事本文件 readme.txt，内容为空

①用命令 git add readme.txt添加到暂存区里面去
②用命令 git commit告诉Git，把文件提交到仓库，提交到当前分支
  通过命令git status来查看是否还有文件未提交
  git diff readme.txt查看readme.txt文件到底改了什么内容
Another git process seems to be running in this repository使用如下命令

    rm -f .git/index.lock

## 版本回退

    git log--查看历史记录
    git log -–pretty=oneline  -->>  如果嫌上面显示的信息太多的话，我们可以使用命令 

    git reset --hard HEAD^  -->>   退回上个版本
    git reset --hard HEAD^^  -->>   退回上上个版本
    git reset --hard HEAD~100  -->>   退回上100个版本
    
    cat -- 终端查看一个文件内容
    Git 的 reflog 是指引用日志（reference logs）的简称，它记录了 Git 仓库中 HEAD 引用的变化历史。换句话说，reflog 记录了本地仓库的操作历史，包括分支切换、合并、重置等操作，即使在一些操作后出现了提交丢失或者分支丢失的情况下，通过 reflog 也可以找回之前的状态
    git reflog获取版本号
    git reset --hard (版本号，一串码)

## 工作区和暂存区的区别

***工作区***：就是你在电脑上看到的目录，比如目录下testgit里的文件(.git隐藏目录版本库除外)。或者以后需要再新建的目录文件等等都属于工作区范畴。  

***版本库***(Repository)：工作区有一个隐藏目录.git,这个不属于工作区，这是版本库。其中版本库里面存了很多东西，其中最重要的就是stage(暂存区)，还有Git为我们自动创建了第一个分支master,以及指向master的一个指针HEAD。

## Git撤销修改和删除文件操作

### 1.撤销修改

在未提交之前发现添加内容有误，得马上恢复以前的版本，现在有如下几种方法可以做修改：

第一：如果我知道要删掉那些内容的话，直接手动更改去掉那些需要的文件，然后add添加到暂存区，最后commit掉。

第二：我可以按以前的方法直接恢复到上一个版本。使用 git reset --hard HEAD^----(不太好用的感觉)

第三（main）
    
    git checkout -- （file名）-----把readme.txt文件在工作区做的修改全部撤销

### 2.删除文件
    
    rm b.txt   >>>>>   删除文件

![delete](\pic\img_1.png)

## 远程仓库

由于本地Git仓库和github仓库之间的传输是通过SSH加密的，所以需要一点设置，

***第一步***

    ssh-keygen -t rsa –C “youremail@example.com”   >>>>    创建id_rsa（私钥）和id_rsa.pub（公钥）

***第二步***

登录github,打开” settings”中的SSH Keys页面，然后点击“Add SSH Key”,填上任意title，在Key文本框里黏贴id_rsa.pub文件的内容。

![SSH](\pic\img_2.png)

Authentication Keys（身份验证密钥）:

1.用于身份验证，允许您与GitHub进行安全通信，例如通过SSH连接。

2.当您从本地系统与GitHub进行交互时，这是用于验证您身份的密钥。通常，这与访问和推送代码相关。

Signing Keys（签名密钥）:

1.用于对Git提交进行数字签名，以验证提交的真实性和完整性。

2.这是在Git操作中确保提交的来源和内容未被篡改的一种方式。通过签署提交，您可以确保提交是由特定的私钥持有者创建的。

### 仓库同步

**已经在本地创建了一个Git仓库后，又想在github创建一个Git仓库，并且希望这两个仓库进行远程同步，这样github的仓库可以作为备份，又可以其他人通过该仓库来协作**

①登录github上，然后在右上角找到“create a new repo”创建一个新的仓库

②在Repository name填入testgit，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库

③可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库

    git remote add origin （https://github.com/hhqggy0504/testgit   >>>   github库SSH连接复制）

    git push -u origin master   >>>>>>   把本地仓库分支master内容推送到元仓库中

***连接报错***

    fatal: unable to access 'https://github.com/hhqggy0504/testgit.git/': Failed to connect to github.com port 443 after 21084 ms: Could not connect to server

    git push origin master   >>>>>   从现在起，只要本地作了提交，就可以通过如下命令

#### 如何从远程库克隆

    git clone （github库的SSH连接）  >>>>>   克隆一个本地库

## 创建与合并分支

    git checkout 命令加上 –b参数表示创建并切换，相当于如下2条命令
    git branch dev
    git checkout dev
    git merge    >>>>   命令用于合并指定分支到当前分支上

总结创建与合并分支命令如下：

查看分支：git branch

创建分支：git branch name

切换分支：git checkout name

创建+切换分支：git checkout –b name

合并某分支到当前分支：git merge name

删除分支：git branch –d name

### 冲突解决

（***手动修改***）Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，其中<<<HEAD是指主分支修改的内容，>>>>>fenzhi1 是指fenzhi1上修改的内容，我们可以修改下如下后保存：

    git log  >>>   查看分支合并的情况    （按q退出）

### 分支管理策略

通常合并分支时，git一般使用”Fast forward”模式，在这种模式下，删除分支后，会丢掉分支信息，可以使用带参数 –no-ff来禁用”Fast forward”模式

![DEV](\pic\img_3.png)

***分支策略***：首先master主分支应该是非常稳定的，也就是用来发布新版本，一般情况下不允许在上面干活，干活一般情况下在新建的dev分支上干活，干完后，比如上要发布，或者说dev分支代码稳定后可以合并到主分支master上来

### bug分支

隐藏
    
    git stash >>>  隐藏当前工作现场（让可以去master重新创建分支）

恢复

    ①git stash apply恢复，恢复后，stash内容并不删除，你需要使用命令git stash drop来删除
    ②另一种方式是使用git stash pop,恢复的同时把stash内容也删除了


## 多人协同

多人协作时，大家都会往master分支上推送各自的修改。现在可以模拟另外一个同事，可以在另一台电脑上（注意要把SSH key添加到github上）或者同一台电脑上另外一个目录克隆，新建一个目录名字叫testgit2

***
多人协作工作模式一般是这样的：

首先，可以试图用git push origin branch-name推送自己的修改.
如果推送失败，则因为远程分支比你的本地更新早，需要先用git pull试图合并。
如果合并有冲突，则需要解决冲突，并在本地提交。再用git push origin branch-name推送
***

①首先要把dev分支也要推送到远程去
②接着进入testgit2目录，进行克隆远程的库到本地来
③进入testgit2的testgit1

    git checkout –b dev origin/dev >>>>>  把远程的origin的dev分支到本地来

④小伙伴们已经向origin/dev分支上推送了提交，而我在我的目录文件下也对同样的文件同个地方作了修改，也试图推送到远程库时冲突

  ⑤.1 先用git pull把最新的提交从origin/dev抓下来，然后在本地合并，解决冲突，再推送
  ⑤.2 git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接

    git branch --set-upstream-to=origin/dev

  ⑤.3 git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的 解决冲突完全一样。解决后，提交，再push
  


# 一、新建代码库

## 在当前目录新建一个Git代码库
    $ git init

## 新建一个目录，将其初始化为Git代码库
    $ git init [project-name] # 下载一个项目和它的整个代码历史
    $ git clone [url]

# 二、配置
## 显示当前的Git配置
    $ git config --list

## 编辑Git配置文件
    $ git config -e [--global] # 设置提交代码时的用户信息
    $ git config [--global] user.name "[name]"
    $ git config [--global] user.email "[email address]"

# 三、增加/删除文件
## 添加指定文件到暂存区
    $ git add [file1] [file2] ... # 添加指定目录到暂存区，包括子目录
    $ git add [dir] # 添加当前目录的所有文件到暂存区
    $ git add . # 添加每个变化前，都会要求确认 # 对于同一个文件的多处变化，可以实现分次提交
    $ git add -p

## 删除工作区文件，并且将这次删除放入暂存区
    $ git rm [file1] [file2] ... # 停止追踪指定文件，但该文件会保留在工作区
    $ git rm --cached [file] # 改名文件，并且将这个改名放入暂存区
    $ git mv [file-original] [file-renamed]

# 四、代码提交
## 提交暂存区到仓库区
    $ git commit -m [message] # 提交暂存区的指定文件到仓库区
    $ git commit [file1] [file2] ... -m [message] # 提交工作区自上次commit之后的变化，直接到仓库区
    $ git commit -a

## 提交时显示所有diff信息
    $ git commit -v

## 使用一次新的commit，替代上一次提交 # 如果代码没有任何新变化，则用来改写上一次commit的提交信息
    $ git commit --amend -m [message] # 重做上一次commit，并包括指定文件的新变化
    $ git commit --amend [file1] [file2] ...

# 五、分支
## 列出所有本地分支
    $ git branch

## 列出所有远程分支
    $ git branch -r

## 列出所有本地分支和远程分支
    $ git branch -a

## 新建一个分支，但依然停留在当前分支


  
    $ git branch [branch-name] # 新建一个分支，并切换到该分支
    $ git checkout -b [branch] # 新建一个分支，指向指定commit
    $ git branch [branch] [commit] # 新建一个分支，与指定的远程分支建立追踪关系
    $ git branch --track [branch] [remote-branch] # 切换到指定分支，并更新工作区
    $ git checkout [branch-name] # 切换到上一个分支
    $ git checkout - # 建立追踪关系，在现有分支与指定的远程分支之间
    $ git branch --set-upstream [branch] [remote-branch] # 合并指定分支到当前分支
    $ git merge [branch] # 选择一个commit，合并进当前分支
    $ git cherry-pick [commit] # 删除分支
    $ git branch -d [branch-name] # 删除远程分支
    $ git push origin --delete [branch-name]
    $ git branch -dr [remote/branch]


# 六、标签
## 列出所有tag
    $ git tag

## 新建一个tag在当前commit
    $ git tag [tag] # 新建一个tag在指定commit
    $ git tag [tag] [commit] # 删除本地tag
    $ git tag -d [tag] # 删除远程tag
    $ git push origin :refs/tags/[tagName] # 查看tag信息
    $ git show [tag] # 提交指定tag
    $ git push [remote] [tag] # 提交所有tag
    $ git push [remote] --tags

## 新建一个分支，指向某个tag
    $ git checkout -b [branch] [tag]

# 七、查看信息
## 显示有变更的文件
    $ git status

## 显示当前分支的版本历史
    $ git log

## 显示commit历史，以及每次commit发生变更的文件
    $ git log --stat

## 搜索提交历史，根据关键词
    $ git log -S [keyword] # 显示某个commit之后的所有变动，每个commit占据一行
    $ git log [tag] HEAD --pretty=format:%s

## 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
    $ git log [tag] HEAD --grep feature

## 显示某个文件的版本历史，包括文件改名
    $ git log --follow [file]
    $ git whatchanged [file] # 显示指定文件相关的每一次diff
    $ git log -p [file] # 显示过去5次提交
    $ git log -5 --pretty --oneline

## 显示所有提交过的用户，按提交次数排序
    $ git shortlog -sn

## 显示指定文件是什么人在什么时间修改过
    $ git blame [file] # 显示暂存区和工作区的差异
    $ git diff

## 显示暂存区和上一个commit的差异
    $ git diff --cached [file] # 显示工作区与当前分支最新commit之间的差异
    $ git diff HEAD

## 显示两次提交之间的差异
    $ git diff [first-branch]...[second-branch] # 显示今天你写了多少行代码
    $ git diff --shortstat "@{0 day ago}" # 显示某次提交的元数据和内容变化
    $ git show [commit] # 显示某次提交发生变化的文件
    $ git show --name-only [commit] # 显示某次提交时，某个文件的内容
    $ git show [commit]:[filename] # 显示当前分支的最近几次提交
    $ git reflog

# 八、远程同步
## 下载远程仓库的所有变动
    $ git fetch [remote] # 显示所有远程仓库
    $ git remote -v

## 显示某个远程仓库的信息
    $ git remote show [remote] # 增加一个新的远程仓库，并命名
    $ git remote add [shortname] [url] # 取回远程仓库的变化，并与本地分支合并
    $ git pull [remote] [branch] # 上传本地指定分支到远程仓库
    $ git push [remote] [branch] # 强行推送当前分支到远程仓库，即使有冲突
    $ git push [remote] --force

## 推送所有分支到远程仓库
    $ git push [remote] --all

# 九、撤销
## 恢复暂存区的指定文件到工作区
    $ git checkout [file] # 恢复某个commit的指定文件到暂存区和工作区
    $ git checkout [commit] [file] # 恢复暂存区的所有文件到工作区
    $ git checkout . # 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
    $ git reset [file] # 重置暂存区与工作区，与上一次commit保持一致
    $ git reset --hard

## 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
    $ git reset [commit] # 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
    $ git reset --hard [commit] # 重置当前HEAD为指定commit，但保持暂存区和工作区不变
    $ git reset --keep [commit] # 新建一个commit，用来撤销指定commit # 后者的所有变化都将被前者抵消，并且应用到当前分支
    $ git revert [commit] # 暂时将未提交的变化移除，稍后再移入
    $ git stash
    $ git stash pop


# 好的分支策略

首先，代码库应该有一个、且仅有一个主分支。所有提供给用户使用的正式版本，都在这个主分支上发布。

## 一、主分支Master

Git主分支的名字，默认叫做Master。它是自动建立的，版本库初始化以后，默认就是在主分支在进行开发。

## 二、开发分支Develop

主分支只用来发布重大版本，日常开发应该在另一条分支上完成。我们把开发用的分支，叫做Develop。

![Develop](\pic\img_8.png)

这个分支可以用来生成代码的最新隔夜版本（nightly）。如果想正式对外发布，就在Master分支上，对Develop分支进行"合并"（merge）。

    git checkout -b develop master   >>>>>   Git创建Develop分支的命令
      
    git checkout master       >>>>>      切换到Master分支
  
    git merge --no-ff develop#    >>>>    对Develop分支进行合并

--no-ff参数是什么意思。默认情况下，Git执行"快进式合并"（fast-farward merge），会直接将Master分支指向Develop分支
![no ff](\pic\img_9.png)

使用--no-ff参数后，会执行正常合并，在Master分支上生成一个新节点。为了保证版本演进的清晰，我们希望采用这种做法。

![img_10.png](\pic\img_10.png)

## 三、临时性分支

除了常设分支以外，还有一些临时性分支，用于应对一些特定目的的版本开发。临时性分支主要有三种：

·功能（feature）分支

·预发布（release）分支

·修补bug（fixbug）分支

## 第一种是功能分支

它是为了开发某种特定功能，从Develop分支上面分出来的。开发完成后，要再并入Develop

![img_11.png](\pic\img_11.png)

## 第二种是预发布分支

指发布正式版本之前（即合并到Master分支之前），我们可能需要有一个预发布的版本进行测试。

预发布分支是从Develop分支上面分出来的，预发布结束以后，必须合并进Develop和Master分支。它的命名，可以采用release-*的形式。 

## 最后一种是修补bug分支

修补bug分支是从Master分支上面分出来的。修补结束以后，再合并进Master和Develop分支。它的命名，可以采用fixbug-*的形式。

![img_12.png](\pic\img_12.png)


# GitHub仓库快速导入Gitee及同步更新

## 一、仓库导入

①登录Gitee，点击右上角的 + 号，点击「从 GitHub 导入仓库」，在跳转的页面中授权 Gitee 访问。

与 GitHub 对接。

选择性的导入您的 Github 项目到 Gitee

## 二、Gitee 和 Github 同步更新

### ①方法一（推荐）：比较少分支的仓库

如果是本地仓库，只在需要命令行添加用不同名称标识的 Gitee  和 Github 远程库。

    git remote add 远程库名 远程库地址

具体方法操作如下：

1、首先通过 git remote -v 查看您要同步的仓库的远程库列表，如果在列表中没有您 Gitee 的远程库地址，您需要新增一个地址

    git remote add 远程库名 远程库地址
    eg: git remote add gitee git@github.com:xxx/xxx.git
    如果在 add 的时候出现error: Could not remove config section 'remote.xxx'.一类的错误，通过把仓库下.git/config 文件里面的 [remote "xxx"] 删掉或者是用别的远程库名即可。

2、从 GitHub 上拉取最新代码到本地

    git pull 远程库名 分支名
    eg：git pull origin master

3、推送本地最新代码到 Gitee 上

    git push 远程库名 分支名
    eg：git push gitee master
如果出现有差异的话需要自己手动解决差异

### 方法二（推荐）：比较多分支的仓库

克隆 GitHub 仓库到本地，命令如下

    $ git clone git@github.com:xxx/xxx.git
    # 进入仓库目录
    $ cd xxx

### 方法三：比较多分支的仓库

在 Gitee 仓库主页点击同步更新按钮即可