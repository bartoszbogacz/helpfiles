# X.org

Write to `.Xresources`.

```Xresources
# https://wiki.archlinux.org/title/Xterm
XTerm.termName: xterm-256color
XTerm.loginShell: true

XTerm.vt100.bellIsUrgent: true
XTerm.vt100.borderWidth: 0
XTerm.vt100.highlightSelection: true
XTerm.vt100.saveLines: 4096
XTerm.vt100.jumpScroll: true
XTerm.vt100.fastScroll: true
XTerm.vt100.multiScroll: true
XTerm.vt100.metaSendsEscape: true

XTerm.vt100.translations: #override \
    Shift Ctrl <KeyPress> O: copy-selection(PRIMARY) exec-formatted("xdg-open '%t'", PRIMARY)\n \
    Shift Ctrl <KeyPress> U: select-needle("://") select-set(PRIMARY)\n \
    Shift Ctrl <KeyPress> V: insert-selection(CLIPBOARD)\n \
    Shift Ctrl <KeyPress> C: copy-selection(CLIPBOARD)\n \
    Ctrl <KeyPress> minus: smaller-vt-font()\n \
    Ctrl <KeyPress> plus: larger-vt-font()

XTerm.vt100.faceName: Inconsolata-11
XTerm.vt100.geometry: 90x40
XTerm.vt100.scrollBar: false

XTerm.vt100.foreground: white
XTerm.vt100.background: black
```
