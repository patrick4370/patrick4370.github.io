# QT Themes

If you launch via a menu, and a QT theme doesn't stick, but shows by launching
in the terminal, change the desktop file so the Exec line runs the environment
variable like so.

```
[Desktop Entry]
Version=1.0
Name=MakeMKV
Comment=DVD and Blu-ray to MKV converter and network streamer
Exec=env QT_QPA_PLATFORMTHEME=gtk2 makemkv
Icon=makemkv
Terminal=false
Type=Application
Categories=AudioVideo;Qt;
```

[Arch Linux](Arch_Linux.md)
