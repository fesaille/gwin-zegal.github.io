# Shell

<!-- <div class="mdc-card"> -->
<!--   <div class="mdc-card__primary-action" tabindex="0"> -->
<!--   </div> -->

<!--   qsdsqsdqsd -->
<!-- </div> -->

**nutshell** <badge-start repo='nushell/nushell'></badge-stars>

## Configuration

### `LS_COLORS`

**vivid** <badge-stars repo='sharkdp/vivid'></badge-stars> is a generator for the `LS_COLORS` environment variable

``` bash
    export LS_COLORS="$(vivid generate molokai)"
```

### GNU Stow

[GNU Stow](https://www.gnu.org/software/stow/) is a symlink farm manager which takes distinct packages of software and/or data located in separate directories on the filesystem, and makes them appear to be installed in the same place.

The software can be used to manage dotfiles.

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


**fzy** <badge-stars repo='jhawthorn/fzy'></badge-stars> is written in C


## File content search 

Search can be efficiently performed by **the silver search (`ag`)** <badge-stars repo='ggreer/the_silver_searcher'></badge-stars> <badge-doc href='https://geoff.greer.fm/ag/'></badge-doc> and **ripgrep (`rg`)** <badge-stars repo='BurntSushi/ripgrep'></badge-stars> <badge-doc logo='Markdown' href='https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md'></badge-doc>, written resp. in C and rust. `rg` tends to be one of the quickest.

### Search with substitution

In respect of [DOTADIW](https://en.wikipedia.org/wiki/Unix_philosophy#Do_One_Thing_and_Do_It_Well), `rg` does [not support](https://github.com/BurntSushi/ripgrep/issues/74) natively search and replacement. This can be achieved with a pipe.

!!! Example  "Prepare cookiecutter templates from `molecule init` outputs"

    ```bash
     rg ROLE --files-with-matches | xargs sed -e "s/ROLE/\{\{ cookiecutter.role_name \}\}/g"
    ```

Link: https://learnbyexample.github.io/substitution-with-ripgrep/

## Working with structured data

### JSON


**jq** <badge-stars repo='stedolan/jq'></badge-stars> <badge-doc href="https://stedolan.github.io/jq/"></badge-doc>

??? Question "JQ cheatsheet"
  
    <script src="https://gist.github.com/olih/f7437fb6962fb3ee9fe95bda8d2c8fa4.js"></script>


!!! Example  "Prepare cookiecutter templates from `molecule init` outputs"

    ```bash
    URL=$(you-get --json "https://www.youtube.com/watch?v=ZzfHjytDceU" | jq  -s 'sort_by(.streams.__default__.size) | reverse | .[0].streams.__default__.src[0]' | sed -e s/\"//g)
    ```

### YAML

**yq** <badge-stars repo='mikefarah/yq'></badge-stars> <badge-doc href="https://mikefarah.gitbook.io/yq/"></badge-doc>


## Makefile

Splitting Recipe Lines

https://www.gnu.org/software/make/manual/html_node/Splitting-Recipe-Lines.html

Makefile tutorial

https://makefiletutorial.com/


Introduction à Makefile 

https://gl.developpez.com/tutoriel/outil/makefile/
