---
export_on_save:
 html: true
---
# Git的日常使用
### 1. 删除已经上传到远程库的文件
> 1.  git rm -r --cached dir_name &nbsp; *删除已经提交的文件或者文件夹*
> 2. git commit -m 'Delte someone file'
> 3. git push 

### 2. 删除本地分支
> * git branch -d \<BranchName> &nbsp; *指定分支名称*

### 3. 删除远程分支
> * git push origin --delete \<BranchName> &nbsp; *远程分支名称*

### 4. 创建本地分支并切换到新的分支
> * git push origin \<BranchName>:\<BranchName> &nbsp;  *可使用与本地分支相同的名字*

### 5. 拉取特定远程分支内容
> * git fetch \<RemoteName> \<BranchName> &nbsp; *拉去特定远程仓库的某一分支*  
>> 并且与当前本地分支合并：
> * git merge  \<RemoteName>/\<BranchName> &nbsp; *并与当前本地分支合并*

### 6. 强行拉去分支并覆盖本地文件
> 1. git fetch --all 
> 2. git reset --hard origin/master 
> 3. git pull

### 7. 查看本地分支与远程分支之间的关系
> * git branch -vv  
>> 设置远程跟踪 :
> * git branch --set-upstream-to=origin/\<RemoteName> \<BranchName> &nbsp;   _设置本地分支\<BranchName>跟踪origin\<RemoteName>远程分支_

### 8. 选择一个commit,合并进当前分支
> * git cherry-pick \<commit_ID>

### 9. 查看信息
>  显示有变更的文件:  
>  * git status   
> 
> 显示当前分支的版本历史:  
>  * git log
> 
> 显示commit历史，以及每次commit发生变更的文件:  
> * git log --stat
> 
> 搜索提交历史，根据关键词:
> * git log -S \<keyword>
> 
> 显示暂存区和工作区的差异:
> * git diff  
> 
> 显示暂存区和上一个commit的差异:
> * git diff --cached \<file>
> 
> 显示工作区与当前分支最新commit之间的差异:
> * git diff HEAD

### 10. 撤销
> 恢复暂存区的指定文件到工作区: 
> * git checkout \<file>
> 
> 恢复暂存区的所有文件到工作区:
> * git checkout .
>  
> 重置暂存区与工作区，与上一次commit保持一致:
> * git reset --hard
> 
>重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致:
> * git reset --hard \<commit>
> 
> 新建一个commit，用来撤销指定commit,后者的所有变化都将被前者抵消，并且应用到当前分支:
> * git revert \<commit>
> 

