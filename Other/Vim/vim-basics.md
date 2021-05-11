# Vim basics

# VIMTUTOR - Up to Start - lesson 5

***Navigation***
`h` - cursor left
`l` - cursor right
`j` - cursor down
`k` - cursor up
`w` - jump forward one word
`0` (zero) - move to start of line
`G` - move to bottom of the file
`gg` - move to start of the file
`%` - find matching (), [], {}

***Do-x-Times***
`1-0` - number with operator is do operator number of times
`2dd` - delete 2 lines
`4dw` - delete 4 words
`5w` - jump 5 words forward

***Edit***
`i` - insert mode	(cursor before char)
`a` - append mode (cursor after char)

***Deleting***
`x` - delete next char
`dw` - delete word
`d$` - delete till end of line
`de` - delete to the end of the current word (including last char)
`d(direction from nav)` - delete everything following that direction
`dd` - delete entire line

***Undo+Redo***
`u` - undo last command
`U` - fix a whole line
`ctrl+r` - redo

***Put***
`p` - put deleted word after cursor
`p` - put deleted line under cursor

***Replace***
`r[char]` - replace next character with given char
`c[num][direction]` - remove/replace num of chars in the given direction
`c[num]$` - remove/replace number of words after
`ce` - replace the rest of the word
`:s/old/new`   - replace first occurrence of 'old' to 'new'
`:s/old/new/g` - replace global occurrence of 'old' to 'new'

***Search***
`/[phrase]` - search for the given phrase
`n` - search for same phrase again
`N` - search for same phrase again opposite direction
`?[phrase]` - search in opposite direction
`ctrl+O` - go back to where you were
`ctrl+I` - goes forward

***Save-Quit***
`:q` - quit file
`:q!` - quit without saving changes
`:wq` - write file then quit

***Show-Info***
`ctrl+g` - show file name and current location