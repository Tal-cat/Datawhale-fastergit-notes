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

第四章 Git 工具（不常用的常用工具）   
1. fork以下项目作为示范使用https://github.com/datawhalechina-git-samples/app
2. 个人习惯使用Github desktop clone到指定位置
3. git log查看提交日志，commit 后跟的 40 位的字符是 SHA-1 哈希值，以保证数据完整性
4. 查看某一次提交的信息：git show 40位的SHA-1值（也可以缩短，需要确保没有歧义）
5. 确保没歧义时使用简写：git log --abbrev-commit，也可以使用--pretty=oneline简化输出内容
6. 查看本地分支：git branch,* 表示当前工作的分支.
7. 查看远程分支：git branch -r（其实就是remote，加个参数而已）
8. 查看HEAD分支的【最后一次】提交信息：git show stable， branch 的名称和当前目录名称重名会提示ambiguous argument 'stable'，需要使用--明确告知，-- 前面的为 revision 可以是分支，tag 等，-- 后面的为 file 即要操作的文件
9. 查看特定分支SHA-1：git rev-parse 分支名
10. 查看引用日志：git reflog(不就是reference log),记录了最近几个月 HEAD 和分支引用所指向的历史。
11. 查看特定分支的几次前的提交：git show HEAD@{2}就是仓库中 HEAD 在 2 次前的所指向的提交。
12. 交互式暂存：修改大量文件后，希望将改动拆分成多个提交而不是一起提交：git add 后加 -i 或者 --interactive，暂存一部分时在i界面之后选patch（p或者5）
13. 存储修改（比如改累了看别的的时候）：git stash 将未完成的修改保存至一个栈上
14. 找到之前不干了的工作：git stash list，之后使用git stash apply stash@{n}指定去哪个。
15. 彻底不干了：git stash drop 或者 git stash pop
16. 清理目录：git clean会移除未被跟踪的文件，可以考虑执行 git stash --all 来移除所有文件并保存到栈上。
17. 强制清理：git clean -f（force） -d 命令来移除工作目录中所有未追踪的文件以及空的子目录。使用--dry-run或者-n选项来执行命令，【只告诉你会删除什么，而不会真的删除】.
18. 清理漏网之鱼：git clean 命令只会移除没有忽略的未跟踪文件。任何与 .gitignore 或其他忽略文件中的模式匹配的文件都不会被移除。如果也想移除，可以通过增加选项【-x】，增加选项-d删除目录。
19. 交互式删除还是i。
20. 搜索：git grep，默认查找工作目录文件。用-n或者--line-number显示匹配的行号，-c或者--count输出统计信息，-p 或者 --show-function  显示每个匹配字符串所在的方法或函数
21. 日志搜索：git log -S显示内容的新增和删除提交记录，-L进行行日志搜索，展示代码中一行或者一个函数的历史。
22. 搜索无法匹配到你的函数或者方法，使用通过正则表达式：git log -L '/percentileBoundary/',/^}/:src/trace/histogram.go
23. 子模块添加：git submodule add
24. clone 一个含子模块的项目时，默认是不会包含子模块内容的，只有目录。
25. 获取子模块内容：1） git submodule init 初始化本地配置文件。2） git submodule update 则从该项目中抓取所有数据并检出父项目中列出的合适的提交。
26. 更简单的含有子模块复制：git clone --recurse-submodules  https://github.com/datawhalechina-git-samples/app.git new_app2
27. 如果已经克隆了项目但忘记了 --recurse-submodules，那么可以运行 git submodule update --init合并成一步。如果还要初始化、抓取并检出任何嵌套的子模块，请使用简明的 git submodule update --init --recursive。
28. 更新子模块：git submodule update --remote，默认会更新 main 分支，想设置为其他分支在 .gitmodules 文件中设置： git config -f .gitmodules submodule.model.branch stable
29. 很多子模块的话，可以传递想要更新的子模块的名字。如 git submodule update --remote model
30. 打包：git bundle：如果希望这个仓库可以在别处被克隆，增加一个 HEAD 引用。git bundle create repo.bundle HEAD main
31. 打包之后解压：git clone repo.bundle repo
32. 解压缺HEAD：需要在命令后指定一个 -b main 或者其他被引入的分支， 否则 Git 不知道应该检出哪一个分支。

第五章 Git内部原理
1. 围绕本地仓库下名为 .git 的隐藏目录
2. .git目录包含了几乎所有 Git 存储和操作内容。若想备份或复制一个【版本库】，只需将该目录拷贝至另一处即可。
3. 【划重点】里面的config就是修改HTTPS还是SSH连接的！救了大命！
4. 对象存储-objects: 目录下存储三种对象：数据对象（blob，个人理解是对修改信息的描述，如version 1），树对象（tree，树结构，比如文件夹里的文件）和提交对象（commit）。
5. 存储时Git会根据对象内容生成一个【40位数】 SHA-1 哈希值（就是前面一直说的，也叫校验和）。校验和的前两个字符 => 用于命名子目录，余下的 38 个字符 => 用于文件名。将对象内容存储在 子目录/文件名 内。
6. 以根据校验和，查看存储的内容及对象类型。# 查看文件类型：1）git cat-file -t 40fa006a9f641b977fc7b3b5accb0171993a3d31 2）blob；# 查看文件内容：1）git cat-file -p 40fa006a9f641b977fc7b3b5accb0171993a3d31 2）file inside folder1
7. 存储机制：时不时将多个对象打包成一个称为"包文件"。使用git gc进行【手动】打包，git push时也会【自动】打包。pack内出现包文件.pack和包索引.idx文件。
8. 引用-refs：Git把一些常用的 SHA-1 值存储在文件中，用文件名来替代，这些别名就称为引用。有三种引用类型：heads, remotes和tags。
9. HEAD引用2种类型：1）分支级别，.git/refs/heads目录下，记录本地分支的最后一次提交。有多少个分支，就有多少个同名的HEAD引用。文件内容是commitHash。2）代码库级别，.git/HEAD文件，指代当前代码所处的分支；拓展：也可指代commitHash（称为分离HEAD）。
10. 远程引用：.git/refs/remotes 目录下，远程仓库各分支的最后一次提交，文件【只读】。
11. 标签引用：.git/refs/heads 目录下，可以指向任何类型（更多的是指向一个commit，赋予它一个更友好的名字）。文件内容：SHA-1值。
12. stash：.git/refs/stash 文件，指代的是暂存（见前）。
13. 【重点来了】引用规范-config文件：注意这个[remote "origin"] url = https://github.com/datawhalechina/faster-git.git，连不上就改这里！！！
14. config文件 —— 环境变量3种：1）系统变量git config --system；2）用户变量git config --global；3）本地项目变量git config --local，存储位置：.git/config。
15. 配置常用：1）查看所有配置	git config --list；2）配置用户名	git config --global user.name "你的用户名"；3）配置邮箱	git config --global user.email "你的邮箱"。





