####这篇文章主要是给自己记录一下如何在github上新建立一个repository
在github上建立repository的方式有两种，第一种是**建立一个带readme文件的项目，然后在本地把项目跟该repository关联（本地项目无readme文件，有的话要进行冲突处理）** 第二种是**直接建立repository然后clone下来再添加文件再提交（简单）** 我们现在主要简述第一种。
>1. 新建repository带生成的readme文件，但是要合并的本地文件夹无readme文件
 >>1. 下载git，具体百度 。
 >>2. 进入到本地项目文件夹内，右键鼠标 点击git bash here  键入*git init* 该文件夹变成Git可以管理的仓库。
>>3. 输入 *git add .* 然后通过git add将所有文件提交到暂存区。
>>4. git commit -m '说明'提交到版本库中即可。到现在为止就在本地创建的本地仓库，下面要做把本地仓库和远程仓库关联 
>>5. 到github项目那里右上角 点击clone or download  按钮 复制其中http连接 *git remote add origin https://github.com/YOURUSERNAME/YOURREPOSITORY.git* 。此时注意在将本地仓库与GitHub网站上的仓库进行关联后，便可进行推送了，但是在第一次进行推送时，需要注意的是，GitHub网站上的仓库并非是空的，我们在创建时创建了一个README文档，因此需要将两者进行合并才行。
>> 6. *git pull --rebase origin master* 合并
>>7. 最后，在进行推送即可。*git push -u origin master* 这个带有-u这个参数是指，将master分支的所有内容都提交，第一次关联之后后边你再提交就可以不用这个参数了，之后你的每一次修改，你就可以只将你修改push就好了
>> 8. git add -A  将文件的修改上传到暂存区 
git commit -m '说明'      提交到本地仓库
git push origin master   推送到GitHub网站上 后两个参数代表目的repository的master分支

### git常用命令 ###
```
mkdir： XX (创建一个空目录 XX指目录名)

pwd： 显示当前目录的路径。

git init 把当前的目录变成可以管理的git仓库，生成隐藏.git文件。

git add XX 把xx文件添加到暂存区去。

git commit –m “XX” 提交文件 –m 后面的是注释。

git status 查看仓库状态

git diff XX 查看XX文件修改了那些内容

git log 查看历史记录

git reset –hard HEAD^ 或者 git reset –hard HEAD~ 回退到上一个版本

 (如果想回退到100个版本，使用git reset –hard HEAD~100 )

cat XX 查看XX文件内容

git reflog 查看历史记录的版本号id

git checkout — XX 把XX文件在工作区的修改全部撤销。

git rm XX 删除XX文件

git remote add origin https://github.com/zongyunqingfeng/testgit 关联一个远程库

git push –u(第一次要用-u 以后不需要) origin master 把当前master分支推送到远程库

git clone https://github.com/zongyunqingfeng/testgit 从远程库中克隆

git checkout –b dev 创建dev分支 并切换到dev分支上

git branch 查看当前所有的分支

git checkout master 切换回master分支

git merge dev 在当前的分支上合并dev分支

git branch –d dev 删除dev分支

git branch name 创建分支

git stash 把当前的工作隐藏起来 等以后恢复现场后继续工作

git stash list 查看所有被隐藏的文件列表

git stash apply 恢复被隐藏的文件，但是内容不删除

git stash drop 删除文件

git stash pop 恢复文件的同时 也删除文件

git remote 查看远程库的信息

git remote –v 查看远程库的详细信息

git push origin master Git会把master分支推送到远程库对应的远程分支上

```
未完待更新...





