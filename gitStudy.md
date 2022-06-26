# git Study

## git
git 下载地址：http://git-scm.com/downloads  开源的分布式版本控制软件  
gitconfig 配置文件，当前电脑System 最低级 etc/gitconfig，当前用户global 中级 ~/.gitconfig，global,当前项目 最高级.git/gitconfig，global
git config --global user.name "Dai" ; git config配置文件 --global 全局 user.name 用户名 user.email 邮箱 
GitHub https://github.com/ 开源的软件项目托管平台
`git --version` 查看版本 2.32.0.windows.2
`git --help` 查看帮助


## 初始化
`git init` 在本地项目所在文件夹初始化本地库，缺省创建master分支，出现.git

## 文件过滤
.gitignore 写入过滤规则。在线文档 https://github.com/github/gitignore,原则：忽略os自动生成文件，如缩略图，忽略编译中间文件，忽略带有敏感信息的配置信息
*.class
*.log

## 提交到暂存区 
`git add 目录 或者 文件`
`git add .`  添加所有修改和新增的到暂存区（不包括删除）
`git add -u` 添加所有修改的到暂存区
`git add -A` 添加所有修改和新增的到暂存区（包括删除）

## 提交到版本库
`git commit 目录 或者 文件` 将缓存区的内容添加到本地仓库 参数-m表示提交描述 如果不加-m会默认打开 一个描述文件,-a 能跳过 git add直接commit，可以使用-am

## 查看状态
`git status -s`查看本地工作区、暂存区中文件的修改状态 -s参数表示查看简要信息，状态 A 表示新增 M 表示修改 D 表示删除
`git diff`查看git status的详细信息，尚未缓存的 git -diff ，已缓存的 git diff --cached，查看已缓存与未git缓存的所有改动 git diff HEAD

## 版本回退
`git reset HEAD -- gitOne.txt` 文件名/文件夹回退暂存区,取消已缓存的内容，即取消之前的git add
`git reset --hard HEAD^` 回退版本库,HEAD^表示上一个版本，2个^表示上上个版本 HEAD~100 上100个版本，也可以指定 commit id，通过git reflog得到
`git checkout -- file` 把改文件在工作取得修改全部撤销,让文件回到最后一次 git commit 或 git add时的状态



## 删除
`git rm file` 从版本库中删除文件，如果删除之前修改过并且已经放到暂存区的话，则必须使用强制删除-f命令 git rm -f file,然后commit，如果仅删除缓存区 git -rm --cached file
`git checkout -- file` 删除错误恢复文件,用版本库的文件替换工作区的版本
`git rm -r directory` 递归删除

## 移动/重命名 文件/目录/软连接
`git mv 旧路径+文件名 新路径+文件名` 

## 远程仓库
`git remote add origin https://github.com/DaiHongquan/gitLearn.git` 将本地仓库与远程仓库关联  
`git remote -v` 查看远程库信息
推送
`git push -u origin master` 将本地仓库内容推送到远程库 -u指定默认主机 即默认远程仓库分支，后续即可使用 git push 
`git fetch origin issue12` 从远程库更新,从远程库issue12更新到本地库issue12
`git pull origin issue13`  远程获取并更新,相当于 git fetch + git merge
## 查看日志
git log -p issue12..origin/issue12  -p选项展开显示每次提交的内容差异   git log --pretty=oneline 简化输出  --abbrev-commit 
`git reflog` 全部日志

## 克隆
克隆前先生成SSH Key保证连接
`ssh-keygen -t -rsa -C "github邮箱"`
选择路径，输入自定义ssh密码，确认ssh密码，将id_rsa.pub的内容复制到github SSH keys上保存
`git clone https://github.com/DaiHongquan/gitLearn.git 项目名称` 
DaiHongquan/gitLearn.git你的github项目地址，如果带 项目名称会新建一个此文件名的文件夹，否则，在当前目录
  
## 分支
`git branch -a` 查看所有分支，当clone后只能看到主分支时，使用非常有用，然后切换到对应分支即可操作，*表示当前分支
`git bracnh` 查看本地所有分支
`git checkout 分支名` 切换分支,加上 `-b` 新建并切换分支
`git merge origin/issue12` 合并分支，将 origin/issue12 分支合并到当前分支
`git branch -d 分支名`  删除分支，例如git branch -d dev 
`git merge --no-ff` 合并分支，需要手动解决冲突  <<<<< ====== >>>>>  记得使用 --no-ff，作为一个新的提交
feature_* 用来开发新特性
release_* 在合并的dev上开发小特性（生产环境的准备工作）
hotfix_* 修复bug
git branch --set-upstream dev origin/dev 设置远程库关联分支

## 版本标签
`git tag -a 1.0.0 -m "标签说明"`   git tag 标签名，标签默认打在最新提交的commit id上,`git tag 标签名 （commit id）` git tag v0.8 e871a66,git tag查看标签
`git show` 标签名 查看标签信息
`git tag -d v0.8` 删除标签，删除远程库标签要先删除本地，然后 g`it push origin :refs/tags/v0.9`
`git push origin` 标签名  推送本地标签到远程，也可以一次推送 `git push origin --tags`







