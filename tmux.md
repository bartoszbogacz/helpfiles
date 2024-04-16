# TMUX

## TMUX

Attach or create a new session          tmux new -As dev

Move pane into its own window
Split and move some pane into space

Move window left                        tmux swap-window -t -1
Open history of last pane in vim        tmux capture-pane -t ":.{last}" -pS - | vim -

## Configuration

On Linux `vim ~/.tmux.conf`.

```bash
# Any of the commands may also be set interactively
# in the shell with `tmux ...` or within tmux with `<Ctrl-b>:`

# https://github.com/tmux/tmux/wiki/FAQ#how-do-i-use-a-256-colour-terminal
set-option -g default-terminal "screen-256color"

# Avoid delay when pressing Escape key in VIM
# See also: :help timeout in VIM
# See also: https://superuser.com/questions/942677/consequences-of-escape-time-0-tmux-setting
set-option -g escape-time 100

# set-option -g renumber-windows on # Fill empty slots left by closed windows

set-option -g wrap-search off
set-option -g base-index 1 # Start counting windows at 1
set-option -g history-limit 10000 # Save more lines of scrollback
set-window-option -g mode-keys vi # Use VIM inspired navigation in copy-mode
set-window-option -g pane-base-index 1 # Start counting panes at 1

# Navigate panes and windows without a prefix
# Pane indices can be given as :.N
# Window indices can be given as :=N
#bind-key -n M-1 select-pane -t :.1
#bind-key -n M-2 select-pane -t :.2
#bind-key -n M-3 select-pane -t :.3
#bind-key -n M-4 select-pane -t :.4
#bind-key -n M-5 select-pane -t :.5
#bind-key -n M-6 select-pane -t :.6
#bind-key -n M-7 select-pane -t :.7
#bind-key -n M-8 select-pane -t :.8
#bind-key -n M-9 select-pane -t :.9

# Create new panes from current directory
bind-key -T prefix % split-window -h -c "#{pane_current_path}"
bind-key -T prefix '"' split-window -v -c "#{pane_current_path}"

# Be more like vim terminals in copy-mode-vi and search incrementally
bind-key -T copy-mode-vi a send-keys -X cancel
bind-key -T copy-mode-vi q send-keys -X cancel
bind-key -T copy-mode-vi v send-keys -X begin-selection
bind-key -T copy-mode-vi y send-keys -X copy-selection
bind-key -T copy-mode-vi C-V send-keys -X rectangle-toggle
bind-key -T copy-mode-vi / command-prompt -i -p "(search down)" "send-keys -X search-forward-incremental \"%%%\""
bind-key -T copy-mode-vi ? command-prompt -i -p "(search up)" "send-keys -X search-backward-incremental \"%%%\""

# Allow directly entering search mode from terminal mode
# Requires rebinding ? which shows help to h which is unused
#bind-key -T prefix / copy-mode \; command-prompt -i -p "(search down)" "send-keys -X search-forward-incremental \"%%%\""
#bind-key -T prefix ? copy-mode \; command-prompt -i -p "(search up)" "send-keys -X search-backward-incremental \"%%%\""
#bind-key -T prefix h list-keys
```
