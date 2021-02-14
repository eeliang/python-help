---
title: Concept guide
---

# Concept guide

Here we will run through key concepts in python.

## Logging

```
variable_1 = "hello"
variable_2 = "my name is"

print(variable_1 + " " + variable_2)   # prints "hello my name is"
print(variable_1, variable_2)          # prints "hello my name is"

variable_3 = variable_1 + " " + variable_2 + " piggy."

print(variable_3)                      # prints "hello my name is piggy."
```

There are several ways to communicate between the backend and the "frontend".

| Method    | Description                                                               |
| --------- | ------------------------------------------------------------------------- |
| print()   | Prints the string or number unto the console.                             |
| logger    | An built-in module that handles "print" outputs based on the environment. |
| return    | Pass values between stacks. Use as a terminating statement for functions. |

## Libraries, modules, and packages

```
|----------------- distribution -----------------|
|                                                |
|               library / package                |
|                       |                        |
|           -------------------------            |
|           |                       |            |
|   | -------------- |      | -------------- |   |
|   |     Module     |      |     Module     |   |
|   | -------------- |      | -------------- |   |
|   |     class      |      |     class      |   |
|   |    function    |      |    function    |   |
|   |    variable    |      |    variable    |   |
|   | -------------- |      | -------------- |   |
|________________________________________________|
```

The python ecosystem is made up of directories and sub-directories of python files (`.py`).

Libraries/packages are collections of modules that can be _imported_ into your python script. The python standard library is an extensive library that is prebuilt in most (if not all) python environments. For specialized disciplines, open-sourced libraries like *nunmpy* or *pandas* were created to offer useful functions like `.plot()`.

The collection is _packaged_ as a directory of files. Since it is hierarchcal, you can access `package.module` with object .method syntax


Each module is a single python file. A collection of modules is known as a library. When libraries are large enough, they can be segmented into groups of libraries under a single package.

Read this forum for [clarification](https://www.quora.com/What-is-the-difference-between-Python-modules-packages-libraries-and-frameworks).

### Modules

Modules are files that contain code. They are task specfic and usually serve a single purpose (e.g. `import math`). Unlike libraries/packages which cater to a variety of user needs.

They can be imported into your __main__ python script. Subsequently, prebuilt functions and object methods will be available to use.

### `import`

```
import math
math.factorial(4)

from math import factorial
factorial(4)

import pandas as pd         # Alias namespace
df = pd.Dataframe()
```

When you import the module, you are claiming the module filename as the namespace. Otherwise, you can use an alias to define a namespace for your module.

You may also import and specific class / function / variable.

It is recommended to use `import` statements with the module namespace intact. This allows other code-reviewer to discern when a function is called from a local file or from an external module.

### Distribution

Distributions are implementations of python that come prebuild with certain librarys. **Anaconda** is a python distribution for data anlytics that has the `matplotlib` and `numpy` packages attached, ready to be imported.

The bare-bones **CPython** accessible from terminal is an implementation of python without "extra" libraries - only the python standard library.

Find the current version of the python distribution [here](https://www.python.org/).

### Third party libraries

Third party libraries can be installed with `pip install <>`. Run this command in the _command line interface_.

## Reserved words in Python

```
True, False                     # These are boolean values
None                            # no data
from <> import <> as <>
if: elif: else:                 # conditionals
in                              # membership
for                             # loops
while
with                            # Useful for parse files
def: return                     # defining functions
lambda                          # shorthand for functions. https://www.w3schools.com/python/python_lambda.asp
and, or, not                    # logic operators
is                              # identity operators
global
assert, break, del, except, finally, is
try, except
yield, raise
```

There are reserved words in python, which are pre-defined as built-in functions, type Conversion, and other control flow tools. These cannot be used as variable names.

## Operators

Operators are based on _boolean_ values. It takes two value at any one instance and computes a `True/False` output.

### (1/5) Logic operators

```
True and False          # False
True or false           # True
not False               # True
```

These operators compares the relation between two values, in any one instance.

In python, `and` / `or` operators are executed with a short-circuit "shortcut". This allows the machine to skip over block of code that are redundant. Also known as **Short circuit evaluation**.

- `and`

Evaluates x; if x is true, evaluate y. Else (`x=False`), return x.

This means that if x is false, y is untouched. Python short-circuits the evaluation.

- `or`

Evaluates x; if x is true, returns x. If x is false, evaluate y.

This means that if x is true, y is untouched. The same short-circuit happens.

<aside class="notice">
The short circuit logic allows us to write layered statements that contains multiple conditional statements
</aside>

```python
# long method
if x%2==1:
    return "Odd"
else:
    return "Even"

lambda x:x%2 and "Odd" or "Even"
```

**Example**

- this line uses the truth value of an object, where non-empty variables are True (0=False,''=False).
- if the condition (lambda x:x%2) is True, the second clause of `and` is return. Returns "Odd". As the first clause of the `or`is True. It short circuits and the first clause is returned. Returns "Odd"
- if the condition (lambda x:x%2) is False, the `and` operator short circuits. (lambda x:x%2 and True) returns integer=0. As the first clause of the `or` is False, the second clause of `or` is evaluated. Returns "Even"

### (2/5) Comparison/Relational operators

```
x == y
x != y
x > y
x < y
x >= y
x <= y
```

These operators compares the relation between two values, in any one instance.

When evaluating strings, remember that python evaluates iteratively based on the character set, starting at the first index. Also, note that comparisons are case sensitive - capital letters have a smaller ASCII value than lowercase letters.

TODO: Concept of lazy evaluation. `and` vs `or` operator.




### (3/5) Arithmetic operators

```
addition        = 1 + 2
subtraction     = 15 - 2
multiplication  = 15 * 2
exponential     = 15 ** 2
division        = 15 / 2
division_round  = 15 // 2       # round down to integer value
modulus         = 15 % 2        # remainder
```

Operators that are used to perform comparisions using mathematical notation. Arithmetic operation uses `==` as "equals", `!=` as "not-equals".

Python performs the `modulus` operation different from other programming languages. See this image on the comparison between programming languages for modulus operation on negative numbers [here](https://drive.google.com/file/d/1DhX5IWIKdhjtxqbWr4WQ68LRv_rgWenl/view?usp=sharing).

Arithmetic operators works for strings, list, and  tuples, but behave differently.


### (4/5) Identity operators

```
a = [1, 2, 3]
b = a
c = [1, 2, 3]

print(a == c)                   # this is true, == compares the values
print(a is c)                   # this is false
print(a is b)                   # this is true, the variables are set to mirror the memory location.

print(1 in a)                   # this is true
```

This is also based on _boolean_ values. These operators describe the relation between two values, in any one instance. It either returns True or False according to the condition. You can compare across data types; including membership information (list, tuple, dictionary, set).

The `is` operators answer the question: "if the two comparisions share the same **memory space**". For most immutable variables, `is` equates to `==`. But, not for list, as this is a mutable data containter. Two lists can currently hold the same information, but have different memory locations.

### (5/5) Bitwise operators

```
a = 10 = 1010
b = 6  = 0110

print(a & b)                    # 2  = 0010. Spots overlaps.
print(a | b)                    # 14 = 1110 = 8+4+2
print(~a)                       # -11 = -(1010 + 1)
print(a ^ b)                    # 12 = 1100. Has to be 1/0 pairing.
print(a >> 1)                   # 10 = 0101. All bits move to the right.
print(a << 2)                   # 40 = 101000. All bits move to the left.
```

Bitwise operators acts on bits and performs bit by bit operation.



