## Git 常用命令
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

撤回上次 commit 的操作，并重新同步到 github。
```bash
git reset HEAD~1
# 修改完以后
git push -f
```

## Github 相关
### token
```zsh
Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
```

当出现类似上面的提示时，说明当前的操作需要 Github 的 token。

在 Github 设置中的 [Personal access tokens 页面](https://github.com/settings/tokens)生成一个 token，然后把 token 当作密码输入就可以了。[^3]

## 参考
[^1]: [git status 显示中文和解决中文乱码](https://blog.csdn.net/u012145252/article/details/81775362)
[^2]: [git commit --amend修改push到远程分支的提交](https://blog.csdn.net/ecjtuhq/article/details/80358656)
[^3]: [Support for password authentication was removed ....](https://stackoverflow.com/questions/68775869/support-for-password-authentication-was-removed-please-use-a-personal-access-to)