```
git init
git add -A
git commit -m 'Added my project'
git remote add origin git@github.com:sammy/my-new-project.git
git push -u -f origin main

git push -u -f origin main:master 把本地main传到master branch。
git push -u -f origin  :main   :main前有空格，用于删除该branch。

git remote -v 查看远程origin们
```
奇怪，竟然没有验证环节。

另外obsidian git在push时失败，没有obsibian git类命令。

只好在外部用命令同步。
