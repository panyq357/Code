## 常用命令
修改默认 branch 的名字
```
git config --global init.defaultBranch main
```

设置用户名和 E-mail
```bash
git config --global user.name YOURUSERNAME
git config --global user.email YOUREMAIL
```

显示中文字符。[^1]
```bash
git config --global core.quotepath false
```

Github SSH 连通测试
```bash
ssh -T git@github.com
```

修改上次 `push` 的提交信息。[^2]
```bash
git commit --amend
git push --force-with-lease origin main
```

然后远程仓库中的提交信息就被修改了。

## 参考
[^1]: [git status 显示中文和解决中文乱码](https://blog.csdn.net/u012145252/article/details/81775362)
[^2]: [git commit --amend修改push到远程分支的提交](https://blog.csdn.net/ecjtuhq/article/details/80358656)