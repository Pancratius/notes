微软pownertoys 可以改键位映射

## 插件市场
https://vimawesome.com/

借助 vim-plug 来安装其他vim 插件


## 普通模式
### 控制方向
h     左移
l     右移
j     下移
k     上移
数字+hljk           表示一次跳多少位
w                   表示按单词进行后跳
b                   表示按单词进行前跳
e                   表示按单词调至单词结尾
gg                  跳至第一行开头
G                   跳至最后一行开头
Ctrl+U              向上翻页
Ctrl+D              向下翻页
Ctrl + 左右箭头     表示按整儿单词跳转操作



### 查找对象
f+查找对象           表示查找，但是只能在当前行



### 复制、黏贴、删除、撤销
yy                  复制当前行
yaw                 复制整个单词
y4l                 从当前位置起，向右复制了4位
yft                 在当前行，从当前位置开始复制到第一个t，所有内容
p                   黏贴
d                   d操作与y一直，y相关的操作，d都可以
dd 或 cc            删除当前行
u                   撤销操作


### 编辑
i（input,当前光标） 或 o 或 a（append，当前光标之后）， 加上Shift 表示光标升级为行的感念
caw                 表示删除整个单词，并进入编辑模式
c                   表示修改
c4l                 删除右边4位，然后进入编辑模式
c+对象              表示从当前光标到对象都删除，并进入编辑模式

## 编辑模式
常规操作文本，跳过



## 命令模式
### 进入
按： 进入命令模式

### 退出
两个命令都可以进行保存并退出
:wq                 无论是否修改过，强制更新（例如操作时间）一下
:x                  如果没有修改过，则不会进行强制更新
:set number         临时显示行号

## 可视模式
### 进入
在普通模式下，按v进入可视模式， 在该模式下，可以使用普通模式相关命令


## 查找
在normal模式下按下/即可进入查找模式，输入要查找的字符串并按下回车。 Vim会跳转到第一个匹配。按下n查找下一个，按下N查找上一个。

Vim查找支持正则表达式，例如/vim$匹配行尾的"vim"。 需要查找特殊字符需要转义，例如/vim\$匹配"vim$"。

注意查找回车应当用\n，而替换为回车应当用\r（相当于<CR>）。

### 大小写敏感查找
在查找模式中加入\c表示大小写不敏感查找，\C表示大小写敏感查找。例如：

/foo\c
将会查找所有的"foo","FOO","Foo"等字符串。

### 大小写敏感配置
Vim 默认采用大小写敏感的查找，为了方便我们常常将其配置为大小写不敏感：

" 设置默认进行大小写不敏感查找
set ignorecase
" 如果有一个大写字母，则切换到大小写敏感查找
set smartcase 
将上述设置粘贴到你的~/.vimrc，重新打开Vim即可生效。

## 查找当前单词
在normal模式下按下*即可查找光标所在单词（word）， 要求每次出现的前后为空白字符或标点符号。例如当前为foo， 可以匹配foo bar中的foo，但不可匹配foobar中的foo。 这在查找函数名、变量名时非常有用。

按下g*即可查找光标所在单词的字符序列，每次出现前后字符无要求。 即foo bar和foobar中的foo均可被匹配到。

## 其他设置
:set incsearch 可以在敲键的同时搜索，按下回车把移动光标移动到匹配的词； 按下 Esc 取消搜索。

:set wrapscan 用来设置到文件尾部后是否重新从文件头开始搜索。

## 查找与替换
:s（substitute）命令用来查找和替换字符串。语法如下：

:{作用范围}s/{目标}/{替换}/{替换标志}
例如:%s/foo/bar/g会在全局范围(%)查找foo并替换为bar，所有出现都会被替换（g）。

作用范围
作用范围分为当前行、全文、选区等等。

当前行：

:s/foo/bar/g
全文：

:%s/foo/bar/g
选区，在Visual模式下选择区域后输入:，Vim即可自动补全为 :'<,'>。

:'<,'>s/foo/bar/g
2-11行：

:5,12s/foo/bar/g
当前行.与接下来两行+2：

:.,+2s/foo/bar/g
## 替换标志
上文中命令结尾的g即是替换标志之一，表示全局global替换（即替换目标的所有出现）。 还有很多其他有用的替换标志：

空替换标志表示只替换从光标位置开始，目标的第一次出现：

:%s/foo/bar
i表示大小写不敏感查找，I表示大小写敏感：

:%s/foo/bar/i
# 等效于模式中的\c（不敏感）或\C（敏感）
:%s/foo\c/bar
c表示需要确认，例如全局查找"foo"替换为"bar"并且需要确认：

:%s/foo/bar/gc
回车后Vim会将光标移动到每一次"foo"出现的位置，并提示

replace with bar (y/n/a/q/l/^E/^Y)?
按下y表示替换，n表示不替换，a表示替换所有，q表示退出查找模式， l表示替换当前位置并退出。^E与^Y是光标移动快捷键，参考： Vim中如何快速进行光标移动。

## 高亮设置
### 高亮颜色设置
如果你像我一样觉得高亮的颜色不太舒服，可以在 ~/.vimrc 中进行设置：

highlight Search ctermbg=yellow ctermfg=black 
highlight IncSearch ctermbg=black ctermfg=yellow 
highlight MatchParen cterm=underline ctermbg=NONE ctermfg=NONE
上述配置指定 Search 结果的前景色（foreground）为黑色，背景色（background）为灰色； 渐进搜索的前景色为黑色，背景色为黄色；光标处的字符加下划线。

更多的CTERM颜色可以查阅：http://vim.wikia.com/wiki/Xterm256_color_names_for_console_Vim

### 禁用/启用高亮
有木有觉得每次查找替换后 Vim 仍然高亮着搜索结果？ 可以手动让它停止高亮，在normal模式下输入：

:nohighlight
" 等效于
:nohl
其实上述命令禁用了所有高亮，只禁用搜索高亮的命令是:set nohlsearch。 下次搜索时需要:set hlsearch再次启动搜索高亮。

延时禁用
怎么能够让Vim查找/替换后一段时间自动取消高亮，发生查找时自动开启呢？

" 当光标一段时间保持不动了，就禁用高亮
autocmd cursorhold * set nohlsearch
" 当输入查找命令时，再启用高亮
noremap n :set hlsearch<cr>n
noremap N :set hlsearch<cr>N
noremap / :set hlsearch<cr>/
noremap ? :set hlsearch<cr>?
noremap * *:set hlsearch<cr>
将上述配置粘贴到~/.vimrc，重新打开vim即可生效。

### 一键禁用
如果延时禁用搜索高亮仍然不够舒服，可以设置快捷键来一键禁用/开启搜索高亮：

noremap n :set hlsearch<cr>n
noremap N :set hlsearch<cr>N
noremap / :set hlsearch<cr>/
noremap ? :set hlsearch<cr>?
noremap * *:set hlsearch<cr>

nnoremap <c-h> :call DisableHighlight()<cr>
function! DisableHighlight()
    set nohlsearch
endfunc
希望关闭高亮时只需要按下 Ctrl+H，当发生下次搜索时又会自动启用。