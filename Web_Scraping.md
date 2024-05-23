
*Create Variable for Arch Download URL*

`arch_dir="https://archlinux.org/download/"`

*Download the Arch Linux Download page*

`curl -s ${arch_dir} > arch.html`

*Retrieve current release date*

`rel_date=$(cat arch.html | html2text | awk '/**Current Release:**/ {print $4}')`

*Retrieve MD5sum*

`md5_value=$(cat arch.html | html2text | awk '/**MD5:**/ {print $3}')`

*Obtain download directory from Mirror List*

`dwn_dir=$(cat arch.html | grep aarnet | htmlq -a href a)`

*Construct Current Filename*

`filename=$(echo archlinux-${rel_date}-x86_64.iso)`

*Get the basename*

`curr_iso=${curr_iso_path##*/}`

*Retrieve local Arch ISO*

`curr_iso_path=$(find ~/Downloads/Arch/ -maxdepth 1 -type f -iname "archlinux*.iso")`

*Get the date from the filename*

`local_file_date=${curr_iso:10:10}`

*Convert Date to a format acceptable by date command*

`rel_date=$(echo ${rel_date} | sed 's/\./-/g')`

`local_file_date=$(echo ${local_file_date} | sed 's/\./-/g')`

*Convert to Epoch for comparing dates*

`local_epoch=$(date -d "$local_file_date" +"%s")`

`remote_epoch=$(date -d "$rel_date" +"%s")`

*Compare dates*

``` 
if [[ $remote_epoch -gt $local_epoch ]];
then
    # Do stuff to download ARCH ISO
fi 
```

*Extract MD5sum from md5sums.txt*

`md5_value=$(cat md5sums.txt | awk '/archlinux-2022.08.05-x86_64.iso/ {print $1}'`

[Arch Linux](Arch_Linux.md)
