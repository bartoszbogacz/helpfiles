# Kakoune

    sudo zypper install gcc12-c++
    git clone https://github.com/mawww/kakoune.git
    cd kakoune
    make CXX=g++-12
    sudo make install

    https://github.com/mawww/kakoune#3-basic-interaction
    https://github.com/mawww/kakoune/blob/master/doc/pages/keys.asciidoc

    https://github.com/mawww/kakoune/wiki/Migrating-from-Vim
    https://kakoune-editor.github.io/community-articles/2021/01/01/first_two_hours_in_two_minutes.html
    https://github.com/mawww/kakoune/blob/master/contrib/TRAMPOLINE
    https://phaazon.net/blog/more-hindsight-vim-helix-kakoune

Write to `.config/kak/kakrc`.

```kakrc
colorscheme gruvbox-light

# https://kakoune-editor.github.io/community-articles/2021/01/01/first_two_hours_in_two_minutes.html
set-option global tabstop 4
set-option global indentwidth 4

# https://github.com/mawww/kakoune/issues/4372#issuecomment-925461815
set-option global ui_options terminal_enable_mouse=false

add-highlighter global/ number-lines
add-highlighter global/ show-matching
add-highlighter global/ wrap -indent

# https://github.com/mawww/kakoune/issues/2254
add-highlighter global/trailing-whitespace regex '\h+$' 0:Error

# https://github.com/mawww/kakoune/wiki/Indentation-and-Tabulation#indentation-and-tab-handling--through-a-mapping
map global insert <tab> '<a-;><a-gt>'
map global insert <s-tab> '<a-;><a-lt>'
```
