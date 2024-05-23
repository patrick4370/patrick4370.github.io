# Sed Basics

## Remove until end of line

If the output of a command as superflorous characters, eg 192.168.10.4/24 as the
/24, we can remove them with sed.

` echo "192.168.10.4/24" | sed 's,/.*,,'  `

This will return 192.168.10.4

[Index](index.md)
