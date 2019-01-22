---
interact_link: content/01-python-basics.ipynb
title: 'Python basics'
prev_page:
  url: /00-first-steps
  title: 'First steps'
next_page:
  url: /02-programs
  title: 'Programs'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---

# Python

## Notation

When writing computer commands that you can type, the font will change to `command`. For example, `x=2**3.4/5` is a command that can be typed in.

When we talk about a general command, or some piece of missing data that you should complete, we will use angle brackets as in `<command>` or `<variable>`. For example, `<location>` could mean `"Southampton"`.

When showing actual commands as typed into Python, they will start with `In [<number>]:`. This is the notation used by the IPython console. The `<number>` allows you to refer to previous commands more easily. The output associated with that command will start with `Out [<number>]:`.

When displaying code, certain commands will appear in different colours. The colours are not necessary. They highlight different types of command or variable. When using the spyder editor you may find the colours match up and are useful: if not, either ignore them or switch them off.

## The console - Python as calculator

Start with using Python as a calculator. Look at the *console* in the bottom right part of spyder. Here we can type commands and see a result. Simple arithmetic gives the expected results:



{:.input_area}
```python
2+2
```





{:.output .output_data_text}
```
4
```





{:.input_area}
```python
(13.5*2.6-1.4)/10.2
```





{:.output .output_data_text}
```
3.3039215686274517
```



If we want to raise a number to a power, say $2^4$, the notation is `**`:



{:.input_area}
```python
2**4
```





{:.output .output_data_text}
```
16
```



There is an issue with division. If we divide an integer by an integer, Python `3.X` will do *real* (floating point) division, so that:



{:.input_area}
```python
5/2
```





{:.output .output_data_text}
```
2.5
```



However, Python `2.X` will do division in the integers:

```python
In []: 5/2
Out []: 2
```

If you are using Python `2.X` and want the division operator to behave in this way, start by using the command



{:.input_area}
```python
from __future__ import division
```


Then:



{:.input_area}
```python
5/2
```





{:.output .output_data_text}
```
2.5
```



If you really want to do integer division, the command is `//`:



{:.input_area}
```python
5//2
```





{:.output .output_data_text}
```
2
```



Further mathematical commands, even things as simple as $\log$ or $\sin$, are not included as part of basic Python:



{:.input_area}
```python
log(2.3)
```



{:.output .output_traceback_line}
```
---------------------------------------------------------------------------
```

{:.output .output_traceback_line}
```
NameError                                 Traceback (most recent call last)
```

{:.output .output_traceback_line}
```
<ipython-input-8-83d4dd34e7bf> in <module>()
----> 1 log(2.3)

```

{:.output .output_traceback_line}
```
NameError: name 'log' is not defined
```




{:.input_area}
```python
sin(1.4)
```



{:.output .output_traceback_line}
```
---------------------------------------------------------------------------
```

{:.output .output_traceback_line}
```
NameError                                 Traceback (most recent call last)
```

{:.output .output_traceback_line}
```
<ipython-input-9-6dd12df070cd> in <module>()
----> 1 sin(1.4)

```

{:.output .output_traceback_line}
```
NameError: name 'sin' is not defined
```


First, note the way that errors are reported: we'll see this a lot, and there's useful information there to understand. It's telling us

1. Where the problem occurred
2. What the problem is

The language Python uses takes some getting used to, but it's worth the effort to read these messages, and think about what it's trying to say. Here it's pointing to the line where the problem happened, and saying "I don't understand what this command is!".

Going back to the mathematics, we obviously want to be able to compute more mathematical functions. For this we need a *module* or *package*.

## Importing modules and packages

Anything that isn't provided by the base Python can be provided by modules and packages. A module is a file containing functions and definitions that we can include and use in our code. A package is a collection of modules. They're not included by default, to reduce overhead. They're easy to write - we will write our own later - and easy to include.

To use a package we must *import* it. Let's look at the `math` package.



{:.input_area}
```python
import math
```




{:.input_area}
```python
math.log(2.3)
```





{:.output .output_data_text}
```
0.8329091229351039
```





{:.input_area}
```python
math.sin(1.2)
```





{:.output .output_data_text}
```
0.9320390859672263
```



To use the package we've typed `import <package>`, where in this case `<package>` is `math`. Then we can use functions from that package by typing `<package>.<function>`, as we have here when `<function>` is either `log` or `sin`.

The "dot" notation may seem annoying, and can be avoided by specifying what functions and constants we want to use. For example, we could just get the `log` function and use that:



{:.input_area}
```python
from math import log
```




{:.input_area}
```python
log(2.3)
```





{:.output .output_data_text}
```
0.8329091229351039
```



However, the "dot" notation is useful, as we often find the same symbol or name being used for many different purposes. For example, the `math` package contains the mathematical constant $e$ as `math.e`:



{:.input_area}
```python
math.e
```





{:.output .output_data_text}
```
2.718281828459045
```



But there is also the electron charge, usually denoted $e$, which is in the `scipy.constants` package:



{:.input_area}
```python
import scipy.constants
```




{:.input_area}
```python
scipy.constants.e
```





{:.output .output_data_text}
```
1.6021766208e-19
```



To avoid these name clashes we can import something *as* a different name:



{:.input_area}
```python
from math import e
```




{:.input_area}
```python
from scipy.constants import e as charge_e
```




{:.input_area}
```python
e
```





{:.output .output_data_text}
```
2.718281828459045
```





{:.input_area}
```python
charge_e
```





{:.output .output_data_text}
```
1.6021766208e-19
```



You will often see this method used to shorten the names of imported modules or functions. For example, standard examples often used are:



{:.input_area}
```python
import numpy as np
```




{:.input_area}
```python
import matplotlib.pyplot as plt
```


The commands can then be used by typing `np.<function>`, or `plt.<function>`, which saves typing. We would encourage you *not* to do this as it can make your code less clear.

## Variables

A *variable* is an object with a name and a value:



{:.input_area}
```python
x = 2
```


In standard programming all variables must have a value (although that value may be a placeholder to say "this variable doesn't have a reasonable value *yet*"). Only symbolic packages can mirror the analytical method of having a variable with no specific value. However, code can be written *as if* the variables had no specific value.

For example, we cannot write



{:.input_area}
```python
x = y**2
```



{:.output .output_traceback_line}
```
---------------------------------------------------------------------------
```

{:.output .output_traceback_line}
```
NameError                                 Traceback (most recent call last)
```

{:.output .output_traceback_line}
```
<ipython-input-25-9736a48890b4> in <module>()
----> 1 x = y**2

```

{:.output .output_traceback_line}
```
NameError: name 'y' is not defined
```


as `y` does not have a specific value yet. However, we can write



{:.input_area}
```python
y = 3.14159627
```




{:.input_area}
```python
x = y**2
```




{:.input_area}
```python
print(x)
```


{:.output .output_stream}
```
9.869627123677912

```

and get a sensible result, even though we have written the exact same line of code, as now `y` has a specific value.

##### Warning

Note that we have defined the variable `x` twice in rapid succession: first as an *integer* (`x=2`) and next as a *floating point number*, or *float* (the computer's implementation of a real number, using `x=y**2`, where `y` is a float). Not all programming languages allow you to do this. In a *statically typed* language you have to say whether a variable will be an integer, or a float, or another type, before you define it, and then it cannot change. Python is *dynamically typed*, so any variable can have any type, which can be changed as we go.

## Variable names

A variable is an object with a name, but not just any name will do. Python has rules which *must* be followed, and conventions that *should* be followed, with a few gray areas.

Variables *must*

* not contain spaces
* not start with a number
* not contain a special character (such as `!@#$%^&*()\|`)

So the following are valid:



{:.input_area}
```python
half = 1.0/2.0
```




{:.input_area}
```python
one_half = 1.0/2.0
```


but the following are not:



{:.input_area}
```python
one half = 1.0/2.0
```



{:.output .output_traceback_line}
```
  File "<ipython-input-31-3d1440172542>", line 1
    one half = 1.0/2.0
           ^
SyntaxError: invalid syntax

```




{:.input_area}
```python
1_half = 1.0/2.0
```



{:.output .output_traceback_line}
```
  File "<ipython-input-32-7867c2b402d6>", line 1
    1_half = 1.0/2.0
         ^
SyntaxError: invalid syntax

```




{:.input_area}
```python
one!half = 1.0/2.0
```



{:.output .output_traceback_line}
```
  File "<ipython-input-33-d585fc045f28>", line 1
    one!half = 1.0/2.0
       ^
SyntaxError: invalid syntax

```


Variables *should*

* be descriptive, ie say what their purpose is in the code
* be written entirely in lower case
* separate different words in the variable name using underscores

More detail can be found in [PEP8](https://www.python.org/dev/peps/pep-0008/).

Variables *may* contain some unicode characters, depending on Python version and operating system. In Python `3` you can include accents or extended character sets in variable names:

```python
rôle = 5
π = math.pi
```

However, these tricks are not always portable between different Python versions (they aren't guaranteed to work in Python `2`), or different operating systems, or even different machines. To ensure that your code works as widely as possible, and that the methods you use will carry over to other programming languages, it is recommended that variables do not use any extended characters, but only the basic latin characters, numbers, and underscores.

## Equality and variable assignment

One thing that may seem odd, or just plain *wrong* to a mathematician, is two statements like



{:.input_area}
```python
x = 2
```




{:.input_area}
```python
x = 3
```


How can `x` equal *both* 2 and 3? Mathematically, this is nonsense.

The point is that, in nearly every programming language, the `=` symbol is not mathematical equality. It is the *assignment* operation: "set the value of the variable (on the left hand side) equal to the result of the operation (on the right hand side)". This implies another difference from the mathematical equality: we cannot flip the two sides and the line of code mean the same. For example,



{:.input_area}
```python
3 = x
```



{:.output .output_traceback_line}
```
  File "<ipython-input-36-6f12c1f282a0>", line 1
    3 = x
         ^
SyntaxError: can't assign to literal

```


immediately fails as `3` is not a variable but a fixed quantity (a *literal*), which cannot be assigned to. Mathematically there is no difference between $x=3$ and $3=x$; in programming there is a huge difference between `x=3` and `3=x` as the meaning of `=` is not the mathematical meaning.

To get closer to the standard mathematical equality, Python has the `==` operator. This compares the left and right hand sides and says whether or not their values are equal:



{:.input_area}
```python
x == 3.0
```





{:.output .output_data_text}
```
True
```



However, this may not be exactly what we want. Note that we have assigned `x` to be the *integer* 3, but have compared its value to the *float* 3.0. If we want to check equality of value and type, Python has the `type` function:



{:.input_area}
```python
type(x)
```





{:.output .output_data_text}
```
int
```





{:.input_area}
```python
type(x) == type(3.0)
```





{:.output .output_data_text}
```
False
```





{:.input_area}
```python
type(x) == type(3)
```





{:.output .output_data_text}
```
True
```



Direct comparisons of equality are often avoided for floating point numbers, due to inherent numerical inaccuracies:



{:.input_area}
```python
p = 2.01
```




{:.input_area}
```python
p**2-4.0401
```





{:.output .output_data_text}
```
-8.881784197001252e-16
```





{:.input_area}
```python
p**2 == 4.0401
```





{:.output .output_data_text}
```
False
```



We will return to this later.

# Debugging

Making mistakes and fixing them is an essential part of both mathematics and programming. When trying to fix problems in your code this process is called *debugging*. As you've been following along with the code you will have made "mistakes" as there are intentionally broken commands above to show, for example, why `one!half` is not a valid variable (and you may have made unintentional mistakes as well).

There are a number of techniques and strategies to make debugging less painful. There's more detail in later chapters, but for now let's look at the crucial first method.

## Reading the error message

When you make a mistake Python tells you, and in some detail. When using IPython in particular, there is much information you can get from the error message, and you should read it in detail. Let's look at examples.

### Syntax error

A *syntax error* is when Python cannot interpret the command you have entered.



{:.input_area}
```python
one half = 1.0/2.0
```



{:.output .output_traceback_line}
```
  File "<ipython-input-44-3d1440172542>", line 1
    one half = 1.0/2.0
           ^
SyntaxError: invalid syntax

```


This example we saw above. The `SyntaxError` is because of the space - `one half` is not a valid variable name. The error message says `invalid syntax` because Python can't interpret the command on the left of the equals sign. The use of the carat `^` points to the particular "variable" that Python can't understand.



{:.input_area}
```python
x = 1.0 / ( 2.0 + (3.0 * 4.5)
```



{:.output .output_traceback_line}
```
  File "<ipython-input-45-da9f857ed183>", line 1
    x = 1.0 / ( 2.0 + (3.0 * 4.5)
                                 ^
SyntaxError: unexpected EOF while parsing

```


This example is still a `SyntaxError`, but the pointer (`^`) is indicating the end of the line, and the statement is saying something new. In this statement `unexpected EOF while parsing`, "`EOF`" stands for "end of file". This can be reworded as "Python was reading your command and got to the end before it expected".

This usually means something is missing. In this case a bracket is missing - there are two left brackets but only one right bracket.

A similar example would be



{:.input_area}
```python
name = "This string should end here...
```



{:.output .output_traceback_line}
```
  File "<ipython-input-46-e75a715c38f0>", line 1
    name = "This string should end here...
                                          ^
SyntaxError: EOL while scanning string literal

```


In this case the error message includes "`EOL`", standing for "end of line". So we can reword this message as "Python was reading your command and got to the end of the line before the string finished". We fix this by adding a `"` at the end of the line.

Finally, what happens if the error is buried in many lines of code? This isn't the way we'd enter code in the console, but is how we'd deal with code in the notebook, or in a script or file:



{:.input_area}
```python
x = 1.0
y = 2.3
z = 4.5 * x y + y
a = x + y + z
b = 3.4 * a
```



{:.output .output_traceback_line}
```
  File "<ipython-input-47-8b0bd2354b36>", line 3
    z = 4.5 * x y + y
                ^
SyntaxError: invalid syntax

```


We see that the error message points to the *specific line* that it can't interpret, *and* it says (at first) which line this is.

### Name Errors

This is where Python doesn't know the variable you're trying to refer to:



{:.input_area}
```python
my_variable = 6
my_variable_2 = 10
x = my_variable + my_variable_3
```



{:.output .output_traceback_line}
```
---------------------------------------------------------------------------
```

{:.output .output_traceback_line}
```
NameError                                 Traceback (most recent call last)
```

{:.output .output_traceback_line}
```
<ipython-input-48-06bcebc035d2> in <module>()
      1 my_variable = 6
      2 my_variable_2 = 10
----> 3 x = my_variable + my_variable_3

```

{:.output .output_traceback_line}
```
NameError: name 'my_variable_3' is not defined
```


It usually means you've made a typo, or have referred to a variable before defining it (sometimes by cutting and pasting code around). Using tab completion is a good way of minimizing these errors.

Note that there is a difference between syntax errors and other errors. Syntax errors are spotted by the code before it is run; other errors require running the code. This means the format of the output is different. Rather than giving the line number and using a carat ("`^`") to point to the error, instead it points to the code line using "`---->`" and adds the line number before the line of code.

### Numerical errors

A range of "incorrect" mathematical operations will give errors. For example



{:.input_area}
```python
1.0/0.0
```



{:.output .output_traceback_line}
```
---------------------------------------------------------------------------
```

{:.output .output_traceback_line}
```
ZeroDivisionError                         Traceback (most recent call last)
```

{:.output .output_traceback_line}
```
<ipython-input-49-fd44f356366a> in <module>()
----> 1 1.0/0.0

```

{:.output .output_traceback_line}
```
ZeroDivisionError: float division by zero
```


Obviously dividing by zero is a bad thing to try and do within the reals. Note that the definition of floating point numbers *does* include the concept of infinity (via "`inf`"), but this is painful to use and should be avoided where possible.



{:.input_area}
```python
math.log(0.0)
```



{:.output .output_traceback_line}
```
---------------------------------------------------------------------------
```

{:.output .output_traceback_line}
```
ValueError                                Traceback (most recent call last)
```

{:.output .output_traceback_line}
```
<ipython-input-50-7a32bd6f7959> in <module>()
----> 1 math.log(0.0)

```

{:.output .output_traceback_line}
```
ValueError: math domain error
```


A `ValueError` generally means that you're trying to call a function with a value that just doesn't make sense to it: in this case, $\log(x)$ just can't be evaluated when $x=0$.



{:.input_area}
```python
10.0**(10.0**(10.0**10.0))
```



{:.output .output_traceback_line}
```
---------------------------------------------------------------------------
```

{:.output .output_traceback_line}
```
OverflowError                             Traceback (most recent call last)
```

{:.output .output_traceback_line}
```
<ipython-input-51-c25c175740ef> in <module>()
----> 1 10.0**(10.0**(10.0**10.0))

```

{:.output .output_traceback_line}
```
OverflowError: (34, 'Result too large')
```


An `OverflowError` is when the number gets too large to be represented as a floating point number.

### General procedure

Having read the error message, find the line in your code that it indicates. If the error is clear, then fix it. If not, try splitting the line into multiple simpler commands and see where the problem lies. If using spyder, enter the commands into the editor and see if the syntax highlighting helps spot errors.

# Exercise: Variables and assignment

## Exercise 1

Remember that $n! = n \times (n - 1) \times \dots \times 2 \times 1$. Compute $15!$, assigning the result to a sensible variable name.

## Exercise 2

Using the `math` module, check your result for $15$ factorial. You should explore the help for the `math` library and its functions, using eg tab-completion, the spyder inspector, or online sources.

## Exercise 3

[Stirling's approximation](http://mathworld.wolfram.com/StirlingsApproximation.html) gives that, for large enough $n$, 

$$  n! \simeq S = \sqrt{2 \pi} n^{n + 1/2} e^{-n}. $$

Using functions and constants from the `math` library, compare the results of $n!$ and Stirling's approximation for $n = 5, 10, 15, 20$. In what sense does the approximation improve (investigate the absolute error $\|n! - S\|$ and the relative error $\|n! - S\| / n!$)?
