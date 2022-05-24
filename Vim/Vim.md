
## Vim 基础操作
设置
- 打开搜索高亮：`:set hls`
- 关闭搜索高亮

复制：
-	复制一行：`yy`

粘贴
- 在光标后粘贴：`p`
- 在光标所在位置粘贴：`P`

修改：
- 删除一个字符并进入编辑模式：`s`
- 删除一个单词并进入编辑模式：`cw`
- 删除一个单词（单词可以包括标点符号）并进入编辑模式：`cW`

删除
- 删除同一行内光标和指定字符之间的内容：`dt{char}`
- 删除一个字符：`x`
- 删除一行：`dd`
- 删除光标所在的单词，包括其周围的空格（delete around word）：`daw`
- 删除光标所在的单词，不包含其周围的空格（delete inner word）：`diw`
- 

缩进
- 缩进一行：`>l`
- 缩进从当前行到最后一行间的所有行：`>G`

移动
- 光标移到同一行内下一个字符：`{char}` 处：`f{char}`
- 光标移到上一个单词的开头处：`b`

`q` 模式
- 记录：`q{char}{changes}q`
- 重复：`@{char}`

算数运算：
-	对光标所在数字做加法：`{number}<C-a>`
-	对光标所在数字做减法：`{number}<C-x>`
> 如果执行以上两个命令时光标并不在数字上，Vim 在光标所在行进行搜索，使光标向后移到最近的数字，并进行算术运算。
> 算术运算默认会将有前导 0 的数字当作八进制数，可通过 `set nrformats=`，使 Vim 强制将所有数当作十进制处理。

切换窗口：`<C-w>` + `h/j/k/l`

切换标签页：`gt` 和 `gT`

打开光标下的文件：`gf`

`Insert Mode` 下的临时 `Normal Mode`：`<C-o>`

显示当前编辑文件的完整路径：先按数字 `1`，然后 `ctrl+G`

### 补全

#### 文件名补全

在 `insert` 模式下输入 `<C-x> <C-f>` 即可展开文件路径补全，通过 `<C-n>` 和 `<C-p` 可以上下选择。

## Tips

### 在下方开启终端

在 vim 8 以后的版本，在命令模式输入 `:term` 可开启终端，默认在当前窗口的上面开启。
可通过在 `.vimrc` 中加一行设置让其在下面开启

```vimrc
cnoreabbrev term below term
```

`cnoreabbrev` 中的 `c` 代表命令模式，`nore` 表示 `non recursive`，`abbrev` 当然就是缩写的意思了。
然后就是用 `below term` 替代 `term` 了，相当于一个 alias。

### 改 Vim 的 Tab 键 为 4 个空格。

修改 vim 的配置文件。

````bash
vim /etc/vim/vimrc
````

在文件底部添加以下内容。

````vim
" Tab key == 4 spaces and auto-indent after curly braces in Vim
filetype plugin indent on
" show existing tab with 4 spaces width
set tabstop=4
" when indenting with '>', use 4 spaces width
set shiftwidth=4
" On pressing tab, insert 4 spaces
set expandtab
````

来源：<https://stackoverflow.com/questions/234564/tab-key-4-spaces-and-auto-indent-after-curly-braces-in-vim>

### 复制时不缩进

按 `:` 输入以下命令就不会自动缩进了

```vim
:set paste
```

用以下命令重新开启自动缩进

```vim
:set nopaste
```

## Vim 插件

Vim 插件的集合网站：<https://vimawesome.com>

[vim-plug](https://github.com/junegunn/vim-plug) 是一个 vim 的插件管理器。

使用以下来自 [vim-plug](https://github.com/junegunn/vim-plug) 主页的命令即可安装这个插件管理器。

> 其实也就是下载一个 `plug.vim` 文件放到 `~/.vim/autoload` 目录下而已

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

然后在 `~/.vimrc` 中添加几行代码即可安装各种插件了，比如下面这段

```vim
" Specify a directory for plugins
call plug#begin('~/.vim/plugged')

" Add Plug sentences below. Make sure you use single quotes!

" Shorthand notation; fetches https://github.com/snakemake/snakefmt

Plug 'snakemake/snakefmt'

Plug 'snakemake/snakemake', {'rtp': 'misc/vim'}

Plug 'preservim/nerdtree'

" Initialize plugin system
call plug#end()
```

其中，`call plug#begin('~/.vim/plugged')` 和 `call plug#end()` 标记了载入插件的代码块，`plug#begin()` 函数中的 `'~/.vim/plugged'` 指定了插件的安装目录。

中间的 `Plug` 开头的语句就是载入插件的语句，例如 `Plug 'preservim/nerdtree'` 就是到 Github 上的 `preservim/nerdtree` 仓库去下载安装插件。

所有的引号都必须是单引号，因为在 `.vimrc` 中，双引号是注释的标记。

编写完配置文件后，打开 vim，用以下命令即可进行插件的管理

```vim
:PlugInstall 安装所有插件
:PlugClean 删掉已安装，但不在上面的 Plug 语句列表中的插件
```

### NerdTree


### vim-slime

vim-slime uses vim's definition of paragraph, so when click `<C-c>` `<C-c>` in the middle of these code,

```R
a <- 1

x <- c(1,2,3)▌
y <- c(4,5,6)

z <- 10
```

it will send both `x <- c(1,2,3)` and `y <- c(4,5,6)`.


