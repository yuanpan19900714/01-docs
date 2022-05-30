# 查看和修改本地用户名

在GitBase下执行， `git config user.name` 查看用户名，`git config user.email` 查看邮箱

在GitBase下执行， `git config --global user.name xxx` 修改用户名，`git config --global user.email xxx` 修改邮箱

# 查看某个人创建的所有分支
在GitBase下执行
```
git for-each-ref --format='%(committerdate)%09 %(authorname)%09 %(refname)'|sort -k5n -k2M -k3n -k4n|grep author
```