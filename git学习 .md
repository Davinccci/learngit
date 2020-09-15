__git 学习__
=========

### 1.创建版本库
* 建立新仓库: `git init`
(注意，必须要在git目录里进行)`cd learngit`
* 将文件添加到仓库 :`git add`
```
	git add readme.txt
```

（新建文件夹 `touch` ）

- 将文件提交到仓库：`git commit`

```
	git commit -m "wrote a readme file"
```
### 2.时光机穿梭
* 掌握仓库状态：`git status`
* 查看修改内容：`git diff <file>`
* 查看修改历史：`git log`
* 版本回退: `git reset --hard HEAD^`返回上一层，返回n层：`HEAD～n`
(`cat <file >`显示文件)
版本回退后，工作区文件就会被修改为之前的文件。
* 查看命令历史 ：`git reflog`记录所有的命令，当你后悔时可以用
### 3.工作区和暂存区
>工作区：在电脑里能看到的目录
>版本库：`.git`里的东西，包括暂存区
>暂存区：使用`git add `命令后，即将该文件提交到暂存区
>使用`git commit`即是将暂存区里的所有东西一次性提交上去

### 4.撤销修改
* 丢弃工作区的修改：`git checkout -- <file>`
>有两种情况：
>1.`file`自修改后还没有被放到`暂存区`，现在，撤销修改就回到和`版本库`一模一样的状态；
> 		即上一次`git commit`后的状态
>2.`file`已经添加到`暂存区`后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
>		即上一次`git add`后的状态

* 丢弃暂存区的修改（即已经`git add `）用：`git reset HEAD <file>`
>`git reset HEAD <file>`可以将暂存区的修改撤销掉
>之后就可以再尝试丢弃工作区的修改

* 若已经上传到了版本库
>直接版本回退 `git reset --hard HEAD^`

### 5.删除文件
>linux命令：`rm <file>`删除文件
>版本库中也要删除：`git rm`，并`git commit`
>删错了要复原：`git checkout -- <file>`即同撤销工作区的修改
************************************************

远程仓库
----------------
>* 关联远程库：`git remote add origin git@server-name:path/repo-name.git`
>* 关联后第一次推送：`git push -u origin master`
>* 之后推送：`git push origin master`

* 从远程库克隆
>* git clone `git clone git@github.com:Davinccci/gitskills.git`

分支管理
-------
1. 创建分支 `git branch dev`

2. 切换分支 `git checkout dev`   或`git switch`

3. 查看当前分支`git branch`

   ```  
   git branch 会列出当前所有分支，当前分支前面会标一个‵*‵
   ```

4. 在dev分支的操作若切换回master分支会全部撤回

5. 分支合并到当前分支`git merge dev`

6. 删除分支 `git branch -d dev` 

####    解决冲突

#### 分支管理策略

1. 重新将某分支commit到当前分支`git merge --no-ff -m"xxx" dev`


```策略：
![0](/home/li/%E6%A1%8C%E9%9D%A2/0.png在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

所以，团队合作的分支看起来就像这样：

```

#### ![0](/home/li/git/learngit/git%E5%AD%A6%E4%B9%A0%20.assets/0.png)

#### bug分支

1. 每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。