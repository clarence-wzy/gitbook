### Git

常见命令：

```markdown
添加： 
```



#### reset

**回退文件**（未add撤销修改）：git reset [file]



**回退版本**：git reset [model] [commit_id | origin/xxx]

model：
- --mixed：保留修改文件，只是将 git commit、index 信息回退到了某个版本
- --soft：保留修改文件，只回退到commit信息到某个版本（不涉及index的回退，如果还需要提交，直接commit即可）
- --hard：修改文件会清空，完全回退到某个版本



#### rebase

**由于推送需要强推，存在一定风险，不推荐主分支操作，通常用于开发分支**

```markdown
合并从HEAD开始的n个commit ：git rebase -i HEAD~[n]
合并到commit_id前(不包括commit_id本身)所有commit ： git rebase -i [commit_id]

进入command编辑：操作每一个commit_id，但不处理commit_msg，比如pick-不修改、squash-该提交内容合并到上一个提交、fixup-废弃该commit_msg但提交内容不丢失会合并，等等
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase

保存后，会进入另一个command，这里才是调整commit_msg，不需要的就"#"，该修改commit_msg就修改
最后，推送时需要强推：git push --force
```

- 取消：git rebase --abort

