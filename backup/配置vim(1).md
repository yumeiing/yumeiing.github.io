# 介绍
这篇博客会介绍一个简单强大的vim配置  
使你的`vim coding`过程更顺心！
## 配置后可以拥有：  
1.方便的文件索引开启  
2.LSP代码自动补全（及各种IDE功能）  
3.内置终端  
4.语法高亮  

> 有人可能会说：这些不是很多vim内置功能吗？
> 其实配置只是其中一小部分，重点是介绍vim各种原生功能的使用:)
> 我觉得vim原生功能已经很完备了，只是体量过大导致一些人没有深入了解这些。
# 配置
vim的**下载**与**保存退出等基础功能**就不再叙述了。  
以下在**vim配置文件**中编辑配置。  
Linux/MacOS中为`~/.vimrc`或`~/.vim/vimrc`，  
Windows为`C:\Users\用户名\_vimrc`。
## 基础配置
vim内置了许多功能，对于基本的文字编辑工作已经够用了。
|名称|含义|我的示例|
|:---|:---|:-------|
|nocompatible|禁用 vi 兼容模式，启用 Vim 特性|set nocompatible|
|syntax|开启语法高亮|syntax on|
|number|显示行号|set number|
|relativenumber|显示相对行号（辅助移动）|set relativenumber|
|cursorline|高亮当前行|set cursorline|
|tabstop|Tab键宽度为 4 空格|set tabstop=4|
|shiftwidth|自动缩进为 4 空格|set shiftwidth=4|
|expandtab| 按 Tab 时插入空格而非制表符|" set expandtab|
|autoindent|自动继承上一行缩进|set autoindent|
|smartindent|智能缩进（针对代码结构）|set smartindent|
|incsearch|搜索时实时高亮匹配项|set incsearch|
|hlsearch|搜索完成后保持高亮|set hlsearch|
|hidden|文件切换不保存|set hidden|
|ignorecase|搜索忽略大小写，但含大写时区分|set ignorecase smartcase|
|scrolloff|距上下边缘保留 3 行视距|set scrolloff=3|
|history|记录更多命令历史|set history=1000|
|encoding|默认编码|set encoding=utf-8|
|mouse|启用鼠标|" set mouse=a|
|filetype|开启文件类型检测、插件及缩进加载|filetype plugin indent on|
|path|用于模糊搜索文件|" set path+=** |
|wildmenu|启用状态栏|set wildmenu|
|showcmd|显示使用按键|set showcmd|
|foldenable|启用折叠|set foldenable|
|foldmethod|语法折叠|set foldmethod=syntax|
|foldlevel|默认全打开|set foldlevel=99|
|foldcolumn|处显示一行|set foldcolumn=1|
## LSP插件配置
这里的LSP插件使用[lsp](https://github.com/yegappan/lsp)。
这是一个**vim9原生语言**编写的插件。
因此其需要自行下载语言服务器[LSP](https://langserver.org/)([clangd](https://clangd.llvm.org/installation)、[python-lsp-server](https://pypi.org/project/python-lsp-server/))。
但是其本体极其轻量，无需额外依赖。
### 插件安装
你有2种选择：
1.使用vim自带的pack插件系统
    * 更轻量
2.使用第三方插件系统
    * 拓展性更强
如果只有简单代码需求建议选vim自带的pack。
如果追求美化与拓展性建议选第三方插件(这里以[vim-plug](https://github.com/junegunn/vim-plug)为例)。
#### pack
先创建`.vim/pack/downloads/`文件夹。
```shell
git clone https://github.com/yegappan/lsp $HOME/.vim/pack/downloads/opt/lsp
# 克隆到本地
vim -u NONE -c "helptags $HOME/.vim/pack/downloads/opt/lsp/doc" -c q
# 创建lsp的help界面
```
进入vim配置文件并写入
```vim
packadd lsp
```
#### vim-plug
添加以下语句
```vim
Plug 'yegappan/lsp'
```
然后输入`:PlugInstall`自动下载。
### 插件配置
添加lsp配置
```vim
" Clangd language server
call LspAddServer([#{
	\    name: 'clangd',
	\    filetype: ['c', 'cpp'],
	\    path: '/usr/local/bin/clangd',
	\    args: ['--background-index']
	\  }])
" Go language server
call LspAddServer([#{
	\    name: 'golang',
	\    filetype: ['go', 'gomod'],
	\    path: '/usr/local/bin/gopls',
	\    args: ['serve'],
	\    syncInit: v:true
	\  }])
```
添加一个LSP可以添加以下参数
|参数|描述|
|:---|:---|
|filetype|LSP服务器支持一种或多种文件类型。 这可以是字符串或列表。要指定多种文件类型，可以使用列表。|
|path|完整路径到LSP服务器可执行文件（不含任何参数）。|
|args|这是一份传递给LSP服务器的命令行参数列表。每个参数是一个独立的列表项目。|
|initializationOptions|用户提供了初始化选项。可能是任何类型的。例如 ，intelephense PHP 语言服务器在这里接受多个选项，包括许可密钥等。|
|customNotificationHandlers|一个可指定用于添加自定义语言服务器通知支持的通知和函数词典。|
|customRequestHandlers|一个请求处理程序和函数的词典，可以指定以增加对自定义语言服务器请求响应的支持。|
|features|一个布尔字典，可以指定用于切换某个LSP提供的内容（折叠、去定义等），这在运行多个服务器于一个缓冲区时非常有用。 |

现在你可以打开一个代码文件试一试啦;)
# 总结
配置还未完成，快捷键配置在下期。待续

