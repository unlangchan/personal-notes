git log  [path] 显示[指定文件]版本记录
git show  [HEAD] [path] 显示版本[HEAD]的[指定文件]变更记录
git reset HEAD [path] 撤销[指定文件]暂存区更改
git checkout [path] 还原[指定文件]更改
git checkout [branch] 切换到分支[branch]
git branch [branch] 创建分支[branch]
git branch -D [branch] 删除分支[branch]
git add [path] 添加[指定文件]到暂存区
git commit -m [text] 添加版本并填写标题[text]
git reset [HEAD] 回滚到[HEAD]版本,保留之前的更改
git merge [branch] 从[branch]分支合并代码
git rebase -i HEAD~2 操作最后两次提交信息
git commit --amend 修改上次的提交信息
git rebase --continue 继续下一步直至操作完成