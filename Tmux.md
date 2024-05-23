# Tmux

![Tmux](./images/tmux-logo-medium.png)

## Useful Links

[Tmux Templating](https://thoughtbot.com/blog/templating-tmux-with-tmuxinator)  
[Tmux Cheat Sheet & Quick Reference](https://tmuxcoeatsheet.com/)  

## Tmux Configuration 

```
#   _
#  | |_ _ __ ___  _   ___  __
#  | __| '_ ` _ \| | | \ \/ /
#  | |_| | | | | | |_| |>  <
#   \__|_| |_| |_|\__,_/_/\_\
# 
# Sat 19-06-2021 14:41 +1000

# remap prefix from 'C-b' to 'C-a'
unbind C-b
set -g prefix C-z
bind C-z send-prefix

# 256 Colours
set -g default-terminal "tmux-256color"

# switch panes using Alt-arrow without prefix
bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

# helps in faster key repetition
set -sg escape-time 0

# Shift arrow to switch windows
bind -n S-Left previous-window
bind -n S-Right next-window

# Set easier window split keys
bind-key v split-window -h
bind-key h split-window -v

# Start tmux in xterm-256color terminfo
set -g default-terminal "xterm-256color"

# Enable mouse mode (tmux 2.1 and above)
set -g mouse on

# Lengthen status bar display time
set-option -g display-time 2000

# Resize the current pane using Alt + direction
bind -n M-k resize-pane -U 5 # Up
bind -n M-j resize-pane -D 5 # Down
bind -n M-h resize-pane -L 5 # Left
bind -n M-l resize-pane -R 5 # Right

# Start zsh properly
set -g default-command "/usr/bin/zsh"

# set -ga terminal-overrides ',*:Ss=\E[%p1%d q:Se=\E[2 q'
set -ga terminal-overrides ',*:Tc' # this is for 256 color
set -ga terminal-overrides '*:Ss=\E[%p1%d q:Se=\E[ q' # this is for the cursor shape']]'''
set -ga terminal-overrides ',xterm*:TC'

# Reload ~/.tmux.conf
bind r source-file ~/.config/tmux/tmux.conf \; display-message " Reloaded config"

# don't rename windows automatically
set-option -g allow-rename off

# start session number from 1 rather than 0
set -g base-index 1

# start pane number from 1 similar to windows
set -g pane-base-index 1

# Make the current window the first window
bind T swap-window -t 1

# pane movement
bind-key j command-prompt -p "join pane from:"  "join-pane -s '%%'"
bind-key s command-prompt -p "send pane to:"  "join-pane -t '%%'"

# Toggle Status Bar
bind-key -n C-F3 set-option -g status #Ctrl+F3 Combo

# switch between sessions
bind -r ( switch-client -p
bind -r ) switch-client -n

# Create new window and prompt for name - Prefix + C
bind-key C command-prompt -p "Name of new window: " "new-window -n '%%'"

# copy and paste
set-window-option -g mode-keys vi
bind-key -T copy-mode-vi v send-keys -X begin-selection
bind-key -T copy-mode-vi y send-keys -X copy-selection
bind-key -T copy-mode-vi r send-keys -X rectangle-toggle

# Load plugins here
# Load tmux plugin tmux-resurrect
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-resurrect'
set -g @plugin 'olimorris/tmux-pomodoro-plus'
set -g @plugin 'Alkindi42/tmux-bitwarden'
set -g @plugin 'tmux-plugins/tmux-yank'
set -g @plugin 'sainnhe/tmux-fzf'
set -g @plugin 'jaclu/tmux-menus'
set -g @plugin 'tmux-plugins/tmux-online-status'
set -g @plugin 'christoomey/vim-tmux-navigator'

# Online Plugin
set -g @online_icon "🟢"
set -g @offline_icon "🔴"

# Pomodoro Configuration
set -g @pomodoro_start 'p'                               # Start a Pomodoro with tmux-prefix + p
set -g @pomodoro_cancel 'P'                              # Cancel a Pomodoro with tmux-prefix key + P
set -g @pomodoro_mins 25                                 # The duration of the pomodoro
set -g @pomodoro_break_mins 5                            # The duration of the break after the pomodoro:
set -g @pomodoro_on " 🍅 "                               # The formatted output when the pomodoro is running
set -g @pomodoro_complete "#[text=#ffffff]✅ "           # The formatted output when the break is running
set -g @pomodoro_notifications 'on'                      # Enable desktop notifications from your terminal
set -g @pomodoro_sound 'on'                              # Sound for desktop notifications

set -g default-terminal "tmux-256color"
set -g @bw-session 'BW_SESSION'
set -g @bw-copy-to-clipboard 'on'

bind -r ( switch-client -p
bind -r ) switch-client -n

# tmux-yank
set -g @yank_selection 'clipboard' # or 'secondary' or 'clipboard'
set -g @yank_selection_mouse 'clipboard' # or 'primary' or 'secondary'

# status bar theme

# set-option -g status-style bg=blue
set-option -g status-position bottom
set-option -g status-justify centre
set-option -g status-bg "#3B3B37" 

set-option -g status-left-length 50
set-option -g status-right-length 50
set-option -g status-left ' #[fg=colour255]#(echo "Session: ")#[fg=colour11]#{session_name} #{pomodoro_status} '
set-option -g status-right ' #[fg=colour15]Online: #{online_status} #[fg=colour250]#{?window_zoomed_flag, [👀] , [z]} '
set-option -g status-left-style bg="#07499D"
set-option -g status-right-style bg="#07499D"

set-option -g window-status-format '#[fg=colour11]#{window_index}#(echo ":")#[bold,fg=colour15]#{window_name}#[bold,fg=colour160]#{window_flags} '
set-option -g window-status-current-format '#[bold,fg=colour232,bg=colour26] #{window_index}#(echo ":")#[bold,fg=colour11]#{window_name}#[fg=colour160]#{window_flags} '
set -g message-style bg=colour22,fg=colour15

set-option -g automatic-rename on
set-option -g status-interval 1
#[bold,fg=242] #(uname -r)

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.config/tmux/plugins/tpm/tpm'
```

[Index](index.md)
