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

git switch -c newfile  创建newfile并切换

git switch - 切换上一个分支

git branch 本地分支

git branch newfile 只创建不切换

git branch -m old-name new-name 重命名

git branch -d 删除   -D 强制删除

合并

git merge 合并，需要先切换到main

git merge --no-ff 不快速合并，在lg中体现曾有分支，而不是直线

git merge --abort 合并出问题后放弃

git merge --squash fenzhi 把分支所有改动压成一台条待提交改动

第七课
冲突的解决
git status之后打开冲突的文件修改
# 学习笔记

今天学了 Git 的分支操作。

<<<<<<< HEAD
分支在 Git 里成本很低，可以放心多用。（现在分支）
=======
每个功能都应该开一个独立的 feature 分支。（要合并分支）
>>>>>>> feature/branch-notes

git add <file>
git commit 

如果不想合并了
git merge --abort

第八课
忽略跟踪文件的规则文件 .gitignore
写法	含义
*.log	匹配任意层级的 .log 文件
/dist/	只匹配仓库根目录下的 dist 目录
dist/	匹配任意层级的 dist 目录
**/temp	任意层级（** 显式表示多层）
!important.log	反向例外：不忽略这个文件
doc/*.md	* 不跨目录，只匹配 doc 的直接子文件
doc/**/*.md	匹配 doc 下任意深度的 md
# 注释	注释行
空行	忽略

第九课
建立ssh
# 1. 生成密钥对（ed25519 是当前推荐算法）
ssh-keygen -t ed25519 -C "你的邮箱"

# 提示 Enter file in which to save the key 时，直接回车，用默认路径
# 提示 Enter passphrase 时，可以留空（方便），也可以设置（更安全，但每次用要输）

# 2. 查看生成的文件
ls ~/.ssh
# 应该看到：id_ed25519（私钥，绝不外传）和 id_ed25519.pub（公钥）

# 3. 复制公钥内容
cat ~/.ssh/id_ed25519.pub
# 输出形如：ssh-ed25519 AAAAC3NzaC1lZDI1NTE5... 你的邮箱

# 4. 打开平台设置页，粘贴公钥
#    GitHub: Settings → SSH and GPG keys → New SSH key
#    Gitee:  设置 → SSH 公钥 → 添加公钥
#    标题随便取（如 "我的笔记本"），Key 处粘贴刚复制的内容

# 5. 验证
ssh -T git@github.com       # GitHub
ssh -T git@gitee.com        # Gitee

仓库建立追踪关系 git remote
# 1. 关联远程仓库，命名为 origin
git remote add origin git@github.com:yourname/git-lab.git

# 2. 确认关联成功
git remote -v
# 输出：
# origin  git@github.com:yourname/git-lab.git (fetch)
# origin  git@github.com:yourname/git-lab.git (push)

# 3. 推送本地 main 分支，并建立追踪关系
git push -u origin main

以后直接 git push、git pull 就可以了，不用每次写 origin main。

第十课
pull = fetch + merge
git fetch：把远程的最新提交下载到本地，但不改动你的工作区和当前分支。它只更新 origin/main 这个指针

git branch -vv   # 本地分支及其上游（最有用的一个）
* main 1613092 [origin/main] docs:forget2

冲突的解决和merge一样

第十一课
团队协作规范
一个md文件
观察  grist

第十二课
stash 临时保存未完成的改动-工作区
git stash push -m "企业清单导入：表单校验写到一半"
git stash pop                     # 取出最近的，并从栈中删除
git stash apply                   # 取出但保留在栈中（可以反复 apply）
git stash drop stash@{0}          # 删除指定的一条
git stash clear                   # 清空全部（危险，不可恢复）

 cherry-pick 在分支之间搬运指定提交 产生的是新提交
# 把 main 上的那一条提交搬过来
git cherry-pick a1b2c3d
冲突
--abort
--continue

merge vs rebase（一条直线，被搬动的提交哈希全部改变）
未推送的提交上，用git rebase -i  这是整理历史的利器
冲突
--abort
--continue

git tag 打标签
# 轻量标签（只是一个指向提交的引用）
git tag v1.0.0

# 附注标签（包含打标签的人、时间、说明 —— 发布版本应该用这个）
git tag -a v1.0.0 -m "首个正式版本：完成企业清单导入与导出"
