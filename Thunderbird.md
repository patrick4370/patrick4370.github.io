---
title: Thunderbird
date: May 21 2024
---

# Thunderbird

<img src="./images/thunderbird.png" alt="image" width="300" height="auto"> 

## Remove Thunderbird's (empty) Personal Address Book

In the extended configurations area set the value of `ldap_2.servers.pab.dirType` to `-1`

## CardDav

In Address Book, File/New/CardDAV Address Book... Enter your User Name (usually the email address) and the CardDAV URL. For Google Contacts, it is:

`https://www.googleapis.com/carddav/v1/principals/username@gmail.com/lists/default/` 

Change `username` to your gmail account name.

## Increase textwidth in plain text emails

Open the `about:config` in settings and increase the value of 72 to a higher number under `mailnews.wraplength`

## Increase System Font Size


1. End Thunderbird.
2. Create a folder “chrome” in your thunderbird user profile folder if it does not exist.
4. Create a file called `userChrome.css` if it does not exist.
4. Enter following data into the file: 

```
* {
font-family: Verdana, Arial, Sans Serif !important;
font-weight: normal !important;
font-size: 12px !important;
}
```

You can change font size and used font as you want.

[Index](index.md)
