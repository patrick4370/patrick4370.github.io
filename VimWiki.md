# VimWiki

<img src="./images/vimwiki.png" alt="image" width="200" height="auto">

I have taken the decision to save all my notes in Markdown format in vimwiki. To
achieve this, I have the following configuration in my `.vimrc` file.

```
Plug 'vimwiki/vimwiki' 

let g:vimwiki_list = [{'path': '~/Documents/Vimwiki_md/', 'syntax': 'markdown', 'ext': '.md', 'links_space_char': '_'}]
let g:vimwiki_listsyms = ' ✗○●✓'
let g:vimwiki_markdown_link_ext = 1
let g:vimwiki_global_ext = 0
let g:vimwiki_automatic_nested_syntaxes = 1
let g:vimwiki_dir_link = 'index'
```
The `links_space_char` ensures that my file names do not have spaces in them.
The `vimwiki_markdown_link_ext = 1` adds the .md extension to my note links when
the file is created.

## Resize an image in Markdown

Use the following code  

`<img src="/img/contact.png" alt="image" width="300" height="auto">`

[index](index.md)

