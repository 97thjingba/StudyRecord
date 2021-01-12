持续更新

把远程分支拉到本地
**git fetch origin dev（dev为远程仓库的分支名）**

---
查看某个文件的某行代码谁更改的:
**git blame + 文件名**

---
git 批量删除本地分支
**git branch -D branchName**


删除当前分支外的所有分支
**git branch | xargs git branch -d**

删除分支名包含指定字符的分支
**git branch | grep ‘dev*’ | xargs git branch -d**

⬆️ 上面这个命令会删除分支名包含dev字符的分支

--- 

删除所有已经不在远程仓库维护的分支
```git fetch -p && for branch in `git branch -vv | grep ': gone]' | awk '{print $1}'`; do git branch -D $branch; done```


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI1ODA5NjAsMTgxNjQ0NDIwMiw4NzA2NT
U2ODIsMTUwODY1NjQzOF19
-->