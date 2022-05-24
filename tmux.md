---
tags:
    - tmux
---
tmux 是一个强大的终端复用程序，它可以在一个 ssh 连接中分出多个终端。

## 使用方法

### 快捷键

当身处于一个 tmux 会话中时，可以在按下 `<leader>` 键后，用一些快捷键来进行操作（ `<leader>` 键在默认情况下是 `<ctrl> + b`）。

- `d`：退出当前 session
- `s`：列出所有 session
- `$`：重命名当前 session
- `c`：新建 window
- `x`：删除 window
- `%`：横向分割 window
- `"`：纵向分割 window
- `p`：上一个 window
- `p`：下一个window
- `o`：交换 window 内 pane 的位置
- `<opt> + 1`：切换至横向分屏
- `<opt> + 2`：切换至纵向分屏

### 命令
在 tmux 中，按下 `<leader> :` 可进入类似 vim 的命令模式，一些常用的命令如下（详细的介绍可通过 `man tmux` 然后搜索命令的名字获得）。

- `join-pane`：将别的 window 中的 pane 变成当前 window 中的 pane。[^3]
- `break-pane`：与 `join-pane` 相反。[^4]

## Tips

### 环境变量重复

当时用 `tmux` 命令新建一个会话时，默认载入的是一个 login shell，而不是像 `ssh` 登陆时使用的 non-login shell。[^1]

这个特性使得 `tmux` 在新建会话时会再次加载一些配置文件。如果在加载了 conda 环境后再进入 tmux，`PATH` 环境变量前面会多出一些重复的内容，conda 中的软件无法被正确加载。

要解决这个问题，可在 `~/.tmux.conf` 中添加以下内容。

```
set -g default-command "${SHELL}"
```

然后在终端中运行以下命令刷新配置文件。[^2]

```bash
tmux source ~/.tmux.conf
```

这样用 `tmux` 新建会话，就和运行 `${SHELL}` 程序新建的 shell 没什么区别了。

P.S. `screen` 就没这问题。

## Refs
[^1]: [Why does ‘tmux’ create new windows as login shells by default?](https://superuser.com/questions/968942/why-does-tmux-create-new-windows-as-login-shells-by-default)
[^2]: [Tmux not sourcing my .tmux.conf](https://unix.stackexchange.com/questions/66606/tmux-not-sourcing-my-tmux-conf)
[^3]: [tmux: How to join two tmux windows into one, as panes?](https://stackoverflow.com/questions/9592969/tmux-how-to-join-two-tmux-windows-into-one-as-panes)
[^4]: [How to convert 2 horizontal panes to vertical panes in tmux?](https://superuser.com/questions/493048/how-to-convert-2-horizontal-panes-to-vertical-panes-in-tmux)