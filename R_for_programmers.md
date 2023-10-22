---
author:Nicolas Trutmann
---

# R for programmers

## Intro

This text was designed for people who know how to program and want the basic syntax of R succinctly described with as little faffing about as possible.
This text is **not** complete. Read a different manual for a more thorough treatment of the matter.

The text is structured as follows:

+ language
+ data structures
+ functions

Language refers to basic language notions such as flow control and looping. Data structures includes built-ins and how to define your own.
functions shows how to define functions sensibly, including OO-style (S3 specificly).

## Misc

To get started here is how to get help:

Your first line of defence is R's help function. These can be accesed at the command line by typing:

`?topic` or `?'topic'` or `??'topic'`

for example `?vector` will bring up the documentation page for the vector function. This is an indispensable tool when working with R as it allows you to check the correct syntax, the permitted arguments and the expected behaviour on the fly. Read the documentation page `?'?'` for help with help.

you should write documentation. see e.g. roxygen or official guideline TODO:link

A number of IDE options are available to make developing in R quick and painless. A GUI-based IDE is RStudio; for vim there is the Nvim plugin; emacs has the ESS plugin.

## Language

### key words

One of the most common points of contention is R's assignment operator.

`A <- 10`

as opposed to the usual '=' symbol. Give it a week and you'll have forgotten that it ever was an issue.

### flow control

Nearly identical to C syntax. The usual suspects are as one would expect:

    if (condition) {code}
    if (condition) {code} else {code}
    while (condition) {code}
    for (i in sequence) {code block}
    break
    next

The only big difference here is the 'sequence' in 'for'. This implies a vector data structure over which R will loop

## data structures

R has several data types:

+ logical `TRUE, FALSE, NA`
+ integer `5`
+ numeric (synonym double) `2.71828`
+ complex
+ character
+ raw (intended to hold raw bytes)

'R-base' ships with built in data structures, that suit it's intention for statistics. These are in order of dimension:

+ vectors
+ matrices
+ dataframes
+ arrays
+ lists

Vectors, matrices and arrays are 1,2 and 3 dimensional arrays of a given type. These 3 are in concept all vectors, with the distinction that matrices and arrays have a dimension attribute, that is used to deal with TODO: go on here

TODO: diff matrix and df
TODO: arithmetic and looping
TODO:

## functions

R is _very_ flexible when it comes to defining functions and it is highly recommended that the reader look into function definitions for a good while.


## basics

A standard function definition might look something like this:

    myFunc <- function(arg1, arg2) {
        code
        last line
    }

- setting defaults
- passing on arguments

A more involved function example might look like this:

    myFunc2 <- function(x, bool=TRUE, meanfunc=mean, itermax=100, ...) {
        some code
        if (bool) {
            some more code
        }
        y <- meanfunc(x)
        for(i in 1:itermax) {expression}
        plot(y, ...)
    }

Here we use all the described options when defining functions: we set defaults for 'bool', a true/false value,
 'meanfunc', passing a function as an argument, and 'itermax', an integer.
And furtermore the '...' three dots argument which is passed to 'plot'.

TODO: finer points of function defs
TODO: S3 generics, default and methods

## S3 classes

R provides 2 different methods of defining classes: the S3 and S4 way. We introduce here only the S3 way.
It should be plenty for most programmers to do a great deal of work.

The way a class is defined could not be simpler. Suppose you have some data 'x', then run:

    class(x) <- "myClass"

Voila. 'x' is now of the class '"myClass"'.

Naturally, doing things like this leaves you open to quite a number of issues.
The sensible way to avoid most of them is to write a constructor function:

    myClass <- function(x, further args) {
        necessary checks on x
        class(x) <- "myClass"
        x
    }

If you use 'myClass(x)' as a constructor and instantiate '"myClass"' objects exclusively with that function,
then most of your problems go away.

Next, you will most likely want to write methods for this class. There are 3 distinct ways to do so,
depending on the intended scope of your project.

1. You just need one or two little method for your class
1. You need to write a specific method for popular function, i.e. 'print' or 'plot'
1. You need a method for quite a number of classes

For the first case, write a normal function, that checks in its body if an object has the desired class.
Like so: 'stopifnot(inherits(x, "myClass"))'
This is admittedly a janky way to do it, but there is nothing inherently wrong with it.
If that doesn't sit right with you, read on.

In the second case, there exist countless methods like 'print' in circulation. These are distinguished by dot-notation to specify which object they belong to.
if you run 'methods(print)' it will display all methods associated with the name 'print'.
You will find methods such as 'print.table', 'print.srcfile', 'print.Date' and many more.
These are all different print methods intended for the class listed after the dot.
To write a new one, simply define it in the same notation as described.
So, for example:

    print.myClass <- function(x, ...) {
        some way of printing information
        invisible(x)
    }

would be a reckognized print method. It checks if 'x' is actually of class '"myClass"'.

The last way is the way 'print' is actually defined. Type in 'print' at the command line and the output should look something like this:

    > print
    function (x, ...)
    UseMethod("print")
    <bytecode: 0x4082b50>
    <environment: namespace:base>

The call 'UseMethod("print")' tells R to look for a method called 'print', associated to the class of the first argument. In our example, R would find, that 'x' is of class '"myClass"' and accordingly search for a method called 'print.myClass'

So should you find yourself in the situation where you have a great function, that you would like to apply to all your classes,
asdfafdsasdfadsf


TODO:


## test

    $\sum_{i=0}^n$



### redo?

maybe like this:

- help system
- data structures and how to allocate them
- function definitions and s3 OO system
- efficiency
