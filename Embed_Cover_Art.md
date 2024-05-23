# Embed Album Art

Well, you could want to actually embed the cover image into your mp3 files. To do this simply change to the directory that holds your mp3s and the cover image and run the following:

```Shell
for i in *.mp3
do
    eyeD3 --add-image cover.jpg:FRONT_COVER "$i"
done
```

[Audio](Audio.md)
