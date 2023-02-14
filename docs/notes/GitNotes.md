# GitNotes

- [Git官网](https://git-scm.com/)
- [Git教程|菜鸟教程](https://www.runoob.com/git/git-tutorial.html)
- [Github](https://github.com/)
- [Gitee](https://gitee.com/)



<img src="https://www.runoob.com/wp-content/uploads/2015/02/011500266295799.jpg" style="zoom: 60%;" /> 





**Git上传到远程库完整步骤：**

1. 创建文件夹，初始化本地库`git init`
2. 将文件添加到暂存区`git add 文件名`
3. 将文件提交到本地库`git commit -m "日志信息" 文件名`
4. 给远程库创建别名方便使用`git remote add 别名 远程地址`
5. 将本地分支的内容推送到远程库`git push 别名 分支`





| 命令名称                             | 作用           |
| ------------------------------------ | -------------- |
| git config --global user.name 用户名 | 设置用户签名   |
| git config --global user.email 邮箱  | 设置用户签名   |
| git init                             | 初始化本地库   |
| git status                           | 查看本地库状态 |
| git add 文件名                       | 添加到暂存区   |
| git rm --cached 文件名               | 从暂存区删除   |
| git commit -m "日志信息" 文件名      | 提交到本地库   |
| git reflog                           | 查看历史记录   |
| git reset --hard 版本号              | 版本穿梭       |
|git branch 分支名 |创建分支|
|git branch -v |查看分支|
|git checkout 分支名| 切换分支|
|git merge 分支名 |把指定的分支合并到当前分支上|
|git remote -v |查看当前所有远程地址别名|
|git remote add 别名 远程地址 |起别名|
|git push 别名/链接 分支 |推送本地分支上的内容到远程仓库|
|git clone 远程地址 |将远程仓库的内容克隆到本地|
|git pull 远程库地址别名 远程分支名| 将远程仓库对于分支最新内容拉下来后与当前本地分支直接合并 |
|git remote rm name  |删除远程仓库|
|git remote rename old_name new_name | 修改仓库名 |





- `"C:\Users\当前用户\.gitconfig"`git配置文件

- `ll`查看文件，`ll -a`查看隐藏文件
- `cd .git/`进入文件夹
- `Ctrl + L`清屏
- `.git\HEAD`该文件内容是当前指向的分支
- `.git\refs\heads\`改文件夹存放的是分支指向的版本





**使用GitHub：**

- 在GitHub中创建仓库

- 在本地创建别名

  `git remote add git-demo https://github.com/M-ove/git-demo.git`'
  
  `git remote -v`查看别名
  
- `git push git-demo master`推送master分支到GitHub

- `git pull github-demo master `将远程仓库对于分支最新内容拉下来后与当前本地分支直接合并



- 克隆：`git clone 远程地址`





**ssh免密登录：**

- `ssh-keygen -t rsa -C admin@cgz233.cn` 生成密钥，然后在Github配置

- `git pull git@github.com:cgz233/git-demo.git`拉取
- `git push git@github.com:cgz233/git-demo.git master`推送







