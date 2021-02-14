---
title: Datatypes and operators
---

# Datatypes and operators

```
print(type(variable))           # use this to identify the type

123         # integer
1.23        # float
"Hello"     # Digits, punctuation, and ascii letters

[1,2,3]     # List - can contain mixed datatypes
(1,2,3)     # Tuple
{"key": 1}  # Dictionary
{1,2,3}     # Set
```

There are basic datatypes ("primitives") that are found in all computing languages.

More advanced datatypes ("Data structures") are _collections_ of the basic datatypes. Data structures comes in two flavors - ordered and un-ordered.

|            | Mutable    | Immutable |
| ---------- | ---------- | --------- |
| Ordered    | list       | tuple     |
| Un-ordered | dictionary | set       |

Note that **sets** have mutable and immutable variations.

## Number

```
weight = 64.5
height = 1.69

BMI = weight / (height ** 2)    # 22.583242883652535
'%.3f'%(BMI)                    # 22.583
round(BMI,2)                    # 22.58

BMI + 5                         # 27.583242883652535
```

Integer and floats are python's most common number datatype. You can use arithmetic operators as boolean values.

## String

Places where you might encounter strings.

| Places                | Description                           |
| --------------------- | ------------------------------------- |
| Asking for user input | `name = input("What is your name? ")` |
| Validating a string   | `if "n" in string:`                   |

A method in Python behaves similarly to a function. Methods actually are functions that are called using dot notation.

Some methods do not touch the base value and returns a new temporary output. Make sure to save these values as a new variable. While other method change the values of the base variable (these methods contains "side-effects").

Run `dir(str)` to see a list of available methods for that object.

Python treats lists and strings as iterables, thus methods that work for lists will work for strings.

### Manipulating strings

```
"hELLO".capitalize()        # "Hello"                       Only first character
"hey hello".title()         # "Hey Hello"                   Title style
"hello123".upper()          # "HELLO123"                    All alphabets
"HELLO123".lower()          # "hello123"                    All alphabets
"hello".ljust(15,' ')       # "hello          "             efault fill character is whitespace
"hello".center(25,'~')      # "~~~~~hello~~~~~"             Centralize and fill
"   boo   ".strip()         # "boo"                         Combines .lstrip() and .rstrip()
"hey.hey".split('.', 1)     # ['hey', 'hey']                Default seperator is ' ', specify maxsplit pieces
"fat\tbunny".expandtabs()   # 'fat     bunny'               Fills until next tabspace (default by 8 spaces)
"German_ß".casefold()       # "german_ss'                   For non-english languages. In German (ß.upper, ss.lower)
```

You can manipulate string by adding (concatenate) or padding the string with characters.

One common use case for manipulating strings is to retrieve specific information from user-input. In this scenario is crucial to understand the format on the incoming data in order to formulate rules to parse the data.

You can also format a string for output. Your use-case may require you to print to console using a certain format (for readability) or use spacing to create a diagram.

### String interpolation

```
# 1. OG method from C
'In %d years I have spotted %g %s.' % (3, 0.1, 'camels')    # tuple elements are processed sequentially
                                                            # data types must match

"My %s is %i." % ('dog',10)                                 # "My dog is 10."
"%(x)03d and %(y)d" % ({"x": 2, "y": 10})                   # '002 and 10'

# 2. format() method.
"My {} is {}.".format('dog',10)                             # no need to specify data type
"My {0} is {1}.".format('dog',10)                           # using index calls
"{x} and {y}".format(x=2, y=10)                             # using named index
"{x:03d} and {y}".format_map({"x": 2, "y": 10})             # using key index

# 3. f-string format
name = "bunny"
book = {'chapter':"introduction","page":2}

f"{name} is reading the book {book['chapter']!r} on page {book['page']:03d}"
>>> "bunny is reading the book 'introduction' on page 002"
```

It is common to format strings for output. This is used in logging scenarios or used to write informative `repr` when creating your own modules and packages.

One way to format string dynamically with variables is to use **String interpolation**. Using this, you can substitute variables in the string outputs to create dynamic content. From python 3.8<, it is recommended to use [f-strings](https://docs.python.org/3/reference/lexical_analysis.html#f-strings).

With f-strings, you can perform conversion [!] and formatting [:]. The conversion specifier is mostly used to cast non-string values into stringdatatypes (`!s` or `!r`).

Other dated methods for string interpolation are available in python. You can use the [**% method**](https://docs.python.org/3/library/stdtypes.html#printf-style-string-formatting) most practiced in the C language.

You may also use the built-in `.format()` method to apply treatment to your output string. This [format() method](https://docs.python.org/3/library/stdtypes.html#string-formatting) allowed you to use key-value pairs for string interpolation. This was a huge improvement in code readability. However, the resulting code was often very lengthy.

### Searching strings

```
"bunny".count('n')          # 2                             Case sensitive
"Hello".find('l')           # 2                             Case sensitive, "-1" means not found
"Hello".rfind('l')          # 3                             Search from end
"Hello".index('w')          # ValueError: substring not found
```

It is common to search for matching in strings. See [regex](#) for more information on string matching.

It may be sufficient to find where a value exist ('match' in string), while other use-cases might require you to obtain the index of the occurrence.

### Evaluating strings

```
sample_str.endswith('.')    # True                          Case sensitive (check for company email address)
sample_str.isspace()        # False                         Only whitespace (e.g. \t \n) (i.e. useless strings)
sample_str.isprintable()    # True                          Spots non-printable characters (e.g. escape sequences)
sample_str.isalnum()        # False                         Spots whitespace, symbols
sample_str.isnumeric()      # False                         Spots whitespace, symbols, alphabets.
sample_str.isalpha()        # False                         Spots whitespace, symbols, numeric characters (super/sub, fractions)
sample_str.islower()        # False                         Spots whitespace, symbols, numeric characters, UPPERCASE
sample_str.isupper()        # False                         Spots whitespace, symbols, numeric characters, lowercase
sample_str.istitle()        # True                          Spots Nicely Titled Strings Including $@#$ Symbols
```

Another common scenario is to evaluate strings against certain criteria. Checking if the string contains numeric characters or alphabets.

## List

```
list_friends[0]                         # first item of the list        0 steps from the front
list_friends[len(list_friends) - 1 ]    # last item of the list         Shorthand: use -1
list_months[6:]                         # jul to dec
list_months[:3]                         # jan, feb, mar                 Exclude [3]
list_months[::2]                        # all odd months                Step by 2
```

An ordered collection of items. The items are mutable and a list can contain duplicates.

Python treats lists and strings as iterables, thus methods that work for lists will work for strings.

### Slicing

```
basket = ["apple", "banana", "carrot"]
basket[1:]      #["banana", "carrot"]
basket[:-1]     # ["apple", "banana"]
```

Ordered collections can be accessed by the index. Index supports _slicing_.

Slicing returns an images of the list.

### `sort()`

```
sorted(basket, reverse=True)            # ["carrot", "banana", "apple"]
basket.sort(reverse=True)               # Updates existing list, but does not return anything!
```

This is a built-in method for operating on list datatypes. Since, this is a destrucive action, it is recommended that you use it with caution.

Unless necessary, it is recommended to use the first-level function `sorted()` instead.

### `.join()`

```
"-".join(basket)                        # "apple-banana-carrot"
```

The input to this method is an iterable. If a list is provided, each element within the list is processed. If a string is provided, each character will be processed.

This method returns a string. The input is concatenated with the joining character provided.

### The python way of working with list

```
even_numbers = [ x for x in range(0,100) if x%2==0  ]
```

List comprehension provides a concise way of creating lists. For more information, see [here](#).

## Tuple

```
bmi_me = 170, 63.9
height_me, weight_me = bmi_me           # assigning multiple variables with a tuple
height_me, weight_me = 170, 63.9        # the variable on LHS are assigned to the values on RHS respectively

def merge_into_tuple(*arg):             # tuple gathering
    return  arg

tu = (7,3)
divmod(*tu)                             # tuple scattering
```

Works like a list. But they are immutable. For more information about differences, see [here](https://www.afternerd.com/blog/difference-between-list-tuple/).

Tuples works best for collection of data that go together (.e.g longitudinal and latitudinal coordinates). You can call elements out by the index.

## Dictionary

```
elements = {
    "hydrogen" : {                                      # note the : symbol, this key corresponds to a value (dictionary)
        "number" : 1,
        "weight" : 1.00794,
        "symbol" : H
    },
    "helium" : {
        "numnber" : 2,
        "weight" : 4.002602,
        "symbol" : "He"
    }
}

print(elements["helium"]["weight"])                     # call the nested values by calling the parent keys
```

A collection of `key:value` pairs. In other languages, it might be called an associative array. Items are retrieved and added using a single "lookup" tag. Notice the simply way of adding new records, unlike `.append()` or `.add()`.

Nested dictionaries are ways to store data in a tree structure. Much like other langugages (e.g. JSON). See here for other [dictionary methods](/python/basics/data-types-and-operators/data-collection-methods.md#dictionary-methods).


### `.get()`

```
pets = {"population": 2, "rabbit": "malfoy", "dog": "goldie"}

print("flowers" in pets)                     # KeyError, as the record does not exist
print(pets.get("flower"))                    # prints "none"
print(pets.get("flower", "Missing key!"))    # "Missing key!"
```

This method retrieves the value corresponding to the given key. You can specify the return value if the key does not exist.

### `.keys()`

```
pets.keys()             # ["population", "rabbit", "dog"]

"dog" in pets           # True
"dog" in pets.keys()    # True
```

This method returns a list of keys. Use this method to iterate through the keys of a dictionary.

**Note**: Since python innately treats dictionary as keys. It is redundant to use the membership operator on `.keys().`

### `.values()`

```

```

Use the `.values()` method to call out all the values. Note that this method is a [view object](https://docs.python.org/3/library/stdtypes.html#dict-views).

If your dictionary is a collection of similarly formatted elements, use `.values()` to run through them as you would with a list.

### `.items()`

```
pets.items()            # [('population', 2), ('rabbit', 'malfoy'), ('dog', 'goldie')]
```

This method returns a list of tuples. Each tuple contains the key at index 0, and the stored value as index 1.

If your value is a _collection_ of items, remember to apply additional parsing to read the nested data.

## Set

```
set_organs = {"brain", "heart", "liver"}
set_face = set(["ear", "ear", "eye", "eye"])            # creating a set from a list
```

A collection of unique values without any order.

Sets are most useful to evaluate if there are common items between two collections.

