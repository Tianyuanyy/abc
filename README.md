# Git 学习笔记

第一/二课，工作区>暂存区>仓库

echo “xxxx">readme.md

git add

git commit

第三课，commti -m

每次提交要说明修改的内容

改名 mv 旧名字 新名字

第四课

比较

git diff    工作区vs暂存区

git diff --staged  暂存区 vs 仓库

历史

git log

\--oneline   --graph

详情

git show

第五课

撤回

git restore 撤销工作区改动

git restore --staged 暂存区撤回工作区

git commit --amend 修改最后一条提交

git reset 撤销

\--soft 暂存区保留，工作区保留  提交漏了文件或提交信息想重写，不想用amend

\--mix（默认）head\~1 暂存区重置，工作区保留

\--hard 暂存区重置，工作区重置，彻底丢失

git revert 新提交一次，用在已推送的提交中

第六课

分支

git branch 本地分支

git switch -c newfile  创建newfile并切换

git switch - 切换上一个分支

git branch newfile 只创建不切换

git branch -m old-name new-name 重命名

git branch -d 删除   -D 强制删除

git merge 合并，需要先切换到main



