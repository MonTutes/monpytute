# Data Types

Some of the modules are the ones I use most often, as they can help to reduce code or make things more maintainable.

## datetime — Basic date and time types

## calendar — General calendar-related functions

## collections — Container datatypes

## collections.abc — Abstract Base Classes for Containers

## heapq — Heap queue algorithm

I have only ever used 2 methods in this module: `nlargest` and `nsmallest`.

```python
import heapq
print(heapq.nlargest(3, [5, 10, 20, 40, 80])) # -> [80, 40, 20]
print(heapq.nsmallest(3, [5, 10, 20, 40, 80])) # -> [5, 10, 20]
```

## bisect — Array bisection algorithm

Python calls this "bisect" or a bisection algorithm, but virtually everywhere else I've seen these functions they've been called ["binary sort functions"](https://en.wikipedia.org/wiki/Binary_search_algorithm).

They allow fast, memory-efficient finding of items in a sorted list. There are 2 main functions: either to the left (`bisect_left`) or right (`bisect_right`) of an item. While there `insort_left` and `insort_right` functions, I've never used these, preferring to batch sort as calling `list.insert()` can be inefficient.

```python
from bisect import bisect_left, bisect_right
print(bisect_left([0, 5, 10, 15], 10)) # -> 2
print(bisect_right([0, 5, 10, 15], 10)) # -> 3
```

## array — Efficient arrays of numeric values

## weakref — Weak references

## types — Dynamic type creation and names for built-in types

## copy — Shallow and deep copy operations

## pprint — Data pretty printer

## reprlib — Alternate repr() implementation

## enum — Support for enumerations

