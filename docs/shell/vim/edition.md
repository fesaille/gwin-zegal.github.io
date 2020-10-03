
# Editing

| Operation | ...entire line | ...to eol      | entire word | ...to eow      | ... to begin of next word |
|-----------|----------------|----------------|-------------|----------------|---------------------------|
| Change    | `cc`           | `C` ( or `c$`) | `ciw`       | `cw` (or `ce`) |                           |
| Delete    | `dd`           | `D` ( or `d$`) | `diw`       | `de`           | `dw`                      |


## Selection

`:h text-objects` or <badge-doc href="https://vimhelp.org/motion.txt.html#text-objects" message="terminal" logo="vim"></badge-doc> operate in visual mode and consists ot two characters: <kbd>i</kbd> and <kbd>a</kbd> and correspond to an inner resp. outer selection. 

## Comment
Comment line (via plugin vim-commentary): <kbd>gcc</kbd> in normal mode,
<kbd>gc</kbd> in visual mode

Surroung element while editing

## Completion

The completion menu is controlled by `completeopt` (`ofu`)

File completion is activated with <kbd>C-x</kbd><kbd>C-f</kbd>

- **ale** <badge-stars repo="dense-analysis/ale"></badge-stars>

function! InputTarget()
  let c = getchar()
  echo c
endfunction

function! Codify()
  let selection = getpos('.')
  echo string(selection) . "Yo"
  " Get selection
  " Length == 1   (normal mode)
  " -> expand selection to zone delimited by space
  " Length >= 1   (visual mode)
  " -> get selection and introduce ` around selection
endfunction

## Folding

<badge-doc href="https://vimhelp.org/usr_28.txt.html" logo="vim" message="usr_28"></badge-doc>

**Types of Folding**:

|  Type  | Description                                  |
|:------:|:---------------------------------------------|
| manual | folds are created manually and remain in RAM |
| indent | lines with equal indent form a fold          |
|  expr  | vim scripts give identation of a line        |
| marker | based on specific characters                 |
| syntax | syntax highlightung items specify folds      |
|  diff  | fold test that is not changed                |

The command zc will close a fold (if the cursor is in an open fold), and zo will open a fold (if the cursor is in a closed fold). It's easier to just use za which will toggle the current fold (close it if it was open, or open it if it was closed).

The commands zc (close), zo (open), and za (toggle) operate on one level of folding, at the cursor. The commands zC, zO and zA are similar, but operate on all folding levels (for example, the cursor line may be in an open fold, which is inside another open fold; typing zC would close all folds at the cursor).

The command zr reduces folding by opening one more level of folds throughout the whole buffer (the cursor position is not relevant). Use zR to open all folds.

The command zm gives more folding by closing one more level of folds throughout the whole buffer. Use zM to close all folds. 

Source: https://vim.fandom.com/wiki/Folding

Folding principel:

- folds at defined per level: ```:set foldlevel=<LEVEL>``` and adjacent lines are fold grouped by level value
- to fold level at start ``` :set foldlevelstart=<LEVEL>```

