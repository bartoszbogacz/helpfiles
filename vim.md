# VIM

    https://thevaluable.dev/vim-adept/
    https://learnbyexample.github.io/vim_reference/Visual-mode.html

    Visual Reference: https://vimhelp.org/visual.txt.html
    Visual Mode: https://vimhelp.org/usr_04.txt.html#04.4
    Visual Block Mode: https://vimhelp.org/usr_10.txt.html#10.5


    <C-t>  # Indent complete line
    <C-d>  # De-indent complete line
    vip  # In visual mode, select inner paragraph
    c3l  # Change 3 following characters
    git ls-files | vim -
    :Scratch
    /CMakeLists.txt
    gf
    :bd
    /pattern -- Alternatively, ? or word with # (backward) and * (forward)
    n or N -- Find first instance to replace (consider direction of # or *)
    cgn -- Change next (previous) occurance of "/ register
    [n -- Move to next instace, optional, if you want to preview]
    . -- Repeat last action
    # -- Search word backward
    :%s/ -- Begin search and replace
    <Ctrl-R>/ -- Paste "/ register
    /replacement/gc -- Replace g globally and ask for c confirmation

## Configuration VIM

On Linux `vim ~/.vimrc`. On Windows `vim %USERPROFILE%\_vimrc`.

```vim
" Do not modify any timeout settings, as usually suggested in example configs.
" This results in having to press ESC twice to exit insert mode under tmux.

set nocompatible

" On inserting a parenthesis matchparen jumps to its previous
" match shortly to highlight it and distracts the user.
" Prevent matchparen from loading by pretending it to be loaded.
let loaded_matchparen = 1

" Colors
colorscheme slate
syntax on

" Indent
set autoindent
set expandtab
set shiftwidth=4
set softtabstop=4

" Wrap
set wrap

" Search
set nowrapscan
set hlsearch
set incsearch
" set grepprg=git\ grep\ -n

set backspace=indent,eol,start
set belloff=all
set completeopt=menuone,longest
set encoding=utf8
set fileformats=unix,dos,mac
set lazyredraw
set list
set listchars=tab:>-,trail:~,precedes:<,extends:>,nbsp:%
set nobackup
set nomodeline
set noshowmatch
set nostartofline
set noswapfile
set nowritebackup
set number
set path=.
set ruler
set scrolloff=5
set showcmd
set showmode
set tags=tags
set wildmode=list:longest

command Scratch setlocal buftype=nofile | setlocal bufhidden=hide

set nocursorline
autocmd InsertEnter * set cursorline
autocmd InsertLeave * set nocursorline
```

## Configuration GVIM

On Linux `vim ~/.gvimrc`.

```vim
set columns=100
set guifont=Inconsolata\ 11
set guioptions=!ac
set lines=40

colorscheme slate

"nmap gx :execute 'silent! !xdg-open ' . shellescape(trim(getline(".")), 1)<CR>
vnoremap <silent> gx :<C-U>execute 'silent !xdg-open ' . shellescape(trim(getline("'<")[getpos("'<")[2]-1:getpos("'>")[2]-1]), 1)<CR>
```

On Windows `vim %USERPROFILE%\_vimrc`.

```vim
set shell=C:\Windows\SysNative\cmd.exe

set columns=100
set guifont=Consolas:h12
set guioptions=!ac
set lines=40

colorscheme desert

" https://vi.stackexchange.com/questions/25456/how-can-i-change-the-colorscheme-of-the-vim-terminal-buffer
let g:terminal_ansi_colors = [
    \'#282828', '#CC241D', '#98971A', '#D79921',
    \'#458588', '#B16286', '#689D6A', '#D65D0E',
    \'#fb4934', '#b8bb26', '#fabd2f', '#83a598',
    \'#d3869b', '#8ec07c', '#fe8019', '#FBF1C7']

highlight Terminal guibg='#282828' guifg='#ebdbb2'

" nmap gx :execute 'silent! !start ' . shellescape(expand("<cfile>"), 1)<CR>
vnoremap <silent> gx :<C-U>execute 'silent !start ' . shellescape(trim(getline("'<")[getpos("'<")[2]-1:getpos("'>")[2]-1]), 1)<CR>
```

## Assorted

Index of all commands

    :viusage

Cheat Sheet <https://michaelgoerz.net/refcards/vimqrc.pdf>

### Motion

Move left, move down, move up, move right

    h j k l

Word forward, word backward, WORD forward, WORD backward

    w b W B

To character a, forward, backward, till, backward till, repeat

    fa Fa ta Ta ;

First column, First character, last character

    0 ^ $

Next paragraph, prev paragraph, next sentence, prev sentence

    { } ( )

Next search pattern, previous search pattern

    gn gN

## Visual

Enter visual mode with `v`. Select with motions.

Select paragraph

    v{

## Movement

First line, last line, 35th line

    gg G 35G

Insert before, after, start of line, end of line

    i a I A

Search pattern forward, backward

    /pattern ?pattern

Next in search direction, previous

    n N

Last jump origin, last change, go to older change, newer change

    '' '. g; g,

### Insert Mode

Indent, un-indent

    SHIFT-t SHIFT-d

### Buffers

List buffers

    :ls

Alternate buffer

    CTRL-^

### Terminal

Open terminal, in vertical split

    :terminal
    :vertical terminal

Terminal normal mode (allows copy), terminal insert mode, move to other window

    CTRL-W N
    a
    CTRL-W CTRL-W

Paste register {reg} in terminal insert mode

    CTRL-W " {reg}

### Assorted

In commandline mode, insert word under cursor with `c_CTRL-R c_CTRL-W`.

In includes and files, show first occurence with `[i`, show all with `[I`,
jump to first with `[_CTRL-I` and to the second by `2[_CTRL-I`.

Enable ctags usage with `set tags=tags` and refresh with `ctags -R *`.
For tag under cursor, jump to definition `CTRL-]`, show usages `g]`
or go back with `CTRL-T`. Show stack of visited `:tags`.


:enew | r!git blame #

:bufdo e

i_CTRL-N
i_CTRL-X CTRL-N
i_CTRL-X CTRL-L

:g/Error
:v/Error

:r!ssh dev cat grafana/build/Build_Atom_History/dashboard.json

qa80|F iENTER> ESCq@a@@


Word under cursor in commandline mode   c_CTRL-R CTRL-W

Help for normal mode key
Help for insert mode key
Help for option
Help for setting?

                                        CTRL-X CTRL-T
                                        CTRL-Y / CTRL-E

Show topmost line containing keyword    TODO
Show all lines containing keyword       TODO
Jump to n-th line containing keyword    TODO

Show all lines containing pattern       :isearch /pattern/

Write vim register 0 to clipboard       :!tmux set-buffer <C-r>0
Write vim selection to clipboard        :<'>'w !tmux load-buffer -
Read tmux clipboard into buffer         :r !tmux show-buffer
Read clipboard from other host          :r !ssh dev tmux show-buffer

Enter normal mode for one command       i_CTRL-O

Show all lines in includes for pattern  :isearch /pattern/
Show all lines in includes for keyword  [I
Jump to 2nd line in includes keyword    2[ CTRL-I

Jump to first definition of tag         :tag /pattern/
Select tag matching pattern             :tselect /pattern/
Select tag for word under cursor        g]
Go to previous tag in the tag stack     CTRL-T

Search all buffers for pattern          :bufdo vimgrepadd /pattern/ %

Search last pattern in git repository   :cexpr system('git grep -n /')
Populate quickfix with filenames        :cexpr system('git ls-files | sed s/$/:1:_/')
Buffer contents to quickfix list        :cexpr getline(1, '$')
Clear quickfix list (set to [])         :cexpr []

Run _lines_ in shell and sub. output    :<',>'!bash
Declare current as scratch buffer       :setlocal noswapfile | setlocal buftype=nofile | setlocal bufhidden=hide

Series of articles on vim usage         https://thevaluable.dev/vim-adept/
