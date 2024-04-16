# sed

Simple inline replace replace

    sed -i 's/patternA/patternB/g' file.txt

Extract digits from lines containing sample12

    sed -n -r 's/.*sample([[:digit:]]+)([[:digit:]]+).*/\1\2/p' file.txt

`-n` suppress output of non-matching lines
`-r` extended regular expressions to avoid escaping of grouping parenthesis
