## 简介

[gruvbox](https://github.com/morhetz/gruvbox) 是一个广受好评的 vim 配色主题

本文分为三个部分：
- 如何给 vim 安装 gruvbox 主题
- 如何给 iterm2 安装 gruvbox 主题
- 如何给让 tmux 中的 vim 的 gruvbox 主题能正常使用

## 给 Vim 安装 gruvbox 主题

原始的 gruvbox 主题已经很多年没更新了，存在一些未解决的问题（比如 :term 里的颜色不对）

一些 fork 出来的版本修复了一些问题，比如 [gruvbox-community/gruvbox](https://github.com/gruvbox-community/gruvbox)。

安装就像安装普通插件一样，将下面这行添加到 vim-plug 的插件列表中。

```vimrc
Plug 'gruvbox-community/gruvbox'
```

然后在 `.vimrc` 中添加这些语句

```vimrc
" 光标所在行高亮
set cursorline
" 使颜色正确
set termguicolors
" 启用颜色主题
colorscheme gruvbox
" 启用暗色模式
set background=dark
```

## iterm2 设置

在 iterm2 的 [Online Gallery](https://iterm2colorschemes.com) 中，也有 `gruvbox-dark` 主题，下载下来，然后在 iterm2 > preferences > profiles > color 中导入使用即可

## tmux 设置

在 `.tmux.conf` 中添加以下两行，即可使 tmux 的颜色正确显示。（需要 tmux 版本在 3.2 及以上）[^1]

```txt
set -g default-terminal "xterm-256color"
set -as terminal-overrides ",xterm-256color:RGB"
```

第二行是启用 tmux 的 RGB 转换功能，增加其兼容性。很多终端模拟器都能实现真彩色[^2]，但实现方式似乎不尽相同，只有少数能通过 [24-bit-color.sh](https://github.com/tmux/tmux/blob/master/tools/24-bit-color.sh) 脚本的检测的终端模拟器（比如 iterm2 和 mintty），才不需要转换，否则就得加上这一行。


[^1]: [Tmux 24bit True Color Support](https://ttys3.dev/post/tmux-24bit-true-color-support/)
[^2]: [Colours in terminal](https://gist.github.com/CMCDragonkai/146100155ecd79c7dac19a9e23e6a362)
