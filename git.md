# git 常用命令

显示[指定文件]版本记录

```
git log  [path]
```

显示版本[HEAD]的[指定文件]变更记录

```
git show  [HEAD] [path]
```

撤销[指定文件]暂存区更改

```
git reset HEAD [path]
```

还原[指定文件]更改

```
git checkout [path]
```

切换到分支[branch]

``` 
git checkout [branch]
```

创建分支[branch]

```
git branch [branch]
```

删除分支[branch]

```
git branch -D [branch]
```

添加[指定文件]到暂存区

```
git add [path]
```

添加版本并填写标题[text]

```
git commit -m [text]
```

回滚到[HEAD]版本,保留之前的更改

```
git reset [HEAD]
```
从[branch]分支合并代码

```
git merge [branch]
```

操作最后两次提交信息

```
git rebase -i HEAD~2 
```

修改上次的提交信息

```
git commit --amend
```

继续下一步直至操作完成

```
git rebase --continue
```

显示文件的修改记录

```
git log [path]
// 额外输出变更内容
git log -p [path]
```
比较文件变化

```
// 常用 比较文件2个版本之间的变更内容
git diff [[commit1][commit2]]] [path]
// 比较文件当前版本和倒数第3版本之间的变更内容
git diff HEAD HEAD~3 [path]
```

# 应用示例
