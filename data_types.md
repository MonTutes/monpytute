# Data Types

Some of the modules are the ones I use most often, as they can help to reduce code or make things more maintainable.

## datetime — Basic date and time types

## calendar — General calendar-related functions

## collections — Container datatypes

### namedtuple()

`namedtuple` is kind-of like a type which is somewhere between a `tuple` and a `class`.

They are useful if you need to group a number of related variable together to increase maintenance, but don't need the extensibility of a class. They can be easily converted to a `tuple` or `dict` as needed, and properties can be accessed by name, as shown below. 

```python
from collections import namedtuple
DogType = namedtuple('DogType', ['name', 'temperament'])

border_collie = DogType(name="Border Collie", temperament=["playful", "energetic", "intelligent"])

print(border_collie) # -> DogType(name='Border Collie', temperament=['playful', 'energetic', 'intelligent'])
print(border_collie.name) # -> Border Collie
print(border_collie.temperament) # -> ["playful", "energetic", "intelligent"
print(tuple(border_collie)) # -> ('Border Collie', ['playful', 'energetic', 'intelligent'])
print(border_collie._asdict()) # -> OrderedDict([('name', 'Border Collie'), ('temperament', ['playful', 'energetic', 'intelligent'])])
```

### deque

Like a list which you can append/remove efficiently from either the left or right-hand side.

```python

```

### ChainMap

### Counter

Counters are derived from `dict`, and allows keeping track of how many of a certain 

### OrderedDict

A `dict` which is guaranteed to have keys in the order in which they were assigned.

Perhaps not as essential as it once was as `dict` objects since python 3.6 are also in the order they were assigned, but it may be a good idea to use this type if your code is likely to be used on older versions or other implementations than CPython, or there is a use for methods like `move_to_end` or `popitem`. 

### defaultdict

This is not only a nice-to-have which reduces the amount of code needed when you're using the `dict.setdefault()` method a lot, but can also be faster, as a list object isn't created and discarded for subsequent appends. For instance,

```python
from collections import defaultdict

my_dict = defaultdict([])
my_dict['mykey'].append(1)
my_dict['mykey'].append(2)
```

is the same as 

```python
my_dict = {}
my_dict.setdefault('mykey', []).append(1)
my_dict.setdefault('mykey', []).append(2)
```

## collections.abc — Abstract Base Classes for Containers

## heapq — Heap queue algorithm

I have only ever used 2 methods in this module: `nlargest` and `nsmallest`.

```python
import heapq
print(heapq.nlargest(3, [5, 10, 20, 40, 80])) # -> [80, 40, 20]
print(heapq.nsmallest(3, [5, 10, 20, 40, 80])) # -> [5, 10, 20]
```

## bisect — Array bisection algorithm

Python calls this "bisect" or a bisection algorithm, but virtually everywhere else I've seen these functions they've been called ["binary search"](https://en.wikipedia.org/wiki/Binary_search_algorithm) or "insertion sort" functions.

They allow fast, memory-efficient finding of items in a sorted list. There are 2 main functions: either to the left (`bisect_left`) or right (`bisect_right`) of an item. While there `insort_left` and `insort_right` functions, I've never used these, preferring to batch sort as calling `list.insert()` can be inefficient.

```python
from bisect import bisect_left, bisect_right
print(bisect_left([0, 5, 10, 15], 10)) # -> 2
print(bisect_right([0, 5, 10, 15], 10)) # -> 3
```

## array — Efficient arrays of numeric values

This module allows very memory-efficient reading and writing of binary data, but I've found you need to be a bit careful as it doesn't exactly mirror the `struct` module's types, and you may need to call `array.byteswap()` if the machine which wrote the data has the opposite [endian-ness](https://en.wikipedia.org/wiki/Comparison_of_instruction_set_architectures#Endianness).

```python
from os.path import getsize
from array import array

a = array('I')
a.append(50)
a.append(55)

with open("my_binary_data.bin", "wb") as f:
    a.tofile(f)

b = array('I')
with open("my_binary_data.bin", "rb") as f:
    b.fromfile(f, getsize("my_binary_data.bin")//a.itemsize)

print(b) # -> array('I', [50, 55])
```

## weakref — Weak references

## types — Dynamic type creation and names for built-in types

## copy — Shallow and deep copy operations

There are two functions - `copy` for shallow copy, and `deepcopy` for deep copying objects.

```python
from copy import copy, deepcopy

my_list = [[1, 2, 3]]
copied_my_list = copy(my_list)
deepcopied_my_list = deepcopy(my_list)

my_list.append(5)
my_list[0].append(55)

print(copied_my_list) # -> [[1, 2, 3, 55]]
print(deepcopied_my_list) # -> [[1, 2, 3]]
```

Here, the shallow copied object didn't have the 5 appended on the parent list, but it's clear the child list is a reference to the original (uncopied) object. `deepcopy` might be slower, but it can avoid this kind of problem.

## pprint — Data pretty printer

A module which is useful for printing large, complex data types to console.

```python
from pprint import pprint
o = {55: {33: {22: {"sleep": ["The quick brown fox jumps over the lazy dog"*4]}}}}

pprint(o)
# -> {55: {33: {22: {'sleep': ['The quick brown fox jumps over the lazy dogThe '
#                          'quick brown fox jumps over the lazy dogThe quick '
#                          'brown fox jumps over the lazy dogThe quick brown '
#                          'fox jumps over the lazy dog']}}}}
```

## reprlib — Alternate repr() implementation

## enum — Support for enumerations

It can often be cleaner and easier to use the `enum` module than have lots of integer defines which you need to keep updated.

```python

from enum import Enum, auto

class Animals(Enum):
    SQUIRREL = auto()
    HEDGEHOG = auto()
    LEMMING = auto()

print(Animals.SQUIRREL) # -> Animals.SQUIRREL
print(Animals.SQUIRREL.value) # -> 1
print(Animals.HEDGEHOG.value) # -> 2
```

There are many more powerful ways to use this module in [the docs](https://docs.python.org/3/library/enum.html).
