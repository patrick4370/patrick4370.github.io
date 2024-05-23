
## Find File System Type On a Drive

`# file -sL /dev/sdx1`

## Wrong Application Opening 

Copy /usr/share/applications/mimeinfo.cache to ~/.local/share/applications

`# cp /usr/share/applications/mimeinfo.cache ~/.local/share/applications`

Look through the file and change as appropriate.

Overgrive was opening EasyTag when selecting "Open Google Drive Folder"

## Extract String in output of zbarimg

`zbarimg -q Sourceforge_QR_Code.png | grep -o -P '(?<=secret=).*?(?=&)'
`
The string returned is

`QR-Code:otpauth://totp/Twitter:pheffernan4370@gmail.com?secret=ABC123ABC123&issuer=Twitter
`
and running that string through the above returns

`ABC123ABC123
`
## Disable MOTD without root access

`touch $HOME/.hushlogin`

[Shell Programming](Shell Programming)

###### test
