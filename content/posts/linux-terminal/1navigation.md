+++
isStarred = false
toc = true
tocOpen = true

date = '2024-10-20T18:09:18+05:30'
title = 'Terminal - 1 Navigating in Directories'
description = 'about git and basic terminal commands for navigating the directories and files'
+++

## Bash

Bash - `Bourne Again SHell`    (git Bash - for windows interaction with git )

`Ctrl + Alt + T`    Launch terminal
`Ctrl + Shift + C`    for copying from terminal
`Ctrl + Shift + V`   for pasting in terminal
`clear`      to clear the terminal

The grammar of a shell allows to combine existing tools into powerful pipelines and handle large volumes of data automatically.
Sequence of commands written in a 'script', improves the reproduciblity of workflows.

## Terminal Basics 
#30aug24
`su`  -  super user
`sudo`  -   getting the super user permission
`apt `  -  the installer     
`sudo apt install update`   ` sudo apt upgrade`

`$`  is the prompt for typing, followed by a blinking text cursor
`$ whoami`     ` sujith`


`--help` can be passed to any command  to see what option a command accepts
`cd --help`           `ls --help`           `mkdir --help`  

`help cd`   `help echo`  works
	(if there are long `--` and short `-` versions of a command, use short when typing command in the terminal, use long in scripts when it is written once and read many times)

`man` is manual for a command if it exists 
`man ls`       `man mkdir`         

`space` and `B` used to travel in manual,  
`/` is used to search for a term,  
	`N` is used to move between the hits, `N+Shift` for moving backwards

`man cd` doesn't exist as it is a built is function `--help` can be used


## General Syntax of a Shell command

`$ ls -F /`   Listing of files & directories in Root directory /
	$ is the prompt
	ls is the command
	-F is the option/flag/switches
	/ is the argument

'Command' doesn't always require argument or option
'Command' can be called with more than one 'options' & 'arguments'
	( 'options' and 'arguments' are referred to as 'parameters')

'Options' change the behavior of a 'command' 
'short options' start with single dash ' - ',   `-r`   `-a`
'long options' start with double dash '--'   `--reverse`    `--all`

'Arguments' tell the command what to operate on (files and directories)

> Each parts are separated by spaces, if space is omitted, the difference between command, option and argument will not be known to the terminal.  
    (  `ls-F`   searches for a command called `ls-F`  which doesn't exist)

Capital and Small are also important
`ls -s`   displays size of listed files
`ls -S`  sorts the displayed files


____________

## Navigating Files and Directories

`Directory names in a path are separated by / in unix, \ in windows`


### Tab completion

When there is only one option, like Document or Download, hitting tab on D will show both Document/ Download. (Double tab will show if there are more than one)
Doc + Tab will bring **Documents**

`~/Documents/Odin-Project/foundations/java-script/calculator/`
Doc tab      O tab     f tab     j tab    cal  tab

*  `.`  for opening everything in a project directory
*  `git add .`  to add all files in a directory to Git staging area
* In VS code, opening `cd` in project directory and typing   `code .`    opens project folder
* `code` in terminal launches VS code


### `pwd` Print Working Directory   

`pwd`  print working directory, shows current working directory(shows where we are)
[[pwd  - print working dir]]
`/` indicates the root directory,  `/Users/sujith`  it is the slash before the user     


### Relative and Absolute Paths

When '***Relative paths***' are used with commands `ls` and `cd`, it tries to find that location 'from where we are' rather than from the root of the file system. so it can only look at files within that directory and the `..` parent directory 

***Absolute paths*** can be specified by including its entire entire path from the root directory indicated by a leading slash  `/`
This tells the computer to follow the path from the root of file system so it always refers to one directory.

(Using `pwd` to see the route and typing the absolute path to wherever we want to go)
`~`  tilde character at the start of a path mean **the current users home directory**  
	( `~/data`  is equal to   `/Users/sujith/data`     useful for absolute path typing)
	

### `cd` Change directory

`cd  <name>`    Change directory(changes the shells current working directory)  
	(can only move into directories like this, but not out of it with relative paths)

`cd ~`    going to the home directory at once ( `home/sujith`)

`cd ..`   moves back to parent directory 
	( `..` is a special directory meaning "the directory containing this one" i.e parent directory)
	(`.` by itself means current directory)

`cd -`   the `-` in front moves to the previous directory we were in , 
`cd -`   again will bring us back ( it is switching between current and previous directories only )
	
( `cd /`  goes to root directory,  `cd ~` goes to home directory  )
( `cd ../..`  goes up by two level, parent of parent)


### `ls` Listing

`ls`         listing to check files and directories in the directory
all these options/flags can be combined like ls -Fal  -lF  -aF

flags for `ls`
  `-l`  crates a list of things 
  `-h`  does something i couldn't figure
  `-a`  'show all' shows hidden directories with `.` also `..` directory
( there will be other directories which start with `.` like `.bash_profile` these contain shell config settings, these are hidden to prevent cluttering )

  `-F`  gives an output separated with `/` marker to show what they are, (ones with no marker are files)

`ls -R` to list all nested sub directories within a directories


#### Looking at other directories contents without moving out 

`ls ~/Desktop/trial`
`ls /User/sujith/Desktop/trial`
`ls -F Desktop` 
