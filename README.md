# An introduction to the command line for linux machines

The majority of bioinformatic software is written to be run using a Unix OS. Many are run from the command line interface (CLI) instead of using a graphical user interface (GUI) that you will be more familiar with. Understanding how to navigate the CLI is the first step to being comfortable with using CLI bioinformatic tools. Ultimately this allows you to have more control over working with large data, e.g. to view/edit/wrangle/filter, compared to using applications such as Microsoft Excel. In this tutorial we will go over some basic command line arguments that can be used to navigate the linux filesystem.

## Table of Contents
1. [Basic commands to navigate a linux file system](https://github.com/SianGol/intro-to-command-line/blob/main/README.md#copying-and-moving-files-to-locations-elsewhere-in-the-filesystem)
2. [Creating txt files](https://github.com/SianGol/intro-to-command-line/blob/main/README.md#creating-text-files)
3. [Piping commands together](https://github.com/SianGol/intro-to-command-line/blob/main/README.md#copying-and-moving-files-to-locations-elsewhere-in-the-filesystem)


## Basic commands to navigate a linux filesystem

To access the command line we are going to use the application called Terminal. When you open this app you will see one line of text which is known as your prompt, followed by a flashing cursor. This is where the commands you type will show up. 

The first command we will use is 'pwd', which stands for 'print work directory'. This shows you where your current work directory is, i.e. where you are located within the filesystem. After each complete command you need to press the enter/return key to execute the command.

```bash
pwd
```
The output will show an absolute filepath. An absolute filepath begins with a '/' followed by the location of your work directory. As this is your default location for when you open the Terminal, this is also known as your 'home directory' (this is not necessarily the same as '/home'). Your home directory is a user specific folder within a multi-user machine, where all of your documents, downloads, music, and pictures will be stored. 

To see what folders and files exist in your work directory the next command we'll use is 'ls', which stands for 'list'. Many bash commands are named intuitively to achieve one simple task. We can add 'flags' to bash commands, for example try 'ls -l' and see how to output changes.

```bash
ls
ls -l
```
This prints the output in list format and includes additional information about your folders and files such as the permissions, file size, and the date and time it was made. Depending on what is stored in your work directory you'll see that directories (folders) are different colours to files. This makes it easier to identify the contents of a directory.

The next command we'll use is mkdir. This stands for 'make directory' and is used to create a new directory. Unlike the previous two commands we need to provide the name of the new directory as an argument to this command. In the example below we'll create a new directory called genomics, feel free to call yours whatever you like. You can then use 'ls' to check that the new directory was made.

```bash
mkdir genomics
ls
```
Let's move into this new directory. We can use the command 'cd' to 'change directory'. Like 'mkdir' we need to provide an argument to this command, i.e. the destination you want to move in to. You can check that you've moved into the directory using 'pwd'.

```bash
cd genomics
pwd
```
Your new work directory should now have '/genomics', or equivelent, appended to the end of it. The previous work directory is now referred to as the parent directory. To help make navigating the command line easier and prevent you from typing out the entire file path there are shortcuts you can use.

root directory '/'
home directory '~'
work directory '.'
parent directory '..'

Try the following:

```bash
cd ~
pwd
```
You should see that you've moved into your home directory. If you were to use cd with no filepath/shortcut argument you are also taken back to your home directory by default. Try it!

Let's use the '..' shortcut to move into a parent directory. In this example the parent directory is also your home directory.

```bash
cd genomics/
pwd
cd ..
pwd
```
When navigating the command line it's important to remember the difference between absolute paths, which start from the root directory '/', or relative paths, which start from your work directory './'.

## Creating text files

In this example we're going to use 'nano', a simple text editor, to create a .txt file. This app could also be used to create bash shell (.sh) scripts, however, if you are going to be writing larger scripts in the future it would be better to use an alternative editor, such as VS code.

Navigate into your genomics directory, if you created this folder in your home directory then the below code will work.

``` bash
cd ~/genomics
```
To create a text file we need to use 'nano' command followed by the name of the file you are creating. For example let's say we want to create a .txt file called test.txt.

```bash
nano test.txt
```
You'll see a blank screen corresponding to the inside of your test.txt file. Type a phrase or a sentence and then press the 'control' and 'X' keys at the same time to exit your file. You'll be prompted to save it, press 'y' and then the enter/return key.

Let's now view the contents of your file. We can do this using the 'cat' function which stands for concatenate. The cat function is incredibly useful as it allows you to view the contents of a file, merge the contents of two or more files, and can also be used to create new files. The 'cat' command can have one or multiple arguments. 

```bash
cat test.txt
```
In the above example we've provided 'cat' with one argument, in this case your test.txt file. Therefore 'cat' prints the output of you file to the 'standard output' (stdout) i.e. the command line, the default location that linux commands often prints to. What about if we provide it two files as input? Create a new file containing a different phrase or sentence and let's test it!

```bash
nano test2.txt
```
```bash
cat test.txt test2.txt 
```
You'll see the output is the contents of the first file followed by the contents of the second file. Now instead of printing to stdout, lets direct the output into a specific output file. To do this we use the '>' charater.

```bash
cat test.txt test2.txt > merged.txt
cat merged.txt
```
As you can see merged.txt now contains the contents of both files. This can be done for two or more files, so is an incredibly useful command.

An alternative command to view your files is 'less'. This is interactive and opens your file, allowing you to scroll through it. To exit press 'q'. This is especially useful for large files that would otherwise print a very large output if you were to use 'cat'.

```bash
less test.txt
```

## Copying and moving files to locations elsewhere in the filesystem

To move or copy files using linux commands we can use 'mv' or 'cp' respectively. The 'mv' command moves your file from one location to another, whereas the 'cp' command creates a copy in the location you specify.

What do you think the below command does, try it!

```bash
mv merged.txt ..
```
Here we have used the 'mv' command followed by the file we want to move, in addition to the destination we will move it to. Notice that we used the '..' shortcut to direct it into the parent directory, therefore, we used a relative path as the destination argument.

Alternatively we can create a new copy of a file in the parent directory.

``` bash
cp test.txt ..
ls -l
ls -l ..
```
You'll see that test.txt now exists in both your work directory and the parent directory. Notice that we can use relative paths ('..') with the 'ls' argument also!

## Piping together commands

Each basic linux command tends to perform one function to keep commands simple and easy to utilise.  However, you can merge multiple commands by using '|', also known as piping commands together. To practice piping together commands lets create a file, named cities.txt, that contains an unsorted list of cities with duplicates. Often data is not perfect, so learning to wrangle using basic commands can be really useful! 

Structure your file so that each word appears on a new line, input below:

London
Singapore
Paris
Doha
Bangkok
Singapore
Tokyo
London
Paris

Let's start by sorting the list, using the command 'sort'.

```bash
sort cities.txt
```
The sorted cities are printed to stdout and are ordered alphabetically. However there are duplicates, so lets remove these using the 'uniq' command.

```bash
sort cities.txt | uniq
```
This produces a sorted list with only unique entries. What if we want to count the number of unique entries in our file? Here we can use 'wc' command, which stands for 'word count'. 

```bash
sort cities.txt | uniq | wc
```
This command prints three values to stdout; the number of lines, number of words, and number of letters in your file. To print out only one of these values you can use flags; -l (lines), -w (words), letters (-m).

```bash
# count the number of unique entries in cities.txt
sort cities.txt | uniq | wc -l
```
Finally, lets direct this output to a destination file. When creating files in linux it's important to not create filenames with spaces in their name.

```bash
sort cities.txt | uniq | wc -l > cities_sorted.txt
```



Note that you can't use your mouse to move the cursor to positions within your text, as you would in a MS word document. Instead you use arrow keys, or alternatively there are shortcuts which we'll go over later.









