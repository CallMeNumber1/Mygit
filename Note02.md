git学习笔记
<git简介>
	一、git init 初始化一个git仓库
	二、添加文件到git仓库
		分两步：1、git add <file>，可反复使用，添加多个文件
				2、git commit -m"本次提交的说明" 完成
	三、阿斯顿
	四、git status| git diff
		git diff  是你工作区跟statge的比较，这个时候可以看你开发过程中修改了
		哪些内容
		git diff --cached 是看你stge区和仓库分支上的比较，你add后但是没有
		commit， 这个时候只是在stage中，可以确认下修改是否正确，如果正确无误
		可以commit合并到分支
<时光机穿梭>	
	五、git log命令显示从最近到最远的提交日志，加上--pretty=oneline参数一行显示
	六、Git中用HEAD（其实是指向当前版本的指针）表示当前版本，HEAD^表示上一个版
本，HEAD^^表示上上个版本，HEAD~100表示往上100个版本。
	七、git reset --hard HEAD^表示回退到上一个版本
	八、git reflog可以查看命令历史，以便确定要回到未来的哪个版本
	九、工作区和暂存区
		工作区：电脑里能看的目录 比如：Mygit文件夹。
		版本库：工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
		Git的版本库里存了很多东西，其中最重要的就是称为stage
		（或者叫index）的暂存区。还有Git为我们自动创建的第一个分支master，
		以及指向master的一个指针叫HEAD。
	我们把文件往Git版本库里添加的时候，是分两步执行的：
	第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
	第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支
	十、Git跟踪并管理的是修改，而非文件
		每次修改，如果不add到暂存区，那就不会加入到commit中
撤销修改
	场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
	场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。
	场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。
删除文件
	命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。
远程仓库
 添加到远程库（把一个本地仓库与github中仓库关联）
	git remote add origin git@github.com:账户/仓库名.git
	添加后，远程库的名字就是oringin
	git push -u origin master 把本地库的内容推送到远程
	之后只要本地作了提交就可以 git push origin master 把本地master的最新修改
	推送到GitHub
	一、Git remote:
		1、-v 查看现有远程仓库的url
		2、修改命令
			直接修改
			git remote set-url origin <URL> 更换远程仓库地址。把<URL>更换为新的url地址
			先删后加
			git remote rm origin 
			git remote add origin git@github.com:Liutos/foobar.git 
从远程库克隆
	要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。
	Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。
分支管理
 创建与合并分支
	查看分支：git branch
	创建分支：git branch <name>
	切换分支：git checkout <name>
	创建+切换分支：git checkout -b <name>
	合并某分支到当前分支：git merge <name>
	删除分支：git branch -d <name>
 解决冲突
	个人见解：
	如果新建分支修改内容后commit，切换到master分支修改内容后又commit则会出现冲
	突，则需要处理冲突后再进行commit。之后可用$ git log --graph --pretty=oneline --abbrev-commit
	查看分支的合并情况。
<<<<<<<<<<<<<<<<<<<<<<<
Git 使用vi或vim命令打开、关闭、保存文件
	1、创建、打开文件：$ vi [filename]
		键盘输入字母 “i”或“Insert”键进入最常用的插入编辑模式。
	2、保存文件：
	按下 “ESC” 键，退出编辑模式，切换到命令模式。
	在命令模式下键入"ZZ"或者":wq"保存修改并且退出 vi
附：常见命令
pwd查看当前目录 ls查看当前目录下内容
mkdir创建目录 touch创建文件
cat查看文件全部内容 必须有后缀
rm删除文件
>>>>>>>>>>>>>>>>>>>>>>>>>>>
分支管理策略
	在实际开发中，我们应该按照几个基本原则进行分支管理：
	首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
	那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
	你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。
合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并
BUG分支
	修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
	当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。
		工作区是干净的，刚才的工作现场存到哪去了？用git stash list命令看看：
		$ git stash list
		stash@{0}: WIP on dev: 6224937 add merge
		工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：
		一是用git stash apply恢复，$ git stash apply stash@{0}但是恢复后，stash内容并不删除，你需要用git stash drop来删除；
		另一种方式是用git stash pop，恢复的同时把stash内容也删了：
feature分支
	开发一个新feature，最好新建一个分支；
	如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。
多人协作
	*查看远程库信息，使用git remote -v；
	*本地新建的分支如果不推送到远程，对其他人就是不可见的；
	*从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
	*在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
	*建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
	*从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。
	多人协作的工作模式通常是这样：
 1、首先，可以试图用git push origin branch-name推送自己的修改；
 2、如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
 3、如果合并有冲突，则解决冲突，并在本地提交；
	没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！
 4、如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。
 这就是多人协作的工作模式，一旦熟悉了，就非常简单。
创建标签
	命令git tag <name>用于新建一个标签，默认为HEAD，也可以指定一个commit id；
	git tag -a <tagname> -m "blablabla..."可以指定标签信息；
	git tag -s <tagname> -m "blablabla..."可以用PGP签名标签；
	标签不是按时间顺序列出，而是按字母排序的。可以用git show <tagname>查看标签信息：
	命令git tag可以查看所有标签。
删除标签
	命令git push origin <tagname>可以推送一个本地标签；
	命令git push origin --tags可以推送全部未推送过的本地标签；
	命令git tag -d <tagname>可以删除一个本地标签；
	命令git push origin :refs/tags/<tagname>可以删除一个远程标签。
<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
	1、不同项目关联到同一远程git上的对应仓库上可以都使用origin 这个别名的。
	即在本地仓库与远程仓库关联时 git inti --> git remote add origin URL -->
	git push -u origin master 。
	2、一个本地库能不能既关联GitHub，又关联码云呢？
	答案是肯定的，因为git本身是分布式版本控制系统，可以同步到另外一个远程库，当然也可以同步到另外两个远程库。
	使用多个远程库时，我们要注意，git给远程库起的默认名称是origin，如果有多个远程库，我们需要用不同的名称来标识不同的远程库。
	仍然以learngit本地库为例，我们先删除已关联的名为origin的远程库：
	git remote rm origin
	然后，先关联GitHub的远程库：
	git remote add github git@github.com:michaelliao/learngit.git
	注意，远程库的名称叫github，不叫origin了。
	接着，再关联码云的远程库：
	git remote add gitee git@gitee.com:liaoxuefeng/learngit.git
	同样注意，远程库的名称叫gitee，不叫origin。
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>	
自定义Git
	忽略特殊文件：
	忽略某些文件时，需要编写.gitignore；
	.gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！
	
	如果觉得要忽略的内容太多懒得管理, 可以采取全部忽略逐一排除的策略
	先*忽略全部, 之后再!设定不被忽略的内容
   .gitignore:
	*          # 忽略全部

	!/ch01/    # 不忽略的文件夹
	!/ch02/

	!*.c       # 不忽略的文件
	!*.h
	!*.cpp
	!*.md
	!*.txt
	
	
	
	
	
附：新电脑上使用Git&Github	
2.安装客户端msysgit
github是服务端，要想在自己电脑上使用git我们还需要一个git客户端，我这里选用msysgit，这个只是提供了git的核心功能，而且是基于命令行的。如果想要图形界面的话只要在msysgit的基础上安装TortoiseGit即可。
装完msysgit后右键鼠标会多出一些选项来，在本地仓库里右键选择Git Init Here，会多出来一个.git文件夹，这就表示本地git创建成功。右键Git Bash进入git命令行，为了把本地的仓库传到github，还需要配置ssh key。
3.配置Git
首先在本地创建ssh key；
$ ssh-keygen -t rsa -C "your_email@youremail.com"
后面的your_email@youremail.com改为你的邮箱，之后会要求确认路径和输入密码，我们这使用默认的一路回车就行。成功的话会在~/下生成.ssh文件夹，进去，打开id_rsa.pub，复制里面的key。
回到github，进入Account Settings，左边选择SSH Keys，Add SSH Key,title随便填，粘贴key。为了验证是否成功，在git bash下输入：
$ ssh -T git@github.com
如果是第一次的会提示是否continue，输入yes就会看到：You’ve successfully authenticated, but GitHub does not provide shell access 。这就表示已成功连上github。
接下来我们要做的就是把本地仓库传到github上去，在此之前还需要设置username和email，因为github每次commit都会记录他们。
$ git config --global user.name "your name"
$ git config --global user.email "your_email@youremail.com"
进入要上传的仓库，右键git bash，添加远程地址：
1
$ git remote add origin <a href=""mailto:git@github.com"" target=""_blank"">git@github.com</a>:yourName/yourRepo.git   
后面的yourName和yourRepo表示你再github的用户名和刚才新建的仓库，加完之后进入.git，打开config，这里会多出一个remote “origin”内容，这就是刚才添加的远程地址，也可以直接修改config来配置远程地址。
4.提交、上传
接下来在本地仓库里添加一些文件，比如README，
$ git add README
$ git commit -m "first commit"
上传到github：
$ git push origin master
git push命令会将本地仓库推送到远程服务器。
git pull命令则相反。
修改完代码后，使用git status可以查看文件的差别，使用git add 添加要commit的文件，也可以用git add -i来智能添加文件。之后git commit提交本次修改，git push上传到github。
	
	
C:\Users\pc\Mygit\gitskills Edit with Notepad++
Chong 1.18.2018
