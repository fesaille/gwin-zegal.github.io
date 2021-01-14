# Shell

## Configuration

### Line edition and keybindings

GNU Readline <badge-wiki
href='https://en.wikipedia.org/wiki/GNU_Readline'></badge-wiki> is a software
library that provides line-editing and history capabilities for interactive
programs with a command-line interface. Bash typically uses this library (same [
original author
](https://en.wikipedia.org/wiki/Brian_Fox_(computer_programmer))). Emacs-like
keybindings are [ default
](https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File.html)
but readline enables configuration files at `/etc/inputrc` or `~/.inputrc`.

A lot of program not specifically written in C rely on `readline`, e.g. the
[impala-shell](https://docs.cloudera.com/documentation/enterprise/latest/topics/impala_impala_shell.html)
through python's [readline
module](https://docs.python.org/3/library/readline.html).


Zsh does not use readline, instead uses an own development [Zsh Line Editor
(ZLE)](http://zsh.sourceforge.net/Doc/Release/Zsh-Line-Editor.html). Keybindings
in `inputrc` are not read, rely instead on an internal command
[`bindkey`](`terminfo`) that can be coupled to `terminfo`.


### `LS_COLORS`

**vivid** <badge-stars repo='sharkdp/vivid'></badge-stars> is a generator for
the `LS_COLORS` environment variable

``` bash
export LS_COLORS="$(vivid generate molokai)"
```

### GNU Stow

[GNU Stow](https://www.gnu.org/software/stow/) is a symlink farm manager which
takes distinct packages of software and/or data located in separate directories
on the filesystem, and makes them appear to be installed in the same place.

The software can be used to manage dotfiles.

### GNU envsubst (Gettext package)

[GNU envsubst](https://www.gnu.org/software/gettext/manual/html_node/envsubst-Invocation.html)
substitutes the values of environment variables.

## Autojump

These utilities give the most visited directory for the shortest search term typed.

- **jump** <badge-stars repo='gsamokovarov/jump'></badge-stars> is written in go.
- **autojump** <badge-stars repo='wting/autojump'></badge-stars> is written in python.
- **zoxide** <badge-stars repo='ajeetdsouza/zoxide'></badge-stars> is written in rust.
- **zsh-z** <badge-stars repo='agkozak/zsh-z'></badge-stars> is a native zsh port of z.sh


## Finding files

- **nnn** <badge-stars repo='jarun/nnn'></badge-stars> <badge-doc href="https://github.com/jarun/nnn/wiki"></badge-doc> is another vi-inspired filemanager for the console, lightweight, written in C.
- **Ranger** <badge-stars repo='ranger/ranger'></badge-stars> <badge-doc href="https://ranger.github.io"></badge-doc>, vim-inspired filemanager for the console, written in python.

    Install with `pipx install ranger-fm`

- **exa** <badge-stars repo='ogham/exa'></badge-stars> <badge-doc href="https://the.exa.website/"></badge-doc> is a replacement for ls written in Rust.


## Directory content

**dust** <badge-stars repo='bootandy/dust'></badge-stars> is a rust application
printing a similar output to `du` with additional bar chart.


## fuzzy finder

**fzf** <badge-stars repo='junegunn/fzf'></badge-stars> <badge-doc href="https://github.com/junegunn/fzf#table-of-contents"></badge-doc> is a go fuzzy finder


??? Help "Search syntax"

    | Token     | Match type                 | Description                          |
    | --------- | -------------------------- | ------------------------------------ |
    | `sbtrkt`  | fuzzy-match                | Items that match `sbtrkt`            |
    | `'wild`   | exact-match (quoted)       | Items that include `wild`            |
    | `^music`  | prefix-exact-match         | Items that start with `music`        |
    | `.mp3$`   | suffix-exact-match         | Items that end with `.mp3`           |
    | `!fire`   | inverse-exact-match        | Items that do not include `fire`     |
    | `!^music` | inverse-prefix-exact-match | Items that do not start with `music` |
    | `!.mp3$`  | inverse-suffix-exact-match | Items that do not end with `.mp3`    |

`fzf` [provides
bindings](https://github.com/junegunn/fzf#key-bindings-for-command-line):

- <kbd>Ctrl</kbd><kbd>T</kbd> paste the selected files and directories onto the command-line
- <kbd>Ctrl</kbd><kbd>R</kbd> paste the selected command from history onto the command-line. A second press on <kbd>Ctrl</kbd><kbd>R</kbd> sorts relevant entries in chronological order
- <kbd>Alt</kbd><kbd>C</kbd> cd into the selected directory
- fuzzy competion is activated with `**`, e.g. `vim **<TAB>` completes all files
  in the cwd.


**fzy** <badge-stars repo='jhawthorn/fzy'></badge-stars> is written in C


## File content search

Search can be efficiently performed by **the silver search (`ag`)** <badge-stars repo='ggreer/the_silver_searcher'></badge-stars> <badge-doc href='https://geoff.greer.fm/ag/'></badge-doc> and **ripgrep (`rg`)** <badge-stars repo='BurntSushi/ripgrep'></badge-stars> <badge-doc logo='Markdown' href='https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md'></badge-doc>, written resp. in C and rust. `rg` tends to be one of the quickest.

**Ripgrep**

 <badge-doc href='https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md' logo='github'></badge-doc>

!!! info "Usage"

	```bash
	rg [OPTIONS] PATTERN [PATH ...]
	rg [OPTIONS] [-e PATTERN ...] [-f PATTERNFILE ...] [PATH ...]
	rg [OPTIONS] --files [PATH ...]
	rg [OPTIONS] --type-list
	command | rg [OPTIONS] PATTERN
	```

- `--type <TYPE>` where `<TYPE>` is part of the registered types, can be displayed with `rg --list-types`

### Search with substitution

In respect of [DOTADIW](https://en.wikipedia.org/wiki/Unix_philosophy#Do_One_Thing_and_Do_It_Well), `rg` does [not support](https://github.com/BurntSushi/ripgrep/issues/74) natively search and replacement. This can be achieved with a pipe.

!!! Example  "Prepare cookiecutter templates from `molecule init` outputs"

    ```bash
     rg ROLE --files-with-matches | xargs sed -e "s/ROLE/\{\{ cookiecutter.role_name \}\}/g"
    ```

Link: https://learnbyexample.github.io/substitution-with-ripgrep/

### Manual filtering: globs

!!! Example  "Exclude path 'pack' from search"

    ```bash
    rg -g '!/pack/**' g:ale
    ```

## Working with structured data

### JSON


**jq** <badge-stars repo='stedolan/jq'></badge-stars> <badge-doc
href="https://stedolan.github.io/jq/"></badge-doc>

??? Question "JQ cheatsheet"

    <script
    src="https://gist.github.com/olih/f7437fb6962fb3ee9fe95bda8d2c8fa4.js"></script>


!!! Example  "Prepare cookiecutter templates from `molecule init` outputs"

    ```bash URL=$(you-get --json "https://www.youtube.com/watch?v=ZzfHjytDceU" |
    jq  -s 'sort_by(.streams.__default__.size) | reverse |
    .[0].streams.__default__.src[0]' | sed -e s/\"//g)
    ```

### YAML

**yq** <badge-stars repo='mikefarah/yq'></badge-stars> <badge-doc
href="https://mikefarah.gitbook.io/yq/"></badge-doc>


## Makefile

 <badge-doc href='https://www.gnu.org/software/make/manual'></badge-doc>


### Wildcard characters

`*`, `?` and `[...]`

### Automatic variables

`$^` list all the prerequisites of the rule
`$<` list the first prerequisite
`$?` list all the prerequisites newer than the target

`$@` is the target

Splitting Recipe Lines

https://www.gnu.org/software/make/manual/html_node/Splitting-Recipe-Lines.html

Makefile tutorial

https://makefiletutorial.com/


Introduction à Makefile

https://gl.developpez.com/tutoriel/outil/makefile/


## Workflows

**desk** <badge-stars repo='jamesob/desk'></badge-stars> makes it easy
to flip back and forth between different project contexts in your favorite
shell. Change directory, activate a virtualenv or rvm, load in domain-specific
aliases, environment variables, functions, arbitrary shell files, all in a
single command.

**direnv** <badge-stars repo='direnv/direnv'></badge-stars> augments existing shells with a new feature that can load and unload environment variables depending on the current directory.

**Modules** <badge-stars repo='cea-hpc/modules'></badge-stars>  is a tool that simplify shell initialization and lets users easily modify their environment during the session with modulefiles.

**zsh-autoenv** <badge-stars repo='Tarrasch/zsh-autoenv'></badge-stars>
automatically sources (known/whitelisted) `.autoenv.zsh ` files, handles "enter"
and leave" events, nesting, and stashing of variables (overwriting and
restoring).

**asdf** <badge-stars repo='asdf-vm/asdf'></badge-stars> manage multiple runtime
versions with a single CLI tool, extendable via plugins.

<!-- shadowenv - uses an s-expression format to define -->
<!-- environment changes that should be executed -->

## Others

**nutshell** <badge-stars repo='nushell/nushell'></badge-stars> is a new kind of
shell, currently under heavy development.
