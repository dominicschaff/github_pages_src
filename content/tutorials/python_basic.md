title: Basic Python
date: 2020-03-22

Awhile ago I was asked to give a quick course in Python to some colleagues. And I thought that maybe
it could be useful for others to also have access to. So here follows my attempt at showing one how
python works from the perspective of one that can already program.

## Things to Learn

So the things that are going to be shown in this short tutorial is going to cover the following:

* Basic syntax
* Using variables
* Basic variable types
* Reading from the command line
* Some math (Yay!!!)
* Lists
* Control Structures (ifs and loops)
* Reading the command line arguments
* List comprehension (short hand list manipulation)
* Dictionary comprehension (short hand dictionary manipulation)
* Built In Functions

## Start

The first thing you are going to need is a Python interpreter. For me I prefer Python 3, but almost
everything can be done in Python 2. If you are using `Linux` then Python 2 will be pre-installed,
and Python 3 might be installed. If you are on `Mac OS X`, then Python 2 is installed but Python 3 will need
to be installed separately. And on `Windows` you will need to install it yourself. Instructions on installing
can be found on <https://www.python.org>.

You will also need an editor. You can use any editor you feel comfortable in. I prefer using either [VIM](http://www.vim.org)
or [Sublime 3](https://www.sublimetext.com/3). And if you want a full editor then you can use [PyCharm](https://www.jetbrains.com/pycharm/).

## Basic Syntax

Python has many rules and most of them are similar to other languages like Java and PHP.

Some points that stand out:

* Lines do not need to be ended with a `;`
* Control structures do not use curly braces for blocks of code.
* Control structures do not need parentheses around their evaluation code.

## Variables

Variables in Python can be any set of alphanumeric characters and underscores. However there are some
things you need to look out for:

* Variables cannot start with a number.
* Variables are case sensitive.
* There are only special circumstances where underscores are used as the name of a variable.

## Variable Types

There are many types a variable can be in Python, the basic ones are:

* Integers e.g. `x = 123`
* Floating point numbers e.g. `y = 3.2`
* Strings e.g. `s = "num"`
* Objects
* Lists e.g. `l = [1, 2, 3]`
* Tuples e.g. `t = (1, 2, 3)`
* Dictionaries e.g. `d = {'a': 'b', 'b': 'c'}`
* Function references e.g. `q = len`

```python
x = 123
y = 3.2
s = "num"
l = [1, 2, 3]
t = (1, 2, 3)
d = {'a': 'b', 'b': 'c'}
q = len

print(x)
print(y)
print(s)
print(l)
print(t)
print(d)
print(q)
```

## Reading Input

Now that you know what variables look like and an example of how to print something to screen. Lets
make a simple script that will ask for your name, and then print a greeting and your name:

*Python3*:

```python
name = input('What is your name? ')
print("Hello", name)
```

*Python2*:

```python
name = raw_input('What is your name? ')
print("Hello", name)
```

## Math Operators

Python has the normal math operators that most languages has (`+`, `-`, `*`, `/`, `%`). However it also contains a power operator: `**`.

```python
print(1 + 9)
print(9 - 4)
print(7 * 9)
print(8 / 3) # normal division: 3/2 will be 1.5
print(5 // 2) # integer division 3/2 will be 1
print(8 % 3)
print(2 ** 3)
```

## Lists

In Python we have lists instead of arrays. They behave almost the same, with the main
difference being that lists can have operations on them to extend them, or get sub sections
of them.

When using lists one of the math operators gets over loaded. This being the `+` operator, which
when used with lists will extend them by the list provided.

An example of a list would be: `l = [1, 2, 'three']` as you can tell a list does not have to contain
the same types, unlike other languages. however it is much easier if you always keep your lists
containing the same type.

Lists are zero indexed and are accessed in a similar manor as other languages: `l[1] = 5` and can
be used directly.

**Some examples of using lists:**

```python
l1 = [1, 2, 3, 4, 5]
l2 = [6, 7, 8, 9, 10]
l3 = l1 + l2

for i in l3:
    print(i)

print(l1[3]) # will print 4

l3[2] = 99
print(l3)
```

When making a variable equal to a list, the list is not copied but referenced, so changes to the
original list will make the same changes to the new list. This can be avoided by copying the list.
Copying a list is a special version of splicing a list. To splice a list is to get part of the list
copied into a new list.

**Examples of list splicing:**

```python
l = [1, 2, 3, 4, 5, 6, 7, 8, 9]

l2 = l[2:4] # from the third element till the fifth (but excluding last element)

l3 = l[2:] # from the third element till the end

l4 = l[:] # copy of list
```

You can also make the list longer by appending items, and items can be removed by deleting them.
When an item is removed all the indices are re indexed.

```python
l = [1, 2, 3, 4, 5]
l.append(6) # append item to end
del l[2] # remove the third element.
```

## Dictionaries

A dictionary is something like a mix between a list and a hashmap. They are accessed by in a similar
way to lists except they have string indices. They offer the speed of a hashmap. And when printing out
their values the order can never be assured. The other difference is that dictionaries use curly braces
to initialise them, compared to lists which use square brackets. When adding to a dictionary an explicit
append is not used.

```python
d = {'apple': 'green', 'strawberry': 'red'}
d['grape'] = 'green'

del d['apple']
```

The other difference is that when you iterate over a list you get the values, where as for a dictionary
you iterate over the keys by default:

```python
d = {'apple': 'green', 'strawberry': 'red'}

for k in d:
    print(k, '=', d[k])
```

## Tuples

Tuples are special purpose lists. They are immutable, which means you cannot change the values they
store, you cannot make a tuple longer, and you cannot remove an item from a tuple. However if a tuple
stores objects, those objects may be changed, but which objects the tuple points to cannot be changed.

```python
t = (1, 2, 3)
print(t)

t2 = ([1], [2], [3])
t2[0].append(3)
print(t2)
```

Tuples are great for storing things that should not be changed, like colour codes.

## Control Structures

Python has a few main control structures:

* `if` - for making decisions
* `while` - for looping over an unknown amount
* `for` - for use with iterators

Examples:

```python
if 1 < 2:
    print("Yay")

if 1 < 2 and not 2 > 3:
    print("Again Yay")

if 1 < 0:
    print("Not good")
elif 2 > 3:
    print("Again not good")
else:
    print("Much better")

i = 1
while i < 3:
    print(i)
    i += 1

for x in range(10): # print from 0 to 9
    print(x)

for x in range(2, 11, 2): # print 2, 4, 6, 8, 10
    print x
```

You will notice there is no `switch` as there is in other languages. This is because `if`s and
`elif` (else if) should rather be used. There are a few others but they will not be covered in this
tutorial, as they are for special cases.

But if you are interested some are:

* `try` and `catch` for exception handling.
* `with` which is used for connections, for proper handling of opening and closing behaviour.

## Command Line Arguments

There is a way of getting values from the command line arguments, these are also much more useful
than getting values read in from using `input()`, this allows you to script the use of your program.

In the standard library `sys` (which provides system functions) is an array called `argv` which has
a list of all the arguments passed to python, including the name of the current program. The first
item in this list is the name of the program, the rest are all the values that were passed from the
command line.

```python
import sys

for v in sys.argv:
    print(v)
```

## List Comprehension

In previous sections you have seen that you can use `append` to add an item to the end of a list. But
if you are going to create a list from a fairly simple process then you can use list comprehension
to shorten the amount of code you type. Just as a warning this syntax can be tricky to read, and
even worse to debug. So if you are going to use this then make sure you know what you are doing.

The basic syntax of list comprehension is built from two mandatory sections and one optional section.
The first section is the value that you want, the second is the loop, and the third is some restriction.

This will calculate the first 10 square numbers:

```python
l = [x**2 for x in range(10)]
```

But if we want only the squares of even numbers then:

```python
l = [x**2 for x in range(10) if x % 2 == 0]
```

I know that the above could have been accomplished by just changing the `range(10)` to `range(0, 10, 2)`
but that was just for a simple use case.

You can also do a list comprehension inside a list comprehension (as many times as you wish), but with
every occurrence you need to be even more careful.

An example of producing a multiplication times table:

```python
l = [[x*y for x in range(10)] for y in range(10)]
```

## Dictionary Comprehension

Dictionary comprehension follows all the same rules as above, except the "value" part of the syntax.
Which is expressed as `key: value`.

I am going to use the exact same example as above:

```python
l = {x: x**2 for x in range(10)}
```

```python
l = {x: x**2 for x in range(10) if x % 2 == 0}
```

```python
l = {y: {x: x*y for x in range(10)} for y in range(10)}
```


## Built In Functions

There are quite a few built in functions that are available to be used. Some of them are listed here:

* `len` - get the length of the argument
* `max` - get the maximum value of the passed iterable
* `min` - get the minimum value of the passed iterable
* `sum` - get the sum of the passed iterable (needs to be numbers)
* `range` - creates an iterator of integers
* `print` - sends the argument list to the console
* `del` - remove the given item from memory

# Ending

If you absolutely cannot wait for the next tutorial, you also search the web, their are many very good
sites that give a much better description to this language than what I can ever do. I will try to find
some, and over time will add it to this tutorial page.
