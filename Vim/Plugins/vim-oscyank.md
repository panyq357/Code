vim-oscyank 的 Github 页面：<https://github.com/ojroques/vim-oscyank>

vim-oscyank 插件提供一个简单的功能：在 Visual 模式下选中一段文字，然后通过 `:OSCYank` 命令即可将这段文字处理成一个 **OSC** 字符串，输出给终端，然后这段特殊的字符串就能被终端识别，还原其内容，并将其添加进系统的剪贴板。

相比于 vim 自带的 `"+` register，这么做的好处是：可以将通过 ssh 连接的 vim 中的内容**直接**复制到本机的剪切板。（因为 ssh 的本质就是将远程服务器中终端接收到的内容全部送到本机进行处理）

参考
- [使用 vim 跨 ssh 复制文本](https://taoshu.in/vim/vim-copy-over-ssh.html)