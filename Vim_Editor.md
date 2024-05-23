# Vim Editor 

<img src="./images/vimlogo.png" alt="image" width="200" height="auto">

_Toggle Upper Case/Lower Case_

` *Highlight section with Ctrl-v* 
 *Press ~*`                      
                                 
_Renumber a section_
 
`*Highlight the numbers using ctrl-v*
*Press g and then Ctrl-a*`      

_Buffers_
Here are the essential buffer commands:

```
:ls             List the current buffers (including their numbers).
:b <number>     Display the buffer with the given number.
:b <partial>    Display the first buffer matching the partial name (or press Tab for name completion).
:bd             Delete the current buffer; will fail if unsaved (nothing is deleted).
:bd!            Delete the current buffer; will discard any changes (changes are lost). 
```

_Splits_

You can use :split and :vsplit to divide the current area into two windows with
the same buffer. If you supply an argument then one of the new windows is
created with the argument as a file name used for the buffer in the new window

To gain more control over how the splits are created, you can combine the
:vertical, :leftabove and :rightbelow commands. Also of use are the the :sfind
and :sb commands.

Examples

`:vertical sb 3`
Create a vertical split and show buffer number 3 in the window to the left.
	
`:vertical rightbelow sfind file.txt`
Create a vertical split and read file.txt into the buffer in the right window.
		
`:rightbelow sfind file.txt`
Create a horizontal split and read file.txt into the buffer in the bottom window.
			
Navigating splits
Use Ctrl-W followed by one of the hjkl movement keys. 

## Statusline

```
" Function to return file size
function! FileSize()
    let bytes = getfsize(expand("%:p"))
    if bytes <= 0
        return "Empty"
    endif
    if bytes < 1024
        return bytes . "bytes"
    else
        return (bytes / 1024) . "Kb"
    endif
endfunction

"define 5 custom highlight groups
hi User1 ctermbg=22     ctermfg=white   cterm=bold
hi User2 ctermbg=88     ctermfg=white
hi User3 ctermbg=26     ctermfg=white

" Array of editing modes
let g:currentmode={
       \ 'n'      : 'NORMAL ',
       \ 'v'      : 'VISUAL ',
       \ 'V'      : 'V·Line ',
       \ "\<C-V>" : 'V·Block ',
       \ 'i'      : 'INSERT ',
       \ 'R'      : 'Replace ',
       \ 'Rv'     : 'V·Replace ',
       \ 'c'      : 'Command ',
       \}

" The StatusLine
set statusline=                                                 " Start Status Line
set statusline+=%1*                                             " Switch to User1 highlight
set statusline+=\ %{toupper(g:currentmode[mode()])}             " Display the current editing mode
set statusline+=%{&paste?'PASTE':''}\                           " Show PASTE mode
set statusline+=%2*                                             " Switch to User2 highlight
set statusline+=\ [%{strlen(&ft)?&ft:''}]\                      " Filetype
set statusline+=%3*                                             " Switch to User3 highlight
set statusline+=\ %t                                            " Show filename
set statusline+=\ %{&modified?'[+]':'[\ ]'}\                    " Modified flag
set statusline+=\ Ln:\ %l\:%L\                                  " Line number of total lines
set statusline+=Col:\ %c\                                       " Column number
set statusline+=Pos:\ %p%%\                                     " Percentage thru FileSize
set statusline+=%=                                              " Switch to right alignment
set statusline+=%{&spell?'[SPELL]':''}                          " Show when SPELL is being used
set statusline+=%3*                                             " Switch to User3 highlight
set statusline+=%{&ro?'[RO]':'[W]'}                             " Test if file is Read Only
set statusline+=[%{strlen(&fenc)?&fenc:&enc}]                   " File encoding
set statusline+=\ Buf:[%n]\                                     " Show buffer number 
set statusline+=%{FileSize()}\                                  " Display file size
set statusline+=%2*                                             " Switch to User2 highlight    
set statusline+=\ Dec:\ %b\                                     " Display decimal value of character under cursor 
set statusline+=Hex:\ %B\                                       " Display hexadecimal value of character under cursor
set statusline+=%*                                              " Switch back to statusline highlight

set noshowmode      " To get rid of --INSERT-- etc
set noshowcmd       " To get rid of display of last command
set shortmess+=F    " To get rid of the file name displayed in the command line bar
```

## Reformat Text

Set textwidth to 80 (`:set textwidth=80`), move to the start of the file (can be
done with `Ctrl-Home` or `gg`), and type `gqG`.

gqG formats the text starting from the current position and to the end of the
file. It will automatically join consecutive lines when possible. You can place
a blank line between two lines if you don't want those two to be joined
together.

Reformat the rest of the current paragraph; for this behavior, use `gq`.

## Windows

*Put a buffer into a window*

`:split | buffer<N>`

`:vsplit | buffer<N>`


| Key                 | Description                                        |
|---------------------|----------------------------------------------------|
| CTRL+w, =           | Makes all splits equal size                        |
| CTRL+w, c           | Closes a window but keeps the buffer               |
| CTRL+w, o           | Closes other windows, keeps the active window only |
| CTRL+w, r           | Moves the current window to the right              |
| CTRL+w, s           | Opens a new horizontal split                       |
| CTRL+w, v           | Opens a new vertical split                         |
| CTRL+w, Left Arrow  | Moves the cursor to the window on the left         |
| CTRL+w, Right Arrow | Moves the cursor to the window on the right        |
| CTRL+w, Up Arrow    | Moves the cursor to the window above               |
| CTRL+w, Down Arrow  | Moves the cursor to the window below               |

## Vim Registers

Save text for later retrieval

## The 10 Registers

1. [The unnamed register](The unnamed register) ""
2. 10 numbered registers "0 to 9"
3. The small delete register "-
4. 26 named registers "a to z" or "A to Z"
5. 3 read-only registers ":, "., "%
6. Alternate buffer register "#
7. The expression register "=
8. The selection registers "* "+
9. The black hole register "_
10. Last search pattern register "/

To access a register type

### Normal Mode

`"<register><action>`

Where:  
**\<register\>** is the register you want   
**\<action\>** is an action like paste

eg. "1p will paste the text into your document from register 1

### Insert Mode

`\<CTRL-r\>\<register\>`

Where:  
**\<CTRL-r\>** is control key plus r on the keyboard  
**\<register\>** is the register name

## Autocompletion

### Triggering

Vim's autocompletion can be triggered with the `<C-p>` and `<C-n>` chords, which select the *previous* and *next* items in the word list, respectively.

| Command      | Type of Completion      |
|--------------|-------------------------|
| `<C-n>`      | Generic keywords        |
| `<C-x><C-n>` | Current buffer keywords |
| `<C-x><C-i>` | Included file keywords  |
| `<C-x><C-]>` | tags file keywords      |
| `<C-x><C-k>` | Dictionary lookup       |
| `<C-x><C-l>` | Whole line completion   |
| `<C-x><C-f>` | Filename completion     |
| `<C-x><C-o>` | Omni completion         |

Table: Types of autocompletion

[Index](index.md)
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
