+++
isStarred = false
toc = true
tocOpen = true

date = '2024-10-20T19:30:48+05:30'
title = 'Terminal - 5 Shell Scripting'
description = 'Instroduction to shell scripting in terminal'
+++


***Objective***
Shell script that runs a command or a series of commands for a fixed set of files.
Run a shell script from the command line.
Using a shell script that operates on a set of fines defines by the user on the command line.
Creating a pipeline that included shell scripts.


## Shell Script 

We are going to take the commands we have repeat frequently and save them in files so that we can re-run all those operations again later by typing a single command.
So ***Shell Scripts*** are actually small programs.

`$ cd alkanes`
`$ nano middle.sh`  nano create middle.sh which will contain the command to be run.

`head -n 15 octane.pdb | tail -n 5`   is types into the file, saved and closed.
this collects the lines 11-15 of the file `octane.pdb`

Once the file is saved in the directory, we can ask the shell(bash) to execute it.
***bash [filename]*** runs the commands saved in a file
`$ bash middle.sh`

To make the script more versatile we can remove octane and replace it with `$1`.
Which means the first file name(or other argument) on the command line.
`head -n 15 "$1" | tail -n 5`

In case filename happens to contain space `$1` is put in `""`
Now we can provide different arguments.
`$ bash middle.sh octane.pdb`
`$ bash middle.sh pentane.pdb`


The text editors `ms word, libreoffice` are not just basic text editors, the files are `.docx`
The files also contain also contain formatting information about fonts, headings etc.
Commands like head expect only character to be provided so it is better to save script files using plain text editor as plain text.


To make sure the numbers for head and tail can be altered by arguments,
they can also be taken as `$1 $2 $3` in `middle.sh`.

`head -n "$2" "$1" | tail -n "$3"`
`$ bash middle.sh pentane.pdb 15 5`   now 15 and 5 are arguments for head and tail
`$ bash middle.sh pentane.pdb 20 5`


## Comments

To make sure `middle.sh` is understandable to others on what it does we can add comments which starts with `#` character and runs to the end of the line which is ignored.
`# Select lines from the middle of a file.`
`# Usage: bash middle.sh filename end_line num_lines `

`head -n "$2" "$1" | tail -n "$3"`



## `$@` To process many types of files  

`$ wc -l *.pdb | sort -n`

Used to sort based on number of lines in the `.pdb` files,
but it only sorts `.pdb` files ans `sort -n` only sorts numerically.

We can use `$1 $2` but we might not know how many files there are.
Instead we can use `$@` which means ***All of the command-line arguments to the shell script***.
We should also put it in double quotes to handle spaces in argument `"$@"`

`$ nano sorted.sh`

`# sort files by their length.`
`# Usage: bash sorted.sh one_or_more_filenames`
`wc -l "$@" | sort -n`

`$ bash sorted.sh *.pdb ../creatures/*.dat`


### For sorting unique

Script to find unique species in `scv` files where species is the second data field.
This script accepts any number of file names as a command line arguments.
Loops over all files
```c
for file in $@
do 
	echo "Unique species in $file:"
	# Extract species names
	cut -d , -f 2 $file | sort | uniq
done
```


