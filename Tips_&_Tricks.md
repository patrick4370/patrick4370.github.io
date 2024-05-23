# Tips and Tricks

## How to set 4 space tab in bash

Use the tabs command to change the behavior:

`$ tabs 4
`
```sh
$ echo -e "a\tb"      
a   b
$ tabs 12
```

`$ echo -e "a\tb" 
a           b
`
## basename & extension stripping 

*Basename*

if the file is `/home/patrick/Documents/e7440.pdf
`
```sh
filename="/home/patrick/Documents/e7440.pdf"
basefile="${filename##*/}" # Returns e7440.pdf
fileext="${basefile%.*}"   # Returns e7440

${filename##*/} returns the filename minus the path
${filename%/*}  returns the path minus the filename
${filename%.*}  returns the filename minus the file extension

echo $filename
/home/patrick/Documents/e7440.pdf

echo "${filename##*/}"
e7440.pdf

echo "${filename%/*}"
/home/patrick/Documents

echo "${filename%.*}"
/home/patrick/Documents/e7440
```

[Bash Shell](Bash_Shell.md)
