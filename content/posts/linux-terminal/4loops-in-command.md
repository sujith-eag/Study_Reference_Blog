+++
isStarred = false
toc = true
tocOpen = true

date = '2024-10-20T19:20:16+05:30'
title = 'Terminal - 4 Loops & Scripting'
description = 'Making use of for loops to make scripts and repeatedly run a task'
+++

***Objectives***
Writing a loop that applies to one or more commands separately to each file in a set of files.
Trace the values taken by a loop variable during the execution of the loop.
Explain the difference between variable's name and its value.
Explain why spaces and some punctuation characters should't be used in the file name.
Demonstrate how to see what commands have recently been executed.
Run recently executed commands without retyping them.

## Loops 

Loops are programming constructs that allow us to repeat a command or set of commands for each item in a list.
```c
$ for filename is basilisk.dat minotaur.dat unicorn.dat
> do 
> 	echo $filename
> 	head -n 2 $filename | tail -n 1
> done
```
`for` indicates the start of for-loop
`do` indicates the start of job execution list
`done` indicates the end of a loop
`$` is used to indicate it as a variable that has to be replaced by its value


`echo` all 10 numbers using loop
```c
$ for number in 0 1 2 3 4 5 6 7 8 9
> do
> 	echo $number
> done
```

Wrong method
```c
$ for data in *.pdb
> do
> 	ls *.pdb
> done
# here all values are printed every time, not one at a time
```

Right way, prints each one of the values individually
```c
$ for data in *.pdb
> do
> 	ls $data
> done
```


Prints only cubane.pdb
```c
$ for filename in c*
> do
> 	ls $filename
> done
```


prints only cubane.pdb and octane.pdb
```c
$ for filename in *c*
> do
> 	ls $filename
> done
```


## Saving to a file in a loop

```c
$ for alkanes in *.pdb
> do
> 	echo $alkanes
> 	cat $alkanes >> alkanes.pdb
> done
```
prints all  `.pdb`  and appends all into `alkanes.pdb`
using `>` would have only one value in the file


## Piping

```c
$ for filename in *.dat
> do
> 	echo $filename
> 	head -n 100 $filename | tail -n 20
> done
```
echo all  `.dat`
assuming each file has at least 100 lines
take the first 100 lines and take the last 20 lines from that.
So gives lines from 81 to 100

what happens to the lines??


## Spaces in names

```c
$ for filename in "red dragon.dat" "purple unicorn.dat"
> do
> 	head -n 100 $filename | tail -n 20
> done
```
Enclosing the file with " " around the filename but it should not be around $filename.


## Copying a file into multiple files

```c
$ cp *.dat original-*.dat
``` 
To create a new file with original`-` as prefix.
But raises error as the last argument is not a directory and there are multiple files when   `*.dat`  is expanded


```c
$ for filename in *.dat
> do
> 	cp $filename original-$filename
> done
```
Now each of .dat file come one by one and in the cp there will be only two files so will be copied into the other.


## Scripting

```c
$ for datafile in NENE*A.txt NENE*B.txt; do bash goostat.sh $datafile stats-$datfile; done


$ for datafile in NENE*A.txt NENE*B.txt; do echo $datafile;
bash goostats.sh $datfile stats-$datfile; done
```

```c
$ for datafile in *.dat
> do
> 	echo "cat $datafile >> all.pdb"
> done
```
Without the " " , each entry would have cat cat


## Nested loop

```c
$ for species in cubane ethane methane
> do
> 	for temp in 25 30 37 40
> 	do
> 		mkdir $species-$temp
> 	done
> done
```
