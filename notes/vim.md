# Vim

## Modes

| Key | Mode |
|---|---|
| `Esc` | Normal mode (move, run commands) |
| `i` / `a` | Insert before / after cursor |
| `I` / `A` | Insert at start / end of line |
| `o` / `O` | New line below / above and insert |
| `v` / `V` / `Ctrl+v` | Visual: characters / lines / block |
| `:` | Command line |

## Save & quit

| Command | Action |
|---|---|
| `:w` | Save |
| `:q` | Quit |
| `:wq` or `ZZ` | Save and quit |
| `:q!` | Quit without saving |
| `:w newname` | Save as |
| `:e file` | Open a file |

## Moving around

| Key | Move |
|---|---|
| `h j k l` | Left, down, up, right |
| `w` / `b` | Next / previous word |
| `e` | End of word |
| `0` / `^` / `$` | Start of line / first character / end of line |
| `gg` / `G` | Top / bottom of file |
| `42G` or `:42` | Go to line 42 |
| `Ctrl+d` / `Ctrl+u` | Half page down / up |
| `%` | Jump to matching bracket |
| `f x` | Jump to next `x` on the line (`;` repeats) |

## Editing

| Key | Action |
|---|---|
| `x` | Delete character |
| `dd` | Delete (cut) line |
| `dw` | Delete word |
| `D` | Delete to end of line |
| `yy` | Copy (yank) line |
| `yw` | Copy word |
| `p` / `P` | Paste after / before |
| `u` | Undo |
| `Ctrl+r` | Redo |
| `.` | Repeat last change |
| `r x` | Replace character with `x` |
| `cw` | Change word |
| `cc` | Change whole line |
| `ciw` | Change inner word (cursor anywhere in word) |
| `ci"` | Change text inside quotes |
| `>>` / `<<` | Indent / unindent line |
| `J` | Join line below onto this one |

Add a number to repeat: `3dd` deletes 3 lines, `5j` moves down 5.

In visual mode, select text then `d` (cut), `y` (copy), `>` (indent), or `c` (change).

## Search & replace

| Command | Action |
|---|---|
| `/text` | Search forward |
| `?text` | Search backward |
| `n` / `N` | Next / previous match |
| `*` | Search for word under cursor |
| `:s/old/new/g` | Replace on current line |
| `:%s/old/new/g` | Replace in whole file |
| `:%s/old/new/gc` | Replace in whole file, confirm each |
| `:noh` | Clear search highlight |

## Windows & tabs

| Command | Action |
|---|---|
| `:sp file` / `:vsp file` | Split horizontal / vertical |
| `Ctrl+w w` | Switch split |
| `Ctrl+w h/j/k/l` | Move to split in a direction |
| `:tabnew file` | Open in new tab |
| `gt` / `gT` | Next / previous tab |

## Handy settings

Type these after `:` or put them (without `:`) in `~/.vimrc`:

```vim
set number          " line numbers
set relativenumber  " relative line numbers
syntax on           " syntax highlighting
set paste           " paste from clipboard without auto-indent mess
```
