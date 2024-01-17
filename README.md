# Datawhale-fastergit-notes
第一章 Git简介（准备工作）  
分布式版本控制系统   
首先git -version查看是否安装，本次使用git版本：2.39.3   
git config --list查看，配置正确   

第二章（核心）要点笔记
1. 可以针对已有的文件夹创建.git进行版本控制，或者直接git clone(个人习惯使用github desktop)   
2. git clone 时，默认clone所有版本，可以在命令最后自定义名字，例子：git clone https://github.com/libgit2/libgit2 iwanttotouchfish（我想摸鱼）    
3. 目录文件有2种，在版本控制中的（可以是未修改、已修改或在暂存区）属于已跟踪，顾名思义，该点啥都会被git发现并记录。不在版本控制中的是未跟踪，个人觉得可以理解为失踪，就是改的乱七八糟甚至删除也无人知晓，在角落瑟瑟发抖。
4. git status可以查看文件状态，如果发现新加的文件没跟踪，可以git add跟踪，注意此时还需要commit才是真正提交了
5.  git add 是个多功能命令：（1）可以用它开始跟踪新文件，（2）把已跟踪的文件放到暂存区，还能用于（3）合并时把有冲突的文件标记为已解决状态等。 将这个命令理解为“精确地将内容添加到下一次提交中”而不是“将一个文件添加到项目中”要更加合适。
6.  在提交之前多用git status查看状态，保证提交的是想要的。
7.  使用.gitignore列出要忽略的文件的模式，避免混乱。参考：https://github.com/github/gitignore    
8.  子目录下也可以有自己额外的 .gitignore 文件，规则只作用于它所在的目录中。
9.  git diff查看具体更改。若要查看已暂存的将要添加到下次提交里的内容，可以用 git diff --staged 命令，比对已暂存文件与最后一次提交的文件差异。
10.  注意：git diff 只显示尚未暂存的改动，而不是自上次提交以来所做的所有改动。所以暂存了所有更新过的文件之后，运行 git diff 后什么也没有。
11.  提交时的是放在暂存区域的快照，任何还未暂存文件的仍然保持已修改状态，没有提交！!
12.  此时使用git commit -a，可以把没暂存的一起提交，省去了git add。但是有时这个选项会将不需要的文件添加到提交中。
13.  git rm移除文件，连带从工作目录中删除指定的文件。
14.  git rm --cached使得git不跟踪，但是文件还在。
15.  文件重命名：git mv file_from file_to
16.  git log查看历史记录，可加入选项 -p 或 --patch ，显示每次提交所引入的差异（按 补丁 的格式输出）。加--stat显示总结信息。--pretty可以使用不同于默认格式的方式展示提交历史。
17.  注意作者是做出修改的人，提交者是点击commit的人。
18.  oneline 或 format 与另一个 log 选项 --graph 结合使用时尤其有用。 如：git log --pretty=format:"%h %s" --graph
19.   可以做出多种限制，如--since 和 --until 按照时间作限制。如git log --since=2.weeks
20.   具体--since, --after仅显示指定时间之后的提交。   --until, --before仅显示指定时间之前的提交。   --author仅显示作者匹配指定字符串的提交。    --committer仅显示提交者匹配指定字符串的提交。   --grep仅显示提交说明中包含指定字符串的提交。   -S仅显示添加或删除内容匹配指定字符串的提交。
21.   重新提交：$ git commit --amend。相当于用一个新的提交替换旧的提交。作用：不会让“啊，忘了添加一个文件”或者 “小修补，修正笔误”这种提交信息弄乱你的仓库历史。
22.   危险！！！撤销修改git checkout -- <file>...你对那个文件在本地的任何修改都会消失——Git 会用最近提交的版本覆盖掉它。
23.   查看远程仓库git remote，定选项 -v，会显示需要读写远程仓库使用的 Git 保存的简写与其对应的 URL。
24.   运行 git remote add 添加一个新的远程 Git 仓库，同时指定一个方便使用的简写。git remote add pb https://github.com/paulboone/ticgit
25.   git fetch origin 会抓取克隆（或上一次抓取）后新的工作，只会将数据下载到你的本地仓库——它并不会自动合并或修改你当前的工作。 不如直接git pull.
26.   git push推到远程仓库，有权限且之前没有人推送过时，这条命令才能生效，避免混乱。
27.   查看远程仓库信息 git remote show
28.   使用git remote rename pb paul来修改一个远程仓库的简写名
29.   移除远程仓库：git remote remove paul
30.   打标签，如V1.0，git tag列出标签
31.   创建附注标签：git tag -a v1.4 -m "my version 1.4" 。包含打标签者的名字、电子邮件地址、日期时间， 此外还有一个标签信息，并且可以使用 GNU Privacy Guard （GPG）签名并验证。
32.   创建轻量标签：git tag v1.4-lw。轻量标签本质上是将提交校验和存储到一个文件中——没有保存任何其他信息。
33.   前面忘记了后面补标签：需要在命令的末尾指定提交的校验和（或部分校验和）：$ git tag -a v1.2 9fceb02
34.   git push 命令并不会传送标签到远程仓库服务器上，在创建完标签后你必须显式地推送标签到共享服务器上：git push origin v1.5。一次推送多个标签：$ git push origin --tags。
35.   删除标签 git tag -d，但是意上述命令并不会从任何远程仓库中移除这个标签。
36.   必须用 git push :refs/tags/ 来更新你的远程仓库，直观：git push origin --delete

第三章 Git分支管理（保证多人协助互不影响）   
1. git branch查看分支，后面加参数的话创建分支
2. git checkout 分支名，切换到分支名    
3. 合并分支：切换到主（要合并到的分支）分支后，git merge 被合并的分支，注意合并之后，被合并的分支仍然存在，但是文件合并了   
4. 合并时，如果主分支和分支都对文件进行修改，就有冲突了，可以使用git status查看状态
5. 冲突之后手动合并、或者用git merge --abort放弃合并，或者使用mergetool（略过，还不会）    
6. 当push本地分支到远程时，先查看远程库的信息：git remote -v（得到origin名字，后面用），同时需要指定具体的本地分支：git push origin master
7. git pull合并分支
8. 删除分支，本地的话git branch -d 接分支名，强行删除用-D, 远程分支用git push origin --delete 接分支名
9. 分支重命名git branch -m 旧的名字 新的名字，push到远程需要+2步骤，1）git push origin newBranchName # 将新的分支推送到远程。2）git push --delete origin oldBranchName # 删除远程的旧的分支


