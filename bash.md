# BASH

Bash web server while true; do { echo -e 'HTTP/1.1 200 OK\r\n'; cat index.html; } | nc -l 8080; done

Bash while loop                        while true; do hm init -fb Optimized 2>&1 | grep Initialization; done

Bash stderr redirect must come after file redirect

    python suiteSmokeIt.py > log.txt 2>&1

dd may be used to count bytes

    grep "testgmock" build.ninja | dd > /dev/null

Or as sink to use std in as file argument

    echo "Hello" | cat <(dd)

Bash heredoc

    cat <<- EOF >> .bashrc # HereDoc
        export EDITOR=/usr/bin/vim
    EOF

See also help topics in the "Bash Reference Manual" in
"8 Command Line Editing".

## Configuration

Write to `~/.inputrc`.

```bash
# https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax.html
#set completion-ignore-case on
#set completion-map-case on

set show-all-if-ambiguous on
set show-all-if-unmodified on
set skip-completed-text on

# https://www.gnu.org/software/bash/manual/html_node/Commands-For-Completion.html
#TAB: menu-complete
#"\e[Z": menu-complete-backward

TAB: complete
"\e[Z": insert-completions
"\e[A": history-search-backward
"\e[B": history-search-forward

# "\e[Z" == Shift-Tab
# "\e[A" == Arrow-Up
# "\e[B" == Arrow-Down
```
