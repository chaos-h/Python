# git learning notes
[教程地址](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
## git configuration
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
git config --global color.ui true
这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。
## git basic
1. 创建git仓库
    `git init`
2. 添加文件
`git add <file>`
3. 提交修改
`git commit -m  "the modification desciption" `
4. 查看仓库状态:检查仓库是否有改动
`git status`
5. 查看文件的修改内容
`git diff  <file>`
**注意:1. 必须先add然后才能commit 2. 可以add多个文件,一次提交**  

## 时光穿梭
1. 版本切换(回退or向前)
`git reset --hard <commit_id>`
commit_id  查看:
`git log`:可以查看提交历史,可带参数` --pretty=oneline --abbrev-commit` 第一个参数可以将log内容只显示重要的一行, 第二个参数让取id前几个
`git reflog`: 可以查看命令历史
注意:commit_id 可以用HEAD指代, HEAD^表示上一个版本,HEAD^^表示上上个版本,HEAD~100表示往上第100个版本
2.  工作区和暂存区
工作区: 就是工作目录,文件夹
隐藏目录.git:git的版本库,包含自动创建的分区master,指向master的指针HEAD
stage(index):暂存区
![GIT结构图](http://www.liaoxuefeng.com/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)
把文件往版本库里面添加包含两步骤:
	-  git add 把文件修改添加到缓存区 
	- git commit 提交更改, 把暂存区的内容提交到当前分支
3. 管理修改
git 跟踪管理的是修改,不是文件, 每一次修改都要git add 到暂存区, 否则不能被commit
4. 撤销修改
场景1: 修改了工作区某个文件的内容, 想直接丢弃工作区的修改:`git checkout --  <file>`
场景2: 修改了工作区内容且add 到了暂存区,想丢弃修改:分两步,先`git reset Head <file>`撤销暂存操作, 然后`git checkout -- <file>`
场景3: 修改已经提交, 只能版本回退了,注意,推送到远程库的更改没法解决
注意: git checkout 其实用版本库里面的版本替代工作区的版本
5. 删除文件:
`git rm <file>`+`git commit`
如果误删且没有git rm, 可以用`git checkout -- <file>`找回;即使git rm, 也可以通过版本回退来找回已经提交的文件

## 远程仓库
1. 关联远程仓库
首先, 关联远程仓库:`git remote add origin git@server-name:path/repo-name.git`
其次, 推送master分支所有内容:`git push -u origin master`
最后,在工作中,根据需要推送最新修改:`git push origin master`
2. 从远程仓库克隆
`git clone`+ 远程仓库地址
eg. `git clone git@github.com:chaos-h/clothes-matching-challenge-on-taobao.com.git`
以上是ssh方式,也可以直接跟网址或路径,克隆的仓库只包含master分支,可以在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/<branch-name>`，本地和远程分支的名称最好一致；

## 分支管理
1. 创建和合并分支
查看分支: `git brach`
创建分支: `git brance <branch_name>`
切换分支: `git checkout <branch_name>`
创建+切换分支: `git checkout -b <branch_name>`
合并分支到当前分支: `git merge <branch_name>`
删除分支: `git branch -d <brance_name>`
2. 解决冲突
当git 无法自动合并分支时, 就必须首先解决冲突.解决冲突后,再提交,合并完成.
用`git log --graph`可以查看分支合并图
3. 分支管理策略
两种策略:
策略一:直接`git merge`,是*Fast forward* 模式,这种模式下,删除分支后,会丢失分支信息,看不出曾经做过的合并
策略二: `git merge --no-ff`,禁用*Fast forward*,git在merge时就会生成于i个新的commit,分支历史上可以看出分支信息.所以合并时候可以加上`-m <message>`
4. bug 分支
修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。
命令:
`git stash`: 保存当前工作的工作现场,保存之后工作区会变的和上一次commit一致, 是干净的
`git stash apply`: 恢复现场,stash内容不删除
`git stash drop`: 删除stash内容
`git stash pop`: 恢复现场的同时把stash内容删除
`git stash list`: 查看stash堆栈,可以多次stash,回复指定stash可以用`git stash apply stash@{0}`
5. 功能分支,强行删除未被合并的分支
开发一个新feature，最好新建一个分支；
如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。
6.  多人协作
查看远程库信息，使用`git remote -v`；
本地新建的分支如果不推送到远程，对其他人就是不可见的；
本地推送分支，使用`git push origin <branch-name>`，如果推送失败，先用`git pull`抓取远程的新提交；
在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/<branch-name>`，本地和远程分支的名称最好一致；
建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/<branch-name>`；
从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

## 标签管理
1. 创建标签
    命令`git tag <name>`用于新建一个标签，默认为HEAD，也可以指定一个commit id；
    `git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
    `git tag -s <tagname> -m "blablabla..."`可以用PGP签名标签；
    命令`git tag`可以查看所有标签。
    `git show <tagname> `可以看到说明文字
2.  标签管理

    命令`git push origin <tagname>`可以推送一个本地标签；
    命令`git push origin --tags`可以推送全部未推送过的本地标签；
    命令`git tag -d <tagname>`可以删除一个本地标签；
    命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。

## 使用github

## 自定义 git
1. 忽略特殊文件
> 在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。   
[别人定义好的.gitignore](https://github.com/github/gitignore)
命令:
`git add -f <fielname>`: 强制添加.gitignore规则内的东西
`git check-ignore -v <filename>`: 查看文件与.gitignore规则哪条相合
2. 配置别名
有两种方法更改别名:
用命令:`git config --global alias.<别名>  <命令名>`
改配置文件.git/.config,将alias 下的内容更改即可.
更改别名后, 就可以用别名替代原来命令使用.
常见更改:
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"  
 git config --global alias.unstage 'reset HEAD'
 git config --global alias.st status
 git config --global alias.co checkout
 git config --global alias.ci commit
 git config --global alias.br branch
3. 搭建git服务器