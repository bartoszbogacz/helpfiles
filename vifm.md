# VIFM

Help Topics: Command macros, Menu and dialogs

Rename file                             cw
Move one directory up                   gh
Show file in pane in less-like          e

Set directory of other pane to current  :sync

Diff file and other and show in Menu    :!diff -u %c %C %M
Add file under cursor (any pany)        :!git add %c
Find pattern in git repository          :!git grep -n BuildTask %M
Re-open menu with results               :copen

Copy file path to tmux clipboard        :!tmux set-buffer %d/%c
Open file in vim in (right) pane 2      :!tmux send-keys -t2 :e%d/%c Enter

:help
:copen
/sorting keys
/Command macros
/Menus and dialogs
:set viewcolumns=-{name},{perms},{mtime},{size}

## Configuration

Write to `.vifmrc`.

```vim
only

set findprg="sh -c 'git ls-files | grep %A'"
set grepprg="git grep -n %A"
set ignorecase
set incsearch
set nohlsearch
set syscalls
set trash

colorscheme darkdesert

nnoremap yp :!tmux set-buffer %d/%c
```
