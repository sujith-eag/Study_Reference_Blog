+++
isStarred = false
toc = true
tocOpen = true

date = '2024-10-20T18:35:49+05:30'
title = 'Terminal - 2 Working With Files'
description = 'Commands and methods used to work with files from terminal'
+++


## Creating Directories 

Open where a directory has to added.
`mkdir [name]`  to 'make directory' in the current directory.
	Using relative path without leading slash

`-p`  for multiple directories
`mkdir -p` creates a directory with nested sub-directories in a single operation
`mkdir -p ../project/data ../project/results` 

`ls -R` to list all nested sub directories within a directories

To make a directory `2016` which has `data` and that has 2 directory `processed` and `raw`
```c
 # one                              # two
mkdir 2016                        mkdir 2016
mkdir 2016/data                   cd 2016 
mkdir 2016/data/processed         mkdir data
mkdir 2016/data/raw               cd data
.                                 mkdir raw processed   

# three
mkdir -p 2016/data/raw
mkdir -p 2016/data/processed   # `-p` is creating any intermediate directory
```   

`mkdir north south pacific` will create 3 different directories


## Naming Conventions

* Don't use spaces as arguments need space separation in command line
* Use `_` or `-` instead of space
* Don't start with `-` as it will be considered as option/flag
* Stick with `0-9, a-z . - _`  as other symbols have different meaning
* To refer to names with spaces or other special characters, surround the name in single quotes ' '

***Single Quotes***
Enclosing characters in single quotes ' ' preserves the literal value of each character within the quotes.

***Escape Character***
a non-quoted backslash `\` is the escape character.
It preserves the literal value of the next character that follows, with exception of newline.


## Create a text file

### Using nano editor

`nano` text editor is used to create a `txt` file
`nano draft.txt`   will open nano text editor, data can be typed and then saved(many more options) commands are accessed by holding down `Ctr` 

`nano` can only work with plain character data, no tables or images
`nano` can do only this basic operation. Programmers use `Emacs` or `Vim`.
Graphical editors such as `Gedit` or `VScode`
On windows there are `Notecode++`,  Windows also has `notepad` that can run like `nano`

### `touch` command

`touch my_file.txt` creates a blank text file
`touch  <name.txt>`  to make a file  [[touch]]

### `rm` Removing a file using    [[rm - remove]]

`rm my_file.txt`    file gets removed
`rm -i`  will ask for confirmation before the deletion
`rm` works only on files, not on directories  `rm thesis`  raises an error
`rm -i thesis/quote.txt` will work after confirmation

We can remove a directory and all its contents by using the recursive `-r`
`rm -r thesis`   `rm -r -i`

`rm -i *.txt`  removing all `.txt` file in directory with permission needed for each

Shell does not have any trash bin so any file deleted is actually deleted


## Moving files and directories

### Renaming by moving a file to new name!!

`mv [old] [new]`  moves or renames a file or directory [[mv - move]]

While in directory behind the directory with file
`$ mv trial/draft.txt  trial/quotes.txt`
The `draft.txt` file is moved to `quotes.txt`  which is similar to renaming the file.

While in the same directory
`$ mv draft.txt quotes.txt`

When it is moved to a a directory with same file name, it will delete the previous file silently. 
`mv` will not ask for confirmation by default. 
An additional option, `mv -i` `mv --interactive` will cause `mv` to request such confirmation.

File can be moved to directory also
`$ mv trial/quotes.txt`  this will move it from that directory to current one.

`$ mv sucrose.dat maltase.dat ../raw`    moving two files to raw file in the parent directory


## Copying files and directories

`cp` works similar to `mv`, but copies the file [[cp - copy]]

`cp [old] [new]` copies a file
`$ cp quotes.txt thesis/quotation.txt`
copies file to another directory with different name

A directory and all its contents are copied by using recursive option `-r`  (like backing up directory)
`$ cp -r thesis thesis_backup`

`-r` is used to copy the directory, if it is not included, the directory will be omitted


## Operation with multiple files and directories

Copying or moving several files can be done by giving multiple files,

If given more than one file names followed by a directory name(directory as last argument) `cp` copies the files to the named directory
`$ mkdir backup`
`$ cd cretures/minotaur.dat creatures/unicorn.dat backup/`

`$ cd minotaur.dat unicorn.dat basilisk.dat`   
all three are file names, makes a error, this can be handled by using wildcards.


## Wild Cards

'wildcards' are special characters that can be used to represent unknown characters or sets of characters when navigating the Unix system.

`ethane.pdb   methane.pdb   propane.pdb   pentane.pdb`
`*` is a wild card which represents 0 or more characters.
`*.pdb`  represents every file that ends with `.pdb`
`*ethane.pdb` represents ethane and methane
`p*.pdb` represents files that begin with `p` and has `.pdb`

`?` is also a wildcard, but represents exactly one character
`?ethane.pdb`  represents only `methane.pdb`

Wild cards can be used in combination with one another
`???ane.pde`   is any three characters followed by `---ane.pde`

`ls *t*ane.pdb`    gives most of names
`ls *t?ne.*`          gives octane pentane
`ls *t??ne.pdb`    ethane methane
`ls ethane.*`       only ethane
When a shell sees a wildcard it expands the wildcard to create a list of matching filenames before running the preceding command.

`*.pdf` in directory with `*.pdb` will throw error


### Using wildcards for copying

`$ cp *dataset* backup/datasets`  copy anything having dataset as name to datasets directory inside backups

`$ cp *calibration.txt backup/calibration`   copying all calibration files

`$ cp 2015-11-* send_to_bob/all_november_files/`   copying just November files

`$ cp *-23-dataset* send_to_bob/all_datasets_created_on_23rd/`   just 23rd files


