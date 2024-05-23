# Windows 

This will be filled with Windows fixes

## Repairing Bootloader

#### Save Bootloader Information
`bcdedit /export C:\bcd.bak`

#### Import Bootloader Information
`bcdedit /import C:\bcd.bak`

#### Access Drive
```
    X:\> diskpart
   
    DISKPART> list diskpart
    DISKPART> sel disk 0
    DISKPART> list vol
```
Look for the EFI partition. It will be formatted as FAT32<br /> 

*Assign a driver letter to the volume*
```
    DISKPART> sel vol 1
    DISKPART> assign letter=v
    
    DISKPART> exit
```

*Change to the drive letter that was assigned*

```
X:\> V:

V:\> dir
# We should see an EFI directory

V:\> cd EFI
V:\EFI> cd Microsoft
V:\EFI\Microsoft> cd boot
V:\EFI\Microsoft\Boot> C:

C:\> format v: /fs:FAT32
# Formats the EFI partition to FAT32

C:\> V:
# Will be empty

V:\> C:
# Verify Windows directoy

C:\> dir
# Look for Windows and Users directories

C:\> bcdboot c:\windows /s v: /f UEFI

# Check V:\EFI\Microsoft\Boot by running bcdedit and looking at output

# Close command prompt and shutdown PC
# Restart and see if it boots to Windows
```

[Index](index.md)
