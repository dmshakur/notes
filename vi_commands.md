# Command Summary

## Starting `vi`
* `vi filename`: edit a file named "filename".
* `vi newfile`: Create a new file named "newfile".

## Entering text
* `i`: Insert text left of the cursor.
* `a`: Append text right of the cursor.
 
## Moving the cursor
* `h`: Left one space.
* `j`: Down one line.
* `k`: Up one line.
* `l`: Right one line.

## Basic editing
* `x`: Delete character.
* `nx`: Delete `n` characters.
* `X`: Delete character before the cursor.
* `dw`: Delete word.
* `ndw`: Delete n words.
* `dd`: Delete line.
* `ndd`: Delete `n` lines.
* `D`: Delete characters form cursor to end of line.
* `r`: Replace charcter under cursor.
* `cw`: Replace a word.
* `ncw`: Replace `n` words.
* `C`: Change text from cursor to end of line.
* `o`: Insert blank line below cursor.
* `O`: Insert blank line above cursor.
* `J`: Join succeeding line to currect cursor line.
* `nJ`: Join `n` succeeding lines to current cursor line.
* `u`: Undo last change.
* `U`: Restore current line.

## Moving around in a file
* `w`: Forward word by word.
* `b`: Backward word by word.
* `$`: To end of line.
* `0`: To beginning of line.
* `H`: To top line of screen.
* `M`: To middle line of screen.
* `L`: To last line of screen.
* `G`: To last line of file.
* `lG`: To first line of file.
* `<ctrl>f`: Scroll forward one screen.
* `<ctrl>b`: Scroll backward one screen.
* `<ctrl>u`: Scroll down one-half screen.
* `<ctrl>u`: Scroll up one-half screen.
* `n`: Repeat last search in same direction.
* `N`: Repeat last search in opposite direction.

## Closing and saving a file
* `ZZ`: Save file and then quit.
* `:w`: Save file.
* `:q!`: Discard changes and quit file.
