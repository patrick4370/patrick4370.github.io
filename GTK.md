# GTK

## How to Make File Chooser Dialog default to Current Working Directory

### For GTK2 Apps

Edit `~/.config/gtk-2.0/gtkfilechooser.ini`

Change StartupMode=recent to StartupMode=cwd and save the file.

### For GTK3/GTK4 Apps

When terminal opens, run command to set current working directory as default for GTK3 file chooser:

`gsettings set org.gtk.Settings.FileChooser startup-mode 'cwd'`

For GTK4 applications, run this command instead in terminal window:

`gsettings set org.gtk.gtk4.Settings.FileChooser startup-mode 'cwd'`

[Index](index.md)
