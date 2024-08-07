Yank vimscript and source it: `y:@"`

Configuration
=============

On Linux "~/.vimrc" and "~/.gvimrc".
On Windows "%USERPROFILE%\_vimrc" and "%USERPROFILE%\_gvimrc".

### VIM Configuration {{{

```vimscript
" Do not modify any timeout settings, as usually suggested in example configs.
" This results in having to press ESC twice to exit insert mode under tmux.

set nocompatible

" On inserting a parenthesis matchparen jumps to its previous
" match shortly to highlight it and distracts the user.
" Prevent matchparen from loading by pretending it to be loaded.
let loaded_matchparen = 1

" Colors
set termguicolors
colorscheme catppuccin_mocha
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

let mapleader = " "
nnoremap <leader>ty :call system("tmux load-buffer -", @")<cr>
nnoremap <leader>tp :let @" = system("tmux show-buffer")<cr>p
nnoremap <leader>tP :let @" = system("tmux show-buffer")<cr>P
" nnoremap <leader>t2 :call system("tmux send-keys -t 2 -l " . shellescape(@t))<cr>

vnoremap <leader>ty y<cr>:call system("tmux load-buffer -", @")<cr>
vnoremap <leader>tp :<C-u>let @" = system("tmux show-buffer")<cr>gvp
vnoremap <leader>tP :<C-u>let @" = system("tmux show-buffer")<cr>gvP
" vnoremap <leader>t2 "ty<cr>:call system("tmux send-keys -t 2 -l " . shellescape(@t))<cr>

" set nocursorline
" autocmd InsertEnter * set cursorline
" autocmd InsertLeave * set nocursorline

function! FuzzyGitGrep()
    let tmp = tempname()
    execute '!git grep -nr "" | fzf >'.tmp
    let fname = split(readfile(tmp)[0], ":")
    execute 'edit +'.fname[1] fname[0]
endfunction

function! FuzzyGitFind()
    let tmp = tempname()
    execute '!git ls-files | fzf >'.tmp
    execute 'edit '.readfile(tmp)[0]
endfunction

command GG silent call FuzzyGitGrep() | redraw!
command GF silent call FuzzyGitFind() | redraw!

set grepprg=git\ grep\ -n
set makeprg=mypy\ src

set path=,.,src,test
```

}}}

### GVIM Windows {{{

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

}}}

### FZF -- Fuzzy Finder {{{

function! FuzzyGitGrep()
    let tmp = tempname()
    execute '!git grep -nr "" | fzf >'.tmp
    let fname = split(readfile(tmp)[0], ":")
    execute 'edit +'.fname[1] fname[0]
endfunction

function! FuzzyGitFind()
    let tmp = tempname()
    execute '!git ls-files | fzf >'.tmp
    execute 'edit '.readfile(tmp)[0]
endfunction

command GG silent call FuzzyGitGrep() | redraw!
command GF silent call FuzzyGitFind() | redraw!

function! SelectFile()
  let tmp = tempname()
  execute '!ls | fzf >'.tmp
  let fname = readfile(tmp)[0]
  silent execute '!rm '.tmp
  execute 'vsplit '.fname
endfunction

}}}

### Colors {{{

    Download catppuccin to ~/.vim/colors on Linux

curl "https://raw.githubusercontent.com/catppuccin/vim/main/colors/catppuccin_frappe.vim" > ~/.vim/colors/catppuccin_frappe.vim
curl "https://raw.githubusercontent.com/catppuccin/vim/main/colors/catppuccin_latte.vim" > ~/.vim/colors/catppuccin_latte.vim
curl "https://raw.githubusercontent.com/catppuccin/vim/main/colors/catppuccin_macchiato.vim" > ~/.vim/colors/catppuccin_macchiato.vim
curl "https://raw.githubusercontent.com/catppuccin/vim/main/colors/catppuccin_mocha.vim" > ~/.vim/colors/catppuccin_mocha.vim

    Download catppuccin to %USERPROFILE%\.vim\colors on Windows (using cmd)

mkdir -p %USERPROFILE%\.vim\colors

curl "https://raw.githubusercontent.com/catppuccin/vim/main/colors/catppuccin_frappe.vim" > %USERPROFILE%\vimfiles\colors\catppuccin_frappe.vim
curl "https://raw.githubusercontent.com/catppuccin/vim/main/colors/catppuccin_latte.vim" > %USERPROFILE%\vimfiles\colors\catppuccin_latte.vim
curl "https://raw.githubusercontent.com/catppuccin/vim/main/colors/catppuccin_macchiato.vim" > %USERPROFILE%\vimfiles\colors\catppuccin_macchiato.vim
curl "https://raw.githubusercontent.com/catppuccin/vim/main/colors/catppuccin_mocha.vim" > %USERPROFILE%\vimfiles\colors\catppuccin_mocha.vim

    Configure VIM to use colors in TMUX

set termguicolors
source catppuccin_mocha
syntax on

}}}

### Snippets {{{

}}}

### Movement {{{

}}}

## Tips and tricks

Execute vimscript lines in buffer. More an example of how to use vimscript.

    nnoremap <F2> :execute getline(".")<CR>
    vnoremap <F2> :<C-u>for line in getline("'<", "'>") \| execute line \| endfor<CR>

https://vi.stackexchange.com/questions/17606/vmap-and-visual-block-how-do-i-write-a-function-to-operate-once-for-the-entire

Replace non-breaking spaces with spaces

    :%s/<CTRL-V>u00a0/ /g

    :noremap aq :execute "normal ?\\n\\n\<lt>CR>++V/\\n\\n\<lt>CR>"<CR>

    vim +"copen" -q <(rg -n needle)

    :'<,'>!tmux load-buffer <(cat -)

    :'<,'>!tmux load-buffer $(cat -)

    print(1 + 1)
    :'<,'>!python
    u

https://unix.stackexchange.com/questions/604178/how-can-i-launch-fzf-inside-vim-and-open-the-selected-file-on-a-split-window

https://vim.fandom.com/wiki/Indent_text_object

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

Macro (`qa`) to add `> ` to each line and break (`iENTER`) the line
at whitespace (`F `) before column 80 (`80|`).

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

