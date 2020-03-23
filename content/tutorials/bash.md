title: Bash Usage
date: 2020-03-22
modified: 2020-03-23

> **Note:** I am building this page over time, so content will appear here slightly haphazzardly.
> So if there is content missing, I will add it later.

So you have heard of the terminal environment, and maybe have even typed some commands in it. Now wouldn't you like to learn how add some more programming type logic to it? or perhaps even save these commands for later use? In this basic tutorial I hope to convey some of this knowledge to the reader. I will also try to keep this page updated when I see new tricks that are wonderful to use.

## Things To Be Covered

If you know some of these things then skip to what you want to know.

* Basics
* Quick Notes on Syntax
* Printing
* echo
* printf
* Variables
* Basic Math
* Printing with Variables
* Reading in from the user
* Process Substitution
* Control Structures
* Globing
* Piping
* Input/Output Redirection
* Exit Codes
* Functions
* Arrays
* Shorthand Filtering

## Start

First you are going to need two things, a text editor and a terminal. For each OS there are multiple terminal apps you can use. I only know of a few having only used a few OSs but there are many that you can use. For `OS X` (or `macOS`) there is the built in `Terminal.app` and some people prefer [`iTerm2`](https://www.iterm2.com). If you have an `Ubuntu` based distrobution of Linux then there is the `Terminal` (sometimes called by different names). And in the latest versions of `Windows 10` there is also a bash shell.

And secondly you should get some form of text editor, my preference when writing bash scripts is `Vim` however [Sublime 3](https://www.sublimetext.com/3) is also very good.

## Basics

First and foremost: **be careful what you do in a bash script, bash is very powerful and can do much harm if you make a mistake**. I have made many mistakes while learning, most of them were very easily corrected but not all mistakes are easy to correct.

Now for some things to keep in mind:

* Anything that can be run in your terminal can be put into a script file.
* Your script will run in a different instance to your shell, most of the time.
* Arguments can be passed to your script, and a result can be returned, but variables are usually kept in context of the script or your shell session, there are exceptions to this which I will cover later.

The syntax I will show will look as follows.

When I am using the shell the output will be shown as such:

```bash
$ ls -l
total 4.0K
-rw-r--r-- 1 c0de 1.9K Aug  8 18:23 style.css
$
```

> Remember though that you should not be typing the `$` at the beginning of the line.

However a file will be shown as:

```bash
# filename.sh
ls -l
```

and then the output shown as:

```bash
$ bash filename.sh
total 4.0K
-rw-r--r-- 1 c0de 1.9K Aug  8 18:23 style.css
$
```

> Notice that whenever I use the shell I will always end my output on another `$` symbol to show where the next input starts.

## Quick Notes on Syntax

There are some things you need to be aware of with Bash:

* Bash is **NOT** forgiving when spaces are incorrect. Having one to few or to much will create a syntax error.
* Syntax needs to be exact, otherwise either your script will break, or you will get weird results.
* A comment starts with a `#` and ends when the line ends. There are no multi-line comments.

Bash scripts should always start with one of the following:

* `#!/bin/bash` - most common
* `#!/usr/bin/bash` - an alternative to the above
* `#!bash` - least common
* `#!env bash` - most widely supported (apparently)

If you are unsure which to use then use the first one (`#!/bin/bash`).

## Printing

The basics of printing can be done in one of two ways, using the `echo` command or using the `printf` command. Most of the time you will see the `echo` command being used, and very very rarely the `printf` command is used.

### echo

`echo` is a basic command with some nifty extra first you can echo plain text:

```bash
$ echo "Hello"
Hello
$
```

However is does have some noteworthy options that can be used: `-n` which removes the automatically inserted line ending and `-e` which allows for special symbols to be added.

```bash
$ echo -n "Notice the last character"
Notice the last character$
```

> The previous example was to show that no new line was added by default. Hence the `$` at the end of the line

```bash
$ echo -e "Adding\nNew lines\nIn My text"
Adding
New lines
In My text
$
```

### printf

Using the `printf` function however allows for formatted printing. The formatting works in the same way as in most languages where you have the following meanings:

* `%f` - for floating point number
* `%d` - for an integer
* `%s` - for a string

But the ones that will be seen the most will be:

* `%10s` - ensure a column of 10 characters, adding spaces to the string as needed
* `%03d` - ensure a 3 digit number prepended with zeros to fill the gap.

Notice however that `printf` does not automatically add a new line for you. So you are going to need to that manually by adding `\n` to the end of your format string.

Examples are:

```bash
$ printf "%03d\n" 2
002
$ printf "+%10s - %d\n" "Test" 2
+      Test - 2
$
```

## Variables

Bash allows for variables which you can save one of 3 types of data. Numbers, string and array. Arrays however will be covered in a section on it's own much later.

> There are some things you need to be aware of when using variables in Bash:
>
> * When assigning values there must be no space around the assignment operator: `a="qwerty"` is correct but `a ="qwerty"` and `a= "qwerty"` will  result in syntax errors.
> * When using variables, they need to be prepended with a `$` most of the time (you will see later when not to use them).
> * Variables are blank when they have not been assigned yet so `echo "$a"` will print a blank line if `$a` has not been created yet.

Assigning and using variables:

```bash
$ a=99
$ b="some text"
$ c="$a$b" # will concatenate the two variables
$ echo "$c"
99some text
$
```

## Basic Math

Now as most languages have some way to do basic math operations so does Bash. However note that the math that Bash can do is very limited so use with care:

```bash
$ a=8
$ echo "$((a+1))"
9
$ echo "$((a-1))"
7
$ echo "$((a*2))"
16
$ echo "$((a/2))"
4
$ echo "$((a%2))"
0
$
```

> Notice that this is one of those times when there is no `$` with the usage of a variable.

And to reassign the value back to the orriginal variable we can just use the assignment operator again:

```bash
$ a=2
$ a=$((a+2))
```

## Printing with Variables

Now that we can use variables and save simple data into them we would probably need to be able to print out that data again.

There was an axample further up where we did print out the values.

```bash
$ s="Some String"
$ a=3
$ echo $s
Some String
$ echo $a
3
$ echo "then the string is '$s' and the number is '$a'"
then the string is 'Some String' and the number is '3'
$
```

## Reading in from the user

There are many times that instructions will be needed from the user in terms of input from the user. There are two ways of doing this. Either you use arguments into your file, or you request information from the user in your script. (The first way is preferred.)

### Command Line Argument

A command line argument is what you would add after the name of the program. An example to this is the `-l` argument one can add to the `ls` program. Arguments usually change the way the program or script operates. As for example passing `-l` to `ls` will cause the output to show a list of files instead of your files in one line.

An example of passing arguments into a bash program would look like one of these three ways (depending on how you run your script).

```bash
$ bash myscript.sh argument1 argument2
$ ./myscript.sh argument1 argument2
$ myscript.sh argument1 argument2
```

The first way explicitly calls the program `bash` to run your script. The second way uses that first line in your script (`#!/bin/bash`) to figure out what program to call your script with. And the third way only works if your script is in the executable path, which in our case will not be the case.

Now that we can give arguments to our scripts, our scripts will need a way of reading them out again.

There are some special variables that are used in this case.

* `$#` has the count of variables that are in the list of arguments.
* `$0` contains the name of the script being run.
* `$1` to `$9` has the first nine arguments to your program.
* `${10}` and onwards contains the rest, you can also use `${1}` to get the arguments at the places below 10, but it looks ugly to it this way.

So to use this in a simple example:

```bash
# myscript.sh
echo "Count of arguments provided: $#"
echo "This script name: $0"
echo "The first argument: $1"
echo "The second argument: $2"
```

```bash
$ bash myscript.sh fluffy bunny
Count of arguments provided: 2
This script name: myscript.sh
The first argument: fluffy
The second argument: bunny
$ bash myscript.sh fluffy
Count of arguments provided: 1
This script name: myscript.sh
The first argument: fluffy
The second argument:
$ bash myscript.sh
Count of arguments provided: 0
This script name: myscript.sh
The first argument:
The second argument:
$
```

> Notice that in the second and third run some of the lines didn't print anything (nothing was given) but the script also gave no error.

### Reading User Input

Now the other way is request for information from the user when needed. This is very good for information that you do not want the user to store in their terminal history, and there is even a special command to read passwords so that they do not display on the screen while the user is typing it.

The command we are going to use is `read` note that there are some special arguments that you can give it

* `-s` this is for when you want the text to be hidden while you type.
* `-p "<other text>"` this will allow you to prompt the user for something.
* `-N <number>` this is great for when you only want a certain amount of text read in. Very useful for yes/no questions.
* And anything given without a `-` infront will be treated as if that is the variable to read into.

> If no variable is given then the variable that the data is read into is `$REPLY`

```bash
$ read
hi
$ echo "$REPLY"
hi
$ read -s
$ echo "$REPLY"
password
$ read -p "Answer this question: "
Answer this question: sure
$ echo "$REPLY"
sure
$ read -N 1 -p "Yes or No: "
Ye^C
$ read -N 1 -p "Yes or No: "
Yes or No: Y$ #Notice I pressed enter here after typing which gave the weird printing
$ echo "$REPLY"
Y
$ read answer
hello
$ echo "$answer"
hello
$
```

## Process Substitution

This is a way of running a program and using the input or output to look like a file to another program.

As an example you can compare the output of two instructions.

```bash
diff <(date) <(sleep 2; date)
```

The `<()` syntax makes a file for the `diff` program but allows you to take the output of the program and use it like a file for `diff` without creating
an actual file first.

## Control Structures

As in other languages there are control structures in bash. The 3 main ones are `if`, `while` and `for`. And they work in similiar ways to other languages.

### if

An `if` is used to make decisions as it is used in other languages, the simplest if would be as follows:

```bash
# test_if.bash
if [[ 1 < 3 ]]; then
  echo "Yay"
fi
```

> Remember spacing is very important here!!!

And there is also the `else` keyword as in other languages:

```bash
# test_if_else.bash
if [[ 1 > 3 ]];then
  echo "damn"
else
  echo "Yay"
fi
```

And there is also an else if, however the keyword to use would be `elif`:

```bash
# test_if_elseif.bash
if [[ 1 > 3 ]]; then
  echo "No"
elif [[ 2 > 1 ]]; then
  echo "Yay"
fi
```

### while

The `while` statement follows the following syntax:

```bash
# test_while.bash
while read a; do
  echo "$a"
done
```

> Replacing the `read a` with whatever command you would like to be as the test condition.

The `while` statement can use either the exit code of a command as above or a test condition as in the example with the `if` above. However most of the time that I use the `while` statement I am normally reading in input as in above.

### for

The `for` statement follows the following syntax:

```bash
# test_for.bash
for f in *.mp3; do
  echo "$f"
done
```

The `for` statement requires a variable (the `f`) and something to loop over (the `*.mp3`). Most of the time that I use a for loop I use one of the following examples:

```bash
# test_for_examples.bash

# print all the numbers from 1 to 10:
for i in {1..10}; do
  echo "$i"
done

# print all the odd numbers between 1 and 10:
for i in {1..10..2}; do
  echo "$i"
done

# print out the names of all the mp3 files in the current directory:
for f in *.mp3; do
  echo "$f"
done

# or print out all the parts of a command (the output is split by space):
for p in `date`; do
  print "$p"
done
```

## Comparisons

The comparisons one can make depends on the data type that is used in the comparison. Bash supports using either numeric types or strings:

### Numeric

Numerical types use the same symbols as most languages: `<`, `>`, `==`, `<=`, `>=` and `!=`.

### Strings

Strings on the other hand cannot use the above symboles, instead they use the following:

* `-eq` - to test for equality.
* `-ne` - to test for non equality.
* `-gt` - to test for greater than.
* `-lt` - to test for less than.
* `-ge` - To test for greater and equality.
* `-le` - to test for less than and equality.

## Globing

In essence globing is the reverse of a regular expression. In that the expression that you do give it, the outcome is every possible match to what you provided.

As an example look at the following:

```bash
$ echo {1..20}
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
$ echo {a,d,c,e,f}{1-3}
a1 a2 a3 d1 d2 d3 c1 c2 c3 e1 e2 e3 f1 f2 f3
$ echo server-{1,2}{a,b}-cpt
server-1a-cpt server-1b-cpt server-2a-cpt server-2b-cpt
$ echo {a..c}
a b c
$ echo {1..10..2}
1 3 5 7 9
$ ls
file1 file2 file4a another_file
$ echo file*
file1 file2 file4a
```

Now you might wander why would anyone use this. Let me give you a few examples:

1. Let's say you are wanting to process all the text files in a folder you could then run: `for f in *.txt; do cat "$f"; done` obviously replacing the `cat` program with what ever you need.
2. Perhaps you have a list of servers that are identified by numbers, and you want to get the last 20 lines of the `httpd` logs: `for s in server{1..10}.internal; do ssh "$s" 'tail -n 20 /var/log/httpd.log'; done`
3. What about deleting all your backups? `rm *.bkp *~`
4. Or perhaps clearing or temporary text files on your machine? `rm /tmp/*.txt`

As you can see there can be many uses for this, the limit is only what you need to do, or what you can find.

## Piping

One of the major benefits that Unix brought was the idea that all programs shoould be able to handle text streams as their input and output. Now obviously not all programs handle (think of `ls` that only outputs). But most programs can do both. This might seem unimportant, were it not for another of the Unix philosophies which is that a program should only do one thing well, so that other programs can be delegated to do the other tasks.

For example let's only use the basic form of `ls` to output a list of files and directories. Now let's take what ever we get and reverse it: `ls | sort -r` this obviously can be done with just `ls` however that would give `ls` way to much responsibility, but becareful with that thinking, sometimes it is beneficial to allow one program to do a lot more than one thing (read the `man` pages for `ls` to see why).

There are great benefits to piping in a Unix environment one of the great benefits is that each time a new pipe is started it also signifies that a new process should be forked on the machine. Which means that if you have multiple linear processes that output data slowly, the next parts of the processes can start running even while the others are still going. And this can allow some jobs to be faster, however most of the time this will not be notice able.

In most Unix environments you can pipe for as long as you wish so a command such as:

```bash
$ cmd1 | cmd2 | cmd3 | cmd4 | cmd5 | cmd6
```

Can stretch on to cover many lines, even though this does make things a little more difficult to read.

Note also that if for example `cmd3` breaks the rest of the chain will behave most of the time as if nothing it wrong.

## Input/Output Redirection

Bash provides one of the marvoulous things that it can read and write from files without using programs like `cat`, it can do what is known as redirection. Where it can take the contents of a file as use it as input for a program. Or automatically save the output of a program into a file.

As an example instead of `cat file.txt | wc -l` we could write `wc -l < file.txt` (These are very simple cases, but the idea does work).

Or perhaps you want to save the output of a command into a file for later usage: `curl http://google.com > file.html`.

Both of these can be used at the same time as well: `wc -l < file.txt > results.txt`

There are a few other types of redirection as well, they are listed below:

* `cmd > file.txt` - save the output of `cmd` to the file `file.txt`
* `cmd >> file.txt` - append the output of `cmd` to the file `file.txt`
* `cmd !> file.txt` - save the output of `cmd` to the file `file.txt` but only if it doesn't already exist
* `cmd < file.txt` - use the contents of `file.txt` as the input of `cmd`
* `cmd 2> error.txt` - save the error stream of `cmd` to the file `error.txt`
* `cmd 2>&1` - output the error stream to the standard output stream
* `cmd &> file.txt` - save both the error and standard output stream of `cmd` to `file.txt`

## Exit Codes

Every program once run will produce an exit code, which will let you know whether it exited successfully or with an error. **Note** however that there are some programs that will exit with an error but produce a successful exit code.

## Functions

As with other languages repeating code all the time can be tiring, so sometimes you would like to group functionality together. In Bash you can either do that with scripts, or with functions.

The basic definition of a function would be:

```bash
function_name()
{
  echo "Hello..."
}
```

You can then run any subset of commands in your functions. When inside a function is looks like you are in a seperate script so you can access the function arguments the same way that you access a scripts arguments (refer to <#command_line_arguments>).

For an example see:

```bash
func()
{
  echo "$1"
}
func 'Hello'
```

Functions can be defined in your `.bashrc` file to be used in your shell environment, or in files to be used in your scripts.

## Arrays

Arrays can be created in a few ways. The two most common ways are:

```bash
#Hardcoded:

arr=(
  item1
  item2
  item3
)

#Based on the output of a program
arr2=( $(ls -1) )
```

Then you can do various things with the arrays.

```bash
for a in ${arr[*]}; do
  echo "$a"
done

echo "Array values: ${arr2[@]}"

echo "Array size: ${#arr2[@]}"
```

## Script Snippets

Here I will add short snippets that I have found useful in the past.
