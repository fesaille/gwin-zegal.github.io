# Vim

`:h terminal` or <badge-doc href="https://vimhelp.org/terminal.html" message="terminal" logo="vim"></badge-doc>


https://vim.rtorr.com/

## Configuration

Vim has a number of internal variables and switches:

- [options](https://vimhelp.org/options.txt.html)   description of all options
- [map](https://vimhelp.org/map.txt.html)       key mapping and abbreviations
- [autocmd](https://vimhelp.org/autocmd.txt.html)p  automatically executing commands on an event
<!-- - [eval](https://vimhelp.org/eval.txt.html)      expression evaluation, conditional commands -->
- [fold](https://vimhelp.org/fold.txt.html)      hide (fold) ranges of lines

When starting, vim will look in the [ runtimepath ](https://vimhelp.org/options.txt.html#%27runtimepath%27) and underlying directories for runtime files. Basicaly on unix like systems:

- $HOME/.vim,
- $VIM/vimfiles,
- $VIMRUNTIME,
- $VIM/vimfiles/after,
- $HOME/.vim/after

This is a list of some directories which will be searched for runtime files:

| File           | Description                                     |
|----------------|-------------------------------------------------|
| `filetype.vim` | filetypes by file name new-filetype             |
| `scripts.vim`  | filetypes by file contents new-filetype-scripts |
| `autoload/`    | automatically loaded scripts autoload-functions |
| `colors/`      | color scheme files                              |
| `compiler/`    | compiler files                                  |
| `ftplugin/`    | filetype plugins write-filetype-plugin          |
| `import/`      | files that are found by :import                 |
| `indent/`      | indent scripts indent-expression                |
| `pack/`        | packages :packadd                               |
| `plugin/`      | plugin scripts write-plugin                     |
| `syntax/`      | syntax files mysyntaxfile                       |


`~/.vim/syntax` contains

## Links

[Learn vim script the hard way](https://learnvimscriptthehardway.stevelosh.com/chapters/42.html)
