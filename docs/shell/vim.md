# Vim

`:h terminal` or <badge-doc href="https://vimhelp.org/terminal.html" message="terminal" logo="vim"></badge-doc>


## Panes

Close a terminal pane with <kbd>C-w</kbd><kbd>C-c</kbd>

To change two vertically split windows to horizonally split
<kbd>C-w</kbd><kbd>t</kbd><kbd>C-w</kbd><kbd>K</kbd>

Horizontally to vertically:
<kbd>C-w</kbd><kbd>t</kbd><kbd>C-w</kbd><kbd>H</kbd>

<kbd>C-w</kbd><kbd>t</kbd> makes the first (topleft) window current
<kbd>C-w</kbd><kbd>H</kbd> moves the current window to full-height at far left
<kbd>C-w</kbd><kbd>K</kbd> moves the current window to full-width at the very top


Comment line (via plugin vim-commentary): <kbd>gcc</kbd> in normal mode,
<kbd>gc</kbd> in visual mode

Surroung element while editing

## Code edition

### Folding


For Python, https://github.com/Vimjas/vim-python-pep8-indent


## Plugins

[comment]: <> (- <b>Ale</b> <badge-stars repo='dense-analysis/ale'></badge-stars> <badge-doc href="https://vimawesome.com/plugin/ale"></badge-doc> is a providing asynchronous linting)


### File editing

- <b>vim-commentary</b> <badge-stars repo='tpope/vim-commentary'></badge-stars> <badge-doc href="https://github.com/tpope/vim-commentary"></badge-doc> comment stuff out
- <b>vim-surround</b> <badge-stars repo='tpope/vim-surround'></badge-stars> provides mapping for parentheses, brackets, quotes, XML tags, and more.
- <b>vim-multiple-cursors</b> <badge-stars repo='terryma/vim-multiple-cursors'></badge-stars> <badge-doc href="https://github.com/terryma/vim-multiple-cursors#quick-start" message="latest" logo="github"></badge-doc> is a Sublime Text style multiple selections for Vim

### Browse files, buffers, search

- <b>Ranger.vim</b> <badge-stars repo='francoiscabrol/ranger.vim'></badge-stars> <badge-doc href="https://github.com/francoiscabrol/ranger.vim#how-to-use-it"></badge-doc>, Ranger integration in vim
- <b>ctrlp.vim</b> <badge-stars repo='ctrlpvim/ctrlp.vim'></badge-stars>
- <b>ack.vim</b> <badge-stars repo='mileszs/ack.vim'></badge-stars>

### Languages

- <b>Coc.vim</b> <badge-stars repo='neoclide/coc.nvim'></badge-stars> <badge-doc href="https://github.com/neoclide/coc.nvim/blob/master/doc/coc.txt" message="latest" logo="github"></badge-doc> has full support for [Language Server Protocol](https://microsoft.github.io/language-server-protocol/) completion




[LSP](https://langserver.org/)


- <b>vim-markdown</b> <badge-stars repo='plasticboy/vim-markdown'></badge-stars> <badge-doc href="https://github.com/plasticboy/vim-markdown#vim-markdown"></badge-doc>, Markdown Vim Mode. 

#### Javascript

[A guide to setting up Vim for JavaScript development](https://freshman.tech/vim-javascript/)
[JavaScript Documentation Standards](https://make.wordpress.org/core/handbook/best-practices/inline-documentation-standards/javascript/)
- <b>vim-javascript</b> <badge-stars repo='pangloss/vim-javascript'></badge-stars> <badge-doc href='https://github.com/pangloss/vim-javascript#vim-javascript' message=''></badge-doc>, comment stuff out
- <b>vim-polyglot</b> <badge-stars repo='sheerun/vim-polyglot'></badge-stars> <badge-doc href='https://github.com/sheerun/vim-polyglot/blob/master/README.md'></badge-doc>, collection of language packs for Vim.


### Python

- https://docs.python-guide.org/dev/env/
- https://www.vimfromscratch.com/articles/vim-for-python/
- 
- https://github.com/neoclide/coc-python


### html

```
:set omnifunc=htmlcomplete#CompleteTags
```

### DB

<badge-stars repo='tpope/vim-dadbod'></badge-repo>Modern database interface for Vim 
