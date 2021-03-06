---
title: List comprehension
---

# Working with python list

```
# Bad practice.

count = []
price_list = [1,2,3,4,5]

for i in price_list:
    count = count + i
```

Python lists are wonderful. They perform `.pop`, `.append` at O(1) time, as well as index operations at O(1) - combining the best of the Array and Linked List data structures.

However, python is horrendously slow at performing custom operations to create, edit, or filter lists. Thus, it is recommended to use either a built-in function or to use list comprehensions.

## `zip()`

```
x, y = [1, 2, 3], ["a", "b", "c"]
zipped = zip(x, y)
print(list(zipped))                     # [(1, "a"), (2, "b"), (3, "c")]
x2, y2 = zip(*zipped)
print(x == list(x2) and y == list(y2))  # True
```

You can create ordered data by _stitching_  matching pairs from different data containers.

Use `zip()` to pull together _n_ list into a list of tuples. `zip()` also works to un-zipped a _n_ dimension list.

## `enumerate()`

```
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print(list(enumerate(seasons)))                     # [(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
```

Use `enumerate()` to create ordered data containers by attaching the index as a __index__:__value__ pair.

## `map()`

```
map(lamda x: print(x), range(10))
```

This is the equivalent of `.each` in Javascript or `.foreach` in Ruby. This is a top-level function.

Supply a function variable and _n_ iterables to apply the function on.

## List comprehension

```
long_method = []
for x in range(0, 9, 2):
    long_method.append(x**2)                                            # [0, 4, 16, 36, 64]
print(x)                                                                # x persist outside. Bad practice

lamba_method = list(map(lambda x: x**2, range(0, 9, 2)))

short_method = [x ** 2 for x in range(0, 9, 2)]                         # list
generators = (x ** 2 for x in range(0, 9, 2))                           # generator
```

List comprehension provides a concise way of creating lists. In the long form, list comprehension is taking a block of logic (_function_ + _loop_) and appying it to an iterable.

This has the advantage of requiring less memory capacity. When using the **long method**, a variable named `x` will still exist outside of the loop. But with the **lambda_method** , the `lambda x:` does not persist outside of the code block.

## Iterators and Generators

```
# Iterator
range(10)           # a stream of elements
pet.keys()

# Generator
def squares(start, stop):
    for i in range(start, stop):
        yield i * i

generator = squares(a, b)

generator = (i*i for i in range(a, b))
```

Strings and lists are objects that are iterable - meaning that they can return one element at a time. But iterators are unique because it is an object that represents a stream of data.

Streams are useful because they represent large amounts of data, but because they are not processed into memory immediately, they occupy minimal memory or computing demands.

Successive elements from the iterator can be called using the `.next()` method. Using a list comprehension or `for..in..` syntax automatically executes this method.

Generators are a special subset of iterators that outputs custom values produced from a function. Every time the generator is called, the function stack is activated.


