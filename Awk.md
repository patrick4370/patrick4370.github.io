# Awk 

![awk logo](https://upload.wikimedia.org/wikipedia/commons/thumb/3/39/Official_gnu.svg/131px-Official_gnu.svg.png)

### Remove empty lines 
`awk 'NF' <file>`

### Multi-line records

Awk is an excellent tool for reading in and processing structured data, such as the system's /etc/passwd file. /etc/passwd is the UNIX user database, and is a colon-delimited text file, containing a lot of important information, including all existing user accounts and user IDs, among other things. In my previous article, I showed you how awk could easily parse this file. All we had to do was to set the FS (field separator) variable to ":".

By setting the FS variable correctly, awk can be configured to parse almost any kind of structured data, as long as there is one record per line. However, just setting FS won't do us any good if we want to parse a record that exists over multiple lines. In these situations, we also need to modify the RS record separator variable. The RS variable tells awk when the current record ends and a new record begins.

As an example, let's look at how we'd handle the task of processing an address list of Federal Witness Protection Program participants:

```
Jimmy the Weasel
100 Pleasant Drive
San Francisco, CA 12345

Big Tony
200 Incognito Ave.
Suburbia, WA 67890
```

Ideally, we'd like awk to recognize each 3-line address as an individual record, rather than as three separate records. It would make our code a lot simpler if awk would recognize the first line of the address as the first field ($1), the street address as the second field ($2), and the city, state, and zip code as field $3. The following code will do just what we want:

```awk
BEGIN {
    FS="\n"
    RS=""
}
```

Above, setting FS to "\n" tells awk that each field appears on its own line. By setting RS to "", we also tell awk that each address record is separated by a blank line. Once awk knows how the input is formatted, it can do all the parsing work for us, and the rest of the script is simple. Let's look at a complete script that will parse this address list and print out each address record on a single line, separating each field with a comma.

```awk
BEGIN {
    FS="\n"
    RS=""
}
{ print $1 ", " $2 ", " $3 }
```


If this script is saved as address.awk, and the address data is stored in a file called address.txt, you can execute this script by typing awk -f address.awk address.txt. This code produces the following output:

`Jimmy the Weasel, 100 Pleasant Drive, San Francisco, CA 12345`  
`Big Tony, 200 Incognito Ave., Suburbia, WA 67890`


[Index](index.md)
