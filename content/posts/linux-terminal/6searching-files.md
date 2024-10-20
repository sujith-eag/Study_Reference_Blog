+++
isStarred = false
toc = true
tocOpen = true

date = '2024-10-20T19:35:53+05:30'
title = 'Terminal - 6 Searching in terminal'
description = 'Using grep, find and other ways to find things in in files'
+++


***Overview***
Use `grep` to select lines from text files that match simple patterns.
Use `find` to find files and directories whose names match simple patterns.
Use the output of one command as the command-line argument to another command.
Understanding 'text' & 'binary' files, and why many common tools don't handle the latter well.


## `grep`

`grep` is 'global/regular expression/print'.
A common sequence of operations in Unix text editors.
[[grep]] finds and prints lines in files that match a pattern.

`$ grep not haiku.txt`  gets all lines with `not` in it, doesn't have to be just this word.
`$ grep "is not" haiku.txt`  searching for a phrase.
`$ grep "not" haiku.txt`  using " " for single word also like for double word makes it easier.

`$ grep -w "The" haiku.txt`  
`-w` option will limit matches to the word boundaries, nothing else like Thesis will be result.

`$ grep -n "it" haiku.txt`   
`-n` numbers the results with the line numbers.

`$ grep -n -w "the" haiku.txt`     combining options.

`$ grep -n -w -i "the" haiku.txt`     
`-i` makes the search case sensitive, the, The, THE

`$ grep -v -n -w "the" haiku.txt`   
`-v` inverts the search, getting all lines without THE

`$ grep -r "Yesterday" `   
`-r` searches recursively through all the files in the directory


## Wildcards in `grep` searches

The technical term for these are ***regular expressions*** which is the `re` in `grep`.

`$ grep -E "^.o" haiku.txt` 
Finding the lines with words having o in second position.

`^`  in the pattern anchors the match to the start of the line.
the `.` matches a single character (just like `?` in the shell),    
o matches the o
using `-E` allows using the pattern without being interpreted, like if it had `*` 

so `^.o` is  `^` from beginning, `.`any single character, `o` and o.... so o in second place


## `find`

While `grep` finds lines in files `find` command finds themselves.

`$ find .`   finds and lists all the files and directories under the current directory.

Finding and filtering using the options,
`$ find . -type d`    `-type d` means 'things that are directories'   so lists only directories.

`$ find . -type f`     lists all the files only under the current directory and its directories.


### Finding by name using `-name`

`$ find . -name *.txt`    this finds files by only in current directory because,
the `*` got expanded before execution of command so what actually got executed was,
`$ find . -name numbers.txt`

So only that got listed.

Putting it in quotes will solve this issue.
`$ find . -name "*.txt"`
now `find` will get all `.txt` files in all directories 


## `ls` vs `find`

`ls` lists everything it can while `find` searches for things with certain properties

`$ wc -l $(find . -name "*.txt")`

Doing the word count for all the files under the directories by using `$()`

`$([command])` inserts a command's output in place. 
So the shell first executes what is inside the ( ) and does rest later.

`wc -l $(find . -name "*.dat") | sort -n`
Find all `.dat` files under and in the directory,
get word counts for all those files,
sort them numerically.