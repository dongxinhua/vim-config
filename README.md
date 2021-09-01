# vim-config

​		本人前端开发者，学习使用 Vim 进行前端开发，由于Vim本身并没有一些很好的能力，比如代码提示、保存格式化代码等等；因此需要进行各种配置，比如配置.vimrc、安装插件等等，为了后续更换电脑可以快速进行Vim配置，在此写下具体操作，方便后续查看。

## 插件安装

​		想要让自己的Vim功能更加强大，那么必须安装各种插件进行配置。进而我们需要一个插件管理工具进行管理，这里我使用的是 vim-plug， [vim-plug GitHub](https://github.com/junegunn/vim-plug).

​		安装 vim-plug 很方便，查看 github README 即可，本人使用的 MacBook Pro ，具体安装命令：

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

​		使用方法： .vimrc 配置如下

```vimrc
" Specify a directory for plugins
" - For Neovim: stdpath('data') . '/plugged'
" - Avoid using standard Vim directory names like 'plugin'
call plug#begin('~/.vim/plugged')

" Make sure you use single quotes

" 这里填写自己要安装的插件
" 比如：目录树
Plug 'scrooloose/nerdtree'

" Initialize plugin system
call plug#end()
```

​		这样，我们就可以安装自己想要安装的插件了。

## coc-nvim

**Make your Vim/Neovim as smart as VSCode.**

为了实现一系列的功能，本人使用的是 coc-nvim 这款插件, [con-nvim GitHub](https://github.com/neoclide/coc.nvim).

为什么使用它？去 github 看看呀！

使用 coc-nvim 需要有node环境  node.js >= 12.12

然后在 .vimrc 中配置

```
" 本人使用的是第一种方法
" Use release branch (recommend)
Plug 'neoclide/coc.nvim', {'branch': 'release'}

" Or build from source code by using yarn: https://yarnpkg.com
Plug 'neoclide/coc.nvim', {'branch': 'master', 'do': 'yarn install --frozen-lockfile'}
```

con-nvim 可以管理安装自己的插件

```
// 这是 Vim 命令哦
:CocInstall coc-json coc-tsserve
```

本人安装的插件

+ coc-syntax
+ coc-snippets
+ coc-prettier
+ coc-html-css-support
+ coc-html
+ coc-highlight
+ coc-eslint
+ coc-cssmodules
+ coc-vimlsp
+ coc-vetur
+ coc-tsserver
+ coc-rome
+ coc-json
+ coc-css

更多查看：[coc-extensions GitHub](https://github.com/neoclide/coc.nvim/wiki/Using-coc-extensions).

## .vimrc 配置文件

```vimrc
syn on                      "语法支持

"common conf {{             通用配置
set ai                      "自动缩进
set bs=2                    "在insert模式下用退格键删除
set showmatch               "代码匹配
set laststatus=2            "总是显示状态行
set expandtab               "以下三个配置配合使用，设置tab和缩进空格数
set shiftwidth=2
set tabstop=2
" set cursorline              "为光标所在行加下划线
set number                  "显示行号
set autoread                "文件在Vim之外修改过，自动重新读入

set ignorecase              "检索时忽略大小写
set fileencodings=utf-8,gbk "使用utf-8或gbk打开文件
set hls                     "检索时高亮显示匹配项
set helplang=cn             "帮助系统设置为中文
set foldmethod=syntax       "代码折叠
"}}

" conf for tabs, 为标签页进行的配置，通过ctrl h/l切换标签等
let mapleader = ','
nnoremap <C-l> gt
nnoremap <C-h> gT
nnoremap <leader>t : tabe<CR>

"conf for plugins {{ 插件相关的配置
"状态栏的配置 
"powerline{
set guifont=PowerlineSymbols\ for\ Powerline
set nocompatible
set t_Co=256
let g:Powerline_symbols = 'fancy'
"}
"pathogen是Vim用来管理插件的插件
"pathogen{
"call pathogen#infect()
"}

"}}

" Specify a directory for plugins
" - For Neovim: stdpath('data') . '/plugged'
" - Avoid using standard Vim directory names like 'plugin'
call plug#begin('~/.vim/plugged')

" Make sure you use single quotes

" 目录树
Plug 'scrooloose/nerdtree'

" Visual-Multi 多个光标位置
Plug 'mg979/vim-visual-multi', {'branch': 'master'}

" Use release branch (recommend) 安装 coc.nvim
Plug 'neoclide/coc.nvim', {'branch': 'release'}

" Initialize plugin system
call plug#end()

" 目录树配置
" autocmd VimEnter * NERDTree
map <F4> :NERDTreeMirror<CR>
map <F4> :NERDTreeToggle<CR>

" 切换分屏映射
nnoremap <C-Tab> <C-W>w
nnoremap <C-S-Tab> <C-W>W
```

## coc.settings.json

这个文件的配置，是学习[b站up主TheCW](https://space.bilibili.com/13081489?spm_id_from=333.788.b_765f7570696e666f.1)的配置.

可在 vim 环境下通过`:CocConfig`进行查看配置并保存.

```json
{
  "coc.preferences.semanticTokensHighlights": false,
  "coc.preferences.enableFloatHighlight": true,
  "coc.preferences.snippetStatusText": "Ⓢ ",
  "coc.preferences.extensionUpdateCheck": "daily",
  "coc.preferences.messageLevel": "error",
  "coc.source.around.firstMatch": false,
  "coc.source.buffer.firstMatch": false,
  "coc.source.syntax.firstMatch": false,
  "suggest.detailMaxLength": 60,
  "suggest.noselect": true,
  "suggest.enablePreselect": false,
  "suggest.triggerAfterInsertEnter": true,
  "suggest.autoTrigger": "always",
  "suggest.timeout": 5000,
  "suggest.enablePreview": true,
  "suggest.floatEnable": true,
  "suggest.detailField": "preview",
  "suggest.snippetIndicator": "",
  "suggest.triggerCompletionWait": 100,
  "suggest.echodocSupport": true,
  "suggest.completionItemKindLabels": {
    "class": "\uf0e8",
    "color": "\ue22b",
    "constant": "\uf8fe",
    "default": "\uf29c",
    "enum": "\uf435",
    "enumMember": "\uf02b",
    "event": "\ufacd",
    "field": "\uf93d",
    "file": "\uf723",
    "folder": "\uf115",
    "function": "\u0192",
    "interface": "\uf417",
    "keyword": "\uf1de",
    "method": "\uf6a6",
    "module": "\uf40d",
    "operator": "\uf915",
    "property": "\ue624",
    "reference": "\ufa46",
    "snippet": "\ue60b",
    "struct": "\ufb44",
    "text": "\ue612",
    "typeParameter": "\uf728",
    "unit": "\uf475",
    "value": "\uf89f",
    "variable": "\ue71b"
  },
  "diagnostic.signOffset": 1,
  "diagnostic.errorSign": "\uf467",
  "diagnostic.warningSign": "\uf071",
  "diagnostic.infoSign": "\uf129",
  "diagnostic.hintSign": "\uf864",
  "diagnostic.displayByAle": false,
  "diagnostic.refreshOnInsertMode": false,
  "diagnostic.refreshAfterSave": false,
  "diagnostic.checkCurrentLine": true,
  "diagnostic.virtualTextPrefix": " ❯❯❯ ",
  "diagnostic.virtualText": true,
  "codeLens.enable": true,
  "list.previewHighlightGroup": "Statement",
  "list.nextKeymap": "<C-e>",
  "list.previousKeymap": "<C-u>",
  "importCost.bundleSizeDecoration": "both",
  "importCost.typescriptExtensions": ["\\.tsx?$"],
  "importCost.javascriptExtensions": ["\\.jsx?$"],
  "importCost.showCalculatingDecoration": true,
  "importCost.debug": false,
  "snippets.ultisnips.directories": [
    "$HOME/.config/nvim/Ultisnips/",
    "$HOME/.config/nvim/plugged/vim-snippets/UltiSnips/"
  ],
  "coc.preferences.formatOnSaveFiletypes": [
    "javascript",
    "typescript",
    "html",
    "css",
    "json",
    "java",
    "python",
    "vue",
    "svelte",
    "c",
    "prisma"
  ],
  "yaml.format.enable": true,
  "signature.target": "float",
  "yank.enableCompletion": false,
  "typescript.suggestionActions.enabled": true,
  "typescript.format.enabled": true,
  "jest.watch": false,
  "explorer.width": 38,
  "explorer.quitOnOpen": true,
  "explorer.sources": [
    {
      "name": "buffer",
      "expand": false
    },
    {
      "name": "file",
      "expand": true
    }
  ],
  "explorer.file.column.indent.indentLine": true,
  "explorer.file.showHiddenFiles": true,
  "explorer.icon.enableNerdfont": true,
  "explorer.file.column.git.showIgnored": true,
  "explorer.keyMappingMode": "none",
  "explorer.buffer.showHiddenBuffers": false,
  "explorer.keyMappings.global": {
    "u": "nodePrev",
    "e": "nodeNext",
    "h": "toggleSelection",
    "<tab>": "actionMenu",
    "gl": "expandRecursive",
    "gh": "collapseRecursive",
    "i": ["wait", "expandable?", "expand", "open"],
    "<cr>": ["wait", "expandable?", "cd", "open"],
    "I": "open:vsplit",
    "o": ["wait", "expanded?", "collapse", "expand"],
    "O": "open:tab",
    "n": "collapse",
    "l": "gotoParent",
    "yp": "copyFilepath",
    "yn": "copyFilename",
    "yy": "copyFile",
    "dd": "cutFile",
    "pp": "pasteFile",
    "dD": "deleteForever",
    "a": "addFile",
    "k": "addFile",
    "M": "addDirectory",
    "cw": "rename",
    ".": "toggleHidden",
    "zh": "toggleHidden",
    "R": "refresh",
    "?": "help",
    "q": "quit",
    "X": "systemExecute",
    "gd": "listDrive",
    "f": "search",
    "F": "searchRecursive",
    "B": "gotoSource:file",
    "b": "gotoSource:buffer",
    "[[": "sourcePrev",
    "]]": "sourceNext",
    "[d": "diagnosticPrev",
    "]d": "diagnosticNext",
    "[c": "gitPrev",
    "]c": "gitNext",
    "<<": "gitStage",
    ">>": "gitUnstage"
  },
  "flutter.outlineWidth": 40,
  "flutter.outlineIconPadding": 0,
  "flutter.UIPath": true,
  "flutter.openDevLogSplitCommand": "botright 12split",
  "flutter.lsp.initialization.onlyAnalyzeProjectsWithOpenFiles": false,
  "flutter.trace.server": "off",
  "tslint.autoFixOnSave": false,
  "python.autoComplete.addBrackets": true,
  "python.jediEnabled": false,
  "python.formatting.provider": "yapf",
  "python.formatting.yapfArgs": [
    "--style",
    "{SPACES_AROUND_POWER_OPERATOR: True, SPACES_BEFORE_COMMENT: 1}"
  ],
  "html.format.enable": true,
  "javascript.referencesCodeLens.enable": true,
  "javascript.showUnused": true,
  "javascript.suggest.names": true,
  "javascript.suggestionActions.enabled": true,
  "json.format.enable": true,
  "eslint.autoFixOnSave": false,
  "prettier.printWidth": 100,
  "prettier.eslintIntegration": true,
  "prettier.disableLanguages": [],
  "prettier.formatterPriority": 1,
  "prettier.useTabs": true,
  "prettier.trailingComma": "all",
  "prettier.singleQuote": false,
  "todolist.autoUpload": true,
  "todolist.promptForReminder": false,
  "coc-actions.hideCursor": false,
  "coc-actions.showActionKind": true,
  "diagnostic-languageserver.filetypes": {
    "vim": "vint",
    "email": "languagetool",
    "markdown": ["write-good", "markdownlint"],
    "sh": "shellcheck",
    "elixir": ["mix_credo", "mix_credo_compile"],
    "eelixir": ["mix_credo", "mix_credo_compile"],
    "php": ["phpstan", "psalm"]
  },
  "diagnostic-languageserver.formatFiletypes": {
    "elixir": "mix_format",
    "eelixir": "mix_format"
  },
  "languageserver": {
    "lua": {
      "command": "lua-lsp",
      "filetypes": ["lua"]
    },
    "swift": {
      "command": "/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/sourcekit-lsp",
      "args": [],
      "filetypes": ["swift"],
      "initializationOptions": {},
      "settings": {}
    },
    "golang": {
      "command": "gopls",
      "rootPatterns": ["go.mod"],
      "filetypes": ["go"],
      "initializationOptions": {
        "gocodeCompletionEnabled": true,
        "diagnosticsEnabled": true,
        "lintTool": "golint"
      }
    },
    "bash": {
      "command": "bash-language-server",
      "args": ["start"],
      "filetypes": ["sh"],
      "ignoredRootPaths": []
    },
    "ccls": {
      "command": "ccls",
      "filetypes": ["c", "cpp", "cuda", "objc", "objcpp"],
      "rootPatterns": [".ccls", ".ccls-root", "compile_commands.json", ".git/", ".hg/"],
      "initializationOptions": {
        "cache": {
          "directory": "/tmp/ccls"
        }
      }
    }
  }
}
```

