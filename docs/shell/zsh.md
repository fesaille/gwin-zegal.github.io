# Zsh

The Z-shell <span><badge-doc href="http://www.zsh.org/"></badge-doc> <a href="https://github.com/topics/zsh" target="_blank"> <img src="https://img.shields.io/badge/git-topics-blue?style=flat&logo=Github" alt="Github topic"/> </a></span>

## Initialisation

Shell initilization performs operations depending on the execution context, these operations can be mainly separated on *login* and *interactive* property. An short summary can be found at [pyenv wiki](https://github.com/pyenv/pyenv/wiki/Unix-shell-initialization).

Basically:

- *login*: e.g. when user logs in to a system with non-graphical interface or via SSH;
- *interactive*: shell that has a prompt and whose standard input and error are both connected to terminals.

Zsh performs initialiation in the following order:

- `/etc/zshenv`
- `~/.zshenv`
- login mode:
	- `/etc/zprofile`
	- `~/.zprofile`
- interactive:
	- `/etc/zshrc`
	- `~/.zshrc`
- login mode:
	- `/etc/zlogin`
	- `~/.zlogin`

`.zlogout` is called when exiting, not when opening.

## Functions

### Hook functions <badge-doc href="http://zsh.sourceforge.net/Doc/Release/Functions.html#Hook-Functions"></badge-doc>

It is possible to define an array that has the same name as the function with `_functions` appended. Any element in such an array is taken as the name of a function to execute; it is executed in the same context and with the same arguments as the basic function.

!!! example 

    ```bash
    ❯ echo $precmd_functions
    _zsh_autosuggest_start _zsh_highlight_main__precmd_hook _zshz_precmd prompt_pure_precmd

    # Show the definition of a function:
    # it is possible to use `which` or nearly identical to bash `type -f` 
    ❯ whence -f _zsh_autosuggest_start
    ```


- **chpwd**: executed whenever the current working directory is changed. 
     
- **periodic**: if the parameter PERIOD is set, this function is executed every $PERIOD seconds, just before a prompt.

- **precmd**: executed before each prompt.

- **preexec**: executed just after a command has been read and is about to be executed.

- **zshaddhistory**: executed when a history line has been read interactively, but before it is executed. 

- **zshexit**: executed at the point where the main shell is about to exit normally. 


??? Info "Display user configuration of hooks functions"

    <script src="https://gist.github.com/fesaille/e85f7d44fc3d9bbd453157da2e24fa55.js"></script>


## Prompt

Prompt sequences undergo a [special form of expansion](http://zsh.sourceforge.net/Doc/Release/Prompt-Expansion.html). Some modules make it easier to personalize the prompt.

The prompt system must be loaded (performed by extensions): `autoload -U promptinit; promptinit`.

A theme can be applied with the `prompt` cmd.

```bash
❯ prompt <TAB>
 -- prompt theme --
 adam1    bigfade  elite    fire     pure     restore  zefram
 adam2    clint    elite2   off      pws      suse
 bart     default  fade     oliver   redhat   walters
```

Third party modules:

- <b>spaceshift</b> <badge-stars repo='denysdovhan/spaceship-prompt'></badge-stars> is a pure zsh prompt providing VCS integration, language version, job indicator and more. 
- <b>starshift</b> <badge-stars repo='starship/starship'></badge-stars> is a port of spaceshift in rust.
- <b>pure</b> <badge-stars repo='sindresorhus/pure'></badge-stars> is a lighweight prompt in pure zsh.


## Expansion

This section is a cheatsheet on expansion, based on the manual and reads, especially this [blog post](https://reasoniamhere.com/2014/01/11/outrageously-useful-tips-to-master-your-z-shell/).

The examples hereunder are taken from the latest and to be run, interactive comments must be enabled in zsh (`setopt interactive_comments`).

<script src="https://gist.github.com/fesaille/a3ec9617ef2e6e22d86382c08d46dcb3.js"></script>


The following types of expansions are performed in the indicated order in five steps:

- **History Expansion** is performed only in interactive shells.

- **Alias Expansion** Aliases are expanded immediately.

- **Process Substitution**, **Parameter Expansion**, **Command Substitution**, **Arithmetic Expansion**, **Brace Expansion**

    These five are performed in left-to-right fashion. On each argument, any of the
    five steps that are needed are performed one after the other. Hence, for
    example, all the parts of parameter expansion are completed before command
    substitution is started. After these expansions, all unquoted occurrences of
    the characters ‘\’,‘’’ and ‘"’ are removed.
            
- **Filename Expansion**

    If the `SH_FILE_EXPANSION` option is set, the order of expansion is
    modified for compatibility with sh and ksh: filename expansion
    is performed immediately after alias expansion.
                
- **Filename Generation**, commonly referred to as globbing, always done last.


### Filename generation (globbing)

#### [glob operators](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Glob-Operators)

- `*` matches any string, including the null string.
- `?` matches any character.
- `[...]` matches any of the enclosed characters:
    - ranges of characters can be specified by separating two characters by a `-` or classes as `[:alnum:]`, `[:alpha:]`, `[:ascii:]`, ..., `[:xdigit:]`
    - `!` or `^` negates the class
- `<[x]-[y]>` matches any number in the range x to y, inclusive.
- `(...)` matches the enclosed pattern. 
- `x|y` matches either x or y.
- `^x` matches anything except the pattern x. Requires `EXTENDED_GLOB` to be set.
- `x~y` match anything that matches the pattern x but does not match y. Requires `EXTENDED_GLOB` to be set.
- `x#` Matches zero or more occurrences of the pattern x. Requires `EXTENDED_GLOB` to be set.
- `x##` Matches one or more occurrences of the pattern x. Requires `EXTENDED_GLOB` to be set.


The precedence of the operators given above is (highest) ‘^’, ‘/’, ‘~’, ‘|’ (lowest)

```
# list text files that end in a number from 1 to 10
❯ ls -l zsh_demo/**/*<1-10>.txt

# list text files that start with the letter a
❯ ls -l zsh_demo/**/[a]*.txt

# list text files that start with either ab or bc
❯ ls -l zsh_demo/**/(ab|bc)*.txt

# list text files that don't start with a lower or uppercase c
❯ ls -l zsh_demo/**/[^cC]*.txt
```

#### [glob flag](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Glob-Flags)

- `i` case insensitive.
- `l` lower case characters in the pattern match upper or lower case characters. Upper case characters behvior unchanged.
- `I` case sensitive: locally negates the effect of i or l from that point on.
- ...


#### [glob qualifiers](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Glob-Qualifiers)

??? abstract "Furthers qualifiers"

	 | Qualifiers      | Scope                                                                                                                         |
	 | -----------     | -----------------------------------------------                                                                               |
	 | /               | directories                                                                                                                   |
	 | F               | ‘full’ (i.e. non-empty) directories.                                                                                          |
	 | .               | plain files                                                                                                                   |
	 | @               | symbolic links                                                                                                                |
	 | =               | sockets                                                                                                                       |
	 | p               | named pipes (FIFOs)                                                                                                           |
	 | *               | executable plain files (0100 or 0010 or 0001)                                                                                 |
	 | %               | device files (character or block special)                                                                                     |
	 | %b              | block special files                                                                                                           |
	 | %c              | character special files                                                                                                       |
	 | r               | owner-readable files (0400)                                                                                                   |
	 | w               | owner-writable files (0200)                                                                                                   |
	 | x               | owner-executable files (0100)                                                                                                 |
	 | A               | group-readable files (0040)                                                                                                   |
	 | I               | group-writable files (0020)                                                                                                   |
	 | E               | group-executable files (0010)                                                                                                 |
	 | R               | world-readable files (0004)                                                                                                   |
	 | W               | world-writable files (0002)                                                                                                   |
	 | X               | world-executable files (0001)                                                                                                 |
	 | s               | setuid files (04000)                                                                                                          |
	 | S               | setgid files (02000)                                                                                                          |
	 | t               | files with the sticky bit (01000)                                                                                             |
	 | fspec           | files with access rights matching spec.                                                                                       |
	 | estring +cmd    | The string will be executed as shell code.                                                                                    |
	 | ddev            | files on the device dev                                                                                                       |
	 | l[-\|+]ct       | files having a link count less than ct (-), greater than ct (+), or equal to ct                                               |
	 | U               | files owned by the effective user ID                                                                                          |
	 | G               | files owned by the effective group ID                                                                                         |
	 | uid             | files owned by user ID id if that is a number.                                                                                |
	 | gid             | like uid but with group IDs or names                                                                                          |
	 | a[Mwhms][-\|+]n | files accessed exactly n days ago.                                                                                            |
	 | m[Mwhms][-\|+]n | like the file access qualifier, except that it uses the file modification time.                                               |
	 | c[Mwhms][-\|+]n | like the file access qualifier, except that it uses the file inode change time.                                               |
	 | L[+\|-]n        | files less than n bytes (-), more than n bytes (+), or exactly n bytes in length.                                             |
	 | ^               | negates all qualifiers following it                                                                                           |
	 | -               | toggles between making the qualifiers work on symbolic links (the default) and the files they point to                        |
	 | M               | sets the MARK_DIRS option for the current pattern                                                                             |
	 | T               | appends a trailing qualifier mark to the filenames, analogous to the LIST_TYPES option, for the current pattern (overrides M) |
	 | N               | sets the NULL_GLOB option for the current pattern                                                                             |
	 | D               | sets the GLOB_DOTS option for the current pattern                                                                             |
	 | n               | sets the NUMERIC_GLOB_SORT option for the current pattern                                                                     |
	 | Yn              | enables short-circuit mode: the pattern will expand to at most n filenames.                                                   |


```bash
# show only directories
❯ print -l zsh_demo/**/*(/)

# because the expression is expanded, 
# can be used with editors, e.g. vim
# will open a lot of files (36)
❯ vim zsh_demo/**/*(.)

# show empty files
❯ ls -l zsh_demo/**/*(L0)

# show files greater than 3 KB
❯ ls -l zsh_demo/**/*(Lk+3)

# show files modified in the last hour
❯ print -l zsh_demo/**/*(mh-1)

# sort files from most to least recently modified and show the last 3
❯ ls -l zsh_demo/**/*(om[1,3])

# keep it simple
❯ ls -l zsh_demo/**/*(.Lm-2mh-1om[1,3])
```


## Modules

[Modules](http://zsh.sourceforge.net/Doc/Release/Zsh-Modules.html) are loaded with `zmodload`

### zsh/zutil

The zsh/zutil module adds some builtins:

- `zstyle` is used to define and lookup styles.
- `zformat` provides two different forms of formatting. 
- `zregexparse` implements some internals of the `_regex_arguments` function 
- `zparseopts` simplifies the parsing of options in positional parameters

## Plugins	

- <b>zsh-z</b> <badge-stars repo='agkozak/zsh-z'></badge-stars> Jump quickly to directories that you have visited "frecently."
- <b>zsh-autosuggestions</b> <badge-stars repo='zsh-users/zsh-autosuggestions'></badge-stars> Fish-like autosuggestions for zsh


## Other links

- [Adding Vi to your Zsh](https://dougblack.io/words/zsh-vi-mode.html)
- [Moving to Zsh](https://scriptingosx.com/zsh/)
