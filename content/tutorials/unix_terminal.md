title: Basic Unix Terminal Usage
date: 2020-03-22

This is going to be a tutorial on usage of a Linux/Unix based terminal. If you want a more in depth overview of Bash
on the hand you may find [this]({filename}/tutorials/bash.md) useful.

The topics that are going to be covered are as follows:

* Moving around the system
* Basic commands
* Searching
* Editing
* Tunneling (SSH)

## Moving around the system

The most common thing you are going to need to do is move around the system and see where you are.

Commands that are going to be used here are (not including variations):

* `cd`
* `ls`
* `pwd`
* `cd ~`
* `cd ..`

The first thing you will see when opening a terminal will be something along the lines of:

```bash
merlin@machine ~ $
```

That line tells us 4 things:

1. `merlin` is your username
2. `machine` is your hostname
3. `~` is your current location (`~` means home directory)
4. `$` is your current access rights (`$` is normal, `#` is sudo)

From here there are many things we can do, some of which are seeing what is in this directory (`ls`), or going to a different directory (`cd`), or we could run a program.

Examples of each of those commands:

* `cd Music` - will switch to the "Music" directory
* `ls` - will list all the files and directories (that are not hidden)
* `ls -l` - will produce the above items in a list with more information.

There are some very useful arguments that can be passed into `ls`, a short list of them are:

* `-a` - show all files, including hidden files.
* `-l` - show detailed list
* `-1` - show in a list
* `-h` - show sizes in "human" readable format
* `--help` - will show all the available arguments

If you want to move up a directory then the special file `..` is available, which can be used like: `cd ..` or perhaps `cd ../Pictures`

You can always move around the system like that usually you know exactly where you want to go then you can go straight there like `cd Code/projects/site/src` or if the location is not in your current directory but you know the location from the root (`/`) of the drive then you can use `cd /usr/bin` to get there directly.

If you are ever lost then you can always use `pwd` to see where you are from the root or your home directory, depending on where you are.

And if you need to go to your home directory in a hurry then either of `cd ~` or `cd` will take you directly to your home directory.

## Basic commands

Now that we can see what files are where we would like to see some information regarding the files. There are many things you might want to know about a file. For example the size of a file, or the type of file it is. And quite often the contents of the file.

The various commands and an example of their usage would be:

* `file test.mp3` to see the type of file it is
* `file -I test.mp3` to print the mimetype
* `ls -lh test.mp3` to print the size of the file and other properties
* `wc test.txt` to check how many lines/words/characters are in a file
* `cat test.txt` to print the contents to the screen

## Searching

There are many times that searching for files is needed. This is going to be split into two sections. Searching by file/directory name and searching based on content.

### File/Folder name

The command to use for searching on file names is `find` the basic use would be the following:

```bash
find . -iname "*.txt"
```

That will find all filenames that match the expression "*.txt" but ignoring the case of the text. With this command you can also find directory names. To use that then fo look for the other arguments in the help or man pages.

My personal favourite way of finding files is by piping output of `find` into `grep`

An example of piping `find` into `grep` would be:

```bash
find . | grep 'file_name'
```

### File content

The command to search for the content of files would be `grep` and it's alternatives. Grep has many powerful features that can be used and many ways of searching in the content.

```bash
grep 'content' file.txt
```

Or to search in a directory (example uses current directory).

```bash
grep -r 'content' .
```

There are many useful arguments that can be passed to grep to make things easier. The commonly used is the `-i` parameter which makes searching case-insensitive.

For more help on what `grep` can do refer to either the help or the man pages.

## File Editing

There are many ways to edit files, I will only show the usage of `vim` here.

To open `vim` with a file(new or existing) run: `vim file.txt`

The first thing to know is how to quit (so you do not get stuck!). In the editor press <kbd>Esc</kbd> then type either <kbd>:q</kbd> or if you have made changes and want to revert them type <kbd>:q!</kbd>.

Vim offers a great amount of functionality, most of which is either hidden of disabled by default.

The basics of which is that Vim works in "modes", the default one that the program starts in is called "Normal" or a read-only mode. To get into "Insert" mode so that you can make changes is to press <kbd>i</kbd>. The other modes you are going to need to go read up in the documentation. But an easy way to get to know vim is to follow the tutorial that comes with Vim by running <kbd>vimtututor</kbd>.

## Tunnelling

There are going to be many times in which you need to work on a remote server. The most common way and the way you are going to be using is to use `ssh`. This is a great and powerful tool to use. The amount of things that it can do for you is great, however I am only going to show two usecases.

The most basic usecase is to login into a remote machine. To do this you need an account on that machine, and then either a password or a key file. I am going to assume you have a password:

```bash
ssh username@remote.address
```

You will then be prompted for a password, and if you type it in correctly you will be logged into that server. You can also leave off the `username@` piece if either your local username is the same as on the remote machine, or if you change your ssh config to automatically change your username.

The other thing that is useful to do on with `ssh` is to run a command on the remote machine and get the output locally:

```bash
ssh username@remote.address 'uname -a'
```

That will print out the machine details of the remote machine.

## Getting Help

There are many ways to get help on a command. The easiest of which is to google, but then you have to wade through the answers. If it is something specific I would rather use either the help argument to a program or go read the man pages. There is quite a lot of information that one can find in both those sources, so I would highly suggest you go and read them.

To ge the help from a specific program the most common way to do this is use either `-h` or `--help` or in some cases `-help` as an argument to the program, and the help docs will print to screen. These help pages are usually minimal.

To get much more complete help about a program you should refer to the man pages related to the command that you want to use. for example the man pages for the `date` command can be found by running `man date`

If you are unsure of what the command is exactly but remember part of it then the program `apropos` is very useful. It will search all the program files for the command you requested and print a one-liner message on what the command does. An example of this is to run `apropos date` which will print every command that has "date" in it.

