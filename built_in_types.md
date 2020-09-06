# Built-in Types

Python is duck-typed, which means if it looks like an integer (e.g. `x = 50`), a floating point number (`x = 1.5`), a string (`s = "my string"` or `s = 'my string'`)..then that's what it will be. Below is a quick example of creating the most common python types:

```python
my_int = 15
my_float = 5.5
my_string = "foo"
my_list = [55, 2, "my string"]
my_dict = {
    "string key": "string value", 
    2: 50
}
my_set = set([55, 25, 2])
```

## int/float

In python 3, `1 / 2` becomes `0.5` turning into a `float`, but you can get the same behavior as python 2 by using the `//` operator, e.g. `1 // 2` also becomes `0`.

Unlike python 2, python 3 has just a single `int` type. Python 3 ints have variable numbers of bits, and can represent numbers of any size. 

It's worth noting that calling `int(0.5)` as a function will round downwards to `0`, while `round(0.5)` will round up to `1`. You can also use the `int` function to convert a string with an integer in it, e.g. `int("5")` will give `5`. This function doesn't like floating point numbers inside strings, so in these cases you'll need to convert to a float beforehand, e.g. `int(float("5.0"))` also gives `5`.

<b>Warning:</b> While most of the time you will encounter ordinary python `int`s, some other popular libraries like `numpy` or `pymongo` have their own custom fixed-bit integer/float types which don't behave exactly the same as the builtin ones. These can need special handling when trying to do things like encode them using the `json` module or arithmetic operations, and it's often safer to explicitly coerce them using `int(x)` or `float(x)`. 

## str/bytes

### str

Python 3 strings (the `str` type) are Unicode, which means they can represent a large majority of the characters in use in the world today. Many programming languages and web browsers only have 2-byte unicode support (UCS-2), which means that characters above ordinal 65535 (such as many emoji e.g. this lion: 🦁) will be represented as two characters. In python 3.3 and up, whether strings take up 1, 2, or 4 bytes per character depends on whether there are characters in your strings which need to use that many bytes. This means for the most part you shouldn't need to worry about this, however note some external libraries could have trouble dealing with these characters.

Python isn't particular about whether you use single quotes (`'my string'`) or double quotes (`"my string"`), although it's best to be consistent. If you want to include a single quote character inside a single-quoted string (or a double quote character inside a double-quoted string), you can use a slash before it: `"\""` or `'\''`. A good alternative if you'd like to use these characters in strings is to use triple quotes (`"""my string"""` or `'''my string'''`), which are known as "string literals". Triple double quotes are often used as "docstrings", which document python code for other people reading your code. See also [how to write docstrings for sphinx](https://sphinx-rtd-tutorial.readthedocs.io/en/latest/docstrings.html), which is commonly used to generate documentation for python code.

There are three common ways of formatting strings:

* <b>`printf`-style formatting:</b> `"Hello, %s!" % ("World",)`. `%s` (the equivalent of calling `str(o)` on the object) works in many cases, but the full reference is [here](https://docs.python.org/3/library/stdtypes.html#printf-style-string-formatting).
* <b>Formatting using `str.format()`:</b> `"Hello, {}!".format("World")`. See also the [full reference](https://docs.python.org/3/library/stdtypes.html#str.format).
* <b>`f`-string formatting (python expressions):</b> `f"Hello, {'World'}!"`

There are lots of [convenient methods](https://docs.python.org/3/library/stdtypes.html#string-methods), too:

* <b>Casing:</b> `lower`/`upper`/`capitalize`/`title`/`swapcase`/`casefold`
* <b>Join `str` objects in a `list`/`tuple` to make a single `str`:</b> `join`
* <b>Split by characters to create a `list`:</b> `split`/`rsplit`/`splitlines`
* <b>Split by first instance of characters</b> (to create a list of `[before delimiter, delimiter, after delimiter]`:) `partition`/`rpartition`
* <b>Trim characters (often whitespace):</b> `strip`/`lstrip`/`rstrip`
* <b>Get whether the string starts/ends with characters:</b> `endswith`/`startswith`
* <b>Find/count occurrences of characters:</b> `find`/`index`/`rfind`/`rindex`/`count`
* <b>Convert to `bytes` in a given encoding:</b> `encode`
* <b>Padding:</b> `center`/`expandtabs`/`ljust`/`rjust`
* <b>Character translation:</b>: `maketrans`/`translate`
* <b>Numeric tests:</b> `isdecimal`/`isdigit`/`isnumeric`
* <b>Alphabetic tests:</b> `islower`/`isupper`/`istitle`/`isalpha`
* <b>Miscellaneous tests:</b> `isalnum`/`isascii`/`isprintable`/`isspace`

You might see different prefix characters such as `b`, `r`, `u` or `f` before strings:

* In python 2, `u""` specified a unicode string, but in python 3 it's ignored, and you safely can too.
* `r""` prefixes are intended for regular expressions, eliminating the need to double-escape backslashes. For example, `r"\b"` is the same as `"\\b"` and will physically contain two characters "\\" and "b". 
* `f""` ("format prefixes") allow for embedding any python expression inside them. For instance, `f"Hello {'world'}, I'm {22}!"` will give "Hello world, I'm 22!".
* `b""` "byte prefixes" signify what follows isn't actually a string, but binary byte data. 

### bytes

The `bytes` type stores arbitrary binary data, where each character is a single byte (ordinals from 0 to 255 inclusive for each character), as the name might suggest.

To convert to bytes type from `str`, you can use the `.encode()` method, e.g. `"my data".encode('ascii')` will give binary data encoded as ascii. Similarly `b"my data".decode('ascii')` will decode binary ascii data and give a string. 

(There is also the `bytearray` type which is like a mutable `bytes` type which can be used with `memoryview` for higher performance, but it's best not to prematurely optimize!) 

<b>Warning:</b> `byte` type indexing doesn't behave the same as strings. For example `b"my string"[0]` will give `109` (the ordinal code of "m" as an `int`), while `b"my string"[0:2]` will return a `bytes` object of `b"my"`. Similarly, iterating through a `bytes` type will output integers, e.g. `for i in b"ab": print(i)` will output `97` and `98`. Also note that bytes methods such as `replace` need `bytes`, not string arguments (e.g. `b"my bytes".replace(b"my", b"your")` will give `b'your bytes'`.

## tuple/list

### lists

Lists are ordered collections of items that can be updated/added to in-place, e.g:

```python
my_list = [1, 2, 3]
my_list.insert(1, 5) # Insert 5 before 2 and after 1
print(my_list) # -> [1, 5, 2, 3]

my_list = [1, 2, 3]
my_list.append(6) # Append 6 to the end of the list
print(my_list) # -> [1, 2, 3, 6]
```

Note that the `*` operator can allow for lists to be used as positional arguments, meaning that `print(*["foo", "bar"])` will output "foo bar" rather than `["foo", "bar"]` as it is equivalent to calling `print("foo", "bar")`.

<b>Warning:</b> It's not a good idea to have a `list` as a default function parameter, as any changes will be persistent across function calls. For example:

```python
def my_function(default_param=["foo"]):
    print(default_param)
    default_param.append("bar")

my_function() # -> ["foo"]
my_function() # -> ["foo", "bar"]
```

Lookup times for `"foo" in my_list` or similar operations can also very slow if there are many elements, as python will need to go through every item until it finds the one you've asked it to find. dicts and sets are a much faster alternative in these cases, as only a single operation is needed. Appending to the end of lists is very fast, but inserting at the start of lists can also be slow if there are many elements.

### tuples

Tuples do pretty much the same as lists, except they aren't mutable (you can't change them once you've created them). All of the following create tuples:

```python
tuple_1 = (50, "my string")
tuple_2 = 50, "my string"
tuple_3 = (50,)
tuple_4 = 50,
```

The syntax is ambiguous with the syntax for function arguments, so you must include parenthesis in function calls e.g. `print((50,))` will output `(50,)`. Because a comma at the end of the line will create a tuple and is valid syntax, it's easy to enter e.g. `my_num = 50,` by accident, and this can be a source of bugs.

### slicing lists and tuples

The syntax `list[start:stop:step]` (where `stop:step` are optional) allow creating a new `list`/`tuple` from ranges of elements. For example:

```python
my_list = [0, 1, 2, 3, 4]

# Basic (non-slice) notation
my_list[0] # -> 0
my_list[-1] # -> 4

# Slice notation
my_list[::-1] # -> [4, 3, 2, 1, 0]
my_list[::2] # -> [0, 2, 4]
my_list[1:3] # [1, 2]
my_list[1:] # [1, 2, 3, 4]
my_list[:-1] # [0, 1, 2, 3]
```

Note that `ndarray` from `numpy` (and similar types from various machine learning libraries) behave quite differently from python built-in types when slicing, and are closer to notations used for linear algebra. See also https://numpy.org/doc/stable/reference/arrays.indexing.html.

### list comprehensions

List comprehensions allow compact creation of a new list from something that can also be iterated through. The other iterable object could be another `list`/`tuple`, characters in a string, keys in a `dict`, etc). For example, `my_new_list` will be `[0, 1, 3, 4]`:

```python
my_list = [0, 1, 2, 3, 4]
my_new_list = [i for i in my_list if i != 2]
```

This is exactly the same as the below code, only shorter (and I think more readable):

```python
my_list = [0, 1, 2, 3, 4]

my_new_list = []
for i in my_list:
    if i != 2:
        my_new_list.append(i)
```

### See also:

* the `array` module for memory-efficient representations of basic (numeric/character) types.
* `ndarray` from the external `numpy` module provides similar functions and is very commonly used, with a focus on linear algebra and math/scientific functions. 

## range

The python `range` type allows lazy iteration through a sequence of numbers, in a similar way to the list slice notation (it is called with either `range(stop)` or `range(start, stop, step)`). This basically means that even if you go `range(9999999999)`, it will happen immediately as the numbers are generated on-demand. Usage example:

```python

for i in range(5):
    print(i, end=" ") 
# -> 0, 1, 2, 3, 4. Note that 5 is never reached.

for i in range(1, 8, 3):
    print(i, end=" ")
# -> 1, 4, 7

for i in range(5, 0, -1):
    print(i, end=" ")
# -> 5, 4, 3, 2, 1
```

## dict

The `dict` type is similar to hash tables or hashmaps in other languages, and allows getting items by keys. They can be created using either literal syntax: `{key: value}` or function syntax: `dict(key=value)`. Note that the `**` operator can allow for dicts to be used as keyword arguments, meaning that `dict(**{"foo": "bar"})` will return the dict `{"foo": "bar"}`.

While it was not previously the case, note that from python 3.6 the `dict` type is ordered, which means that you can iterate through the keys in the order you assign them. Note that tuples can be used as keys, but that lists can't. As lists, dicts and sets are mutable, they could change in between of when they are assigned and when they are accessed, so this is not allowed. 

As values in dicts are accessed by hash, it is very fast to both check whether a value is in a dict and to retrieve a value. 

```python
my_int = 15
my_float = 5.5
my_string = "foo"
my_bytes = b"bar"
my_tuple = (55, 2, "my string")
my_list = [55, 2, "my string"]
my_set = set([55, 25, 2])

my_dict = {}
my_dict[my_int] = 0 # -> OK
my_dict[my_float] = 1 # -> OK
my_dict[my_string] = 2 # -> OK
my_dict[my_bytes] = 3 # -> OK
my_dict[my_tuple] = 4 # -> OK

my_dict[my_list] = 5 # -> error
my_dict[my_dict] = 6 # -> error
my_dict[my_set] = 7 # -> error

my_string in my_dict # -> True
"bar" in my_dict # -> False

for key, value in my_dict.items():
    print(key, value)
# -> 15 0
#    5.5 1
#    foo 2
#    b'bar' 3
#    (55, 2, 'my string') 4

for key in my_dict:
    print(key, my_dict[key])
# -> 15 0
#    5.5 1
#    foo 2
#    b'bar' 3
#    (55, 2, 'my string') 4

for value in my_dict.values():
    print(value)
# -> 0
#    1
#    2
#    3
#    4
```

<b>Warning:</b> Similar to lists, it's not a good idea to have a dict as a default function parameter, as any changes will also be persistent. For example:

```python
def my_function(default_param={"foo": "bar"}):
    print(default_param)
    default_param["foo"] = "foo"

my_function() # -> {"foo": "bar"}
my_function() # -> {"foo": "foo"}
```

dicts also initially use more memory than lists, although this is not likely to be a problem unless you create tens of thousands of them.

The methods `{}.get(key, default)`, `{}.setdefault(key, default)` are commonly used to reduce code length:

```python
food_types = {
    "candy cane": "confectionary",
    "chocolate": "confectionary",
    "carrot": "vegetable"
}
print(food_types.get("candy cane", "unknown")) # -> "confectionary"
print(food_types.get("rocky road", "unknown")) # -> "unknown"

foods_by_type = {}
foods_by_type.setdefault("confectionary", []).append("candy cane")
foods_by_type.setdefault("confectionary", []).append("chocolate")
foods_by_type.setdefault("vegetable", []).append("carrot")
print(foods_by_type["confectionary"]) # -> ["candy cane", "chocolate"]
```

The `my_dict.update(other_dict)` method also adds keys from the `other_dict` into `my_dict` only if the key wasn't already present in `my_dict`.

## set

Sets are like dicts with only keys. They are useful for identity tests, and asking whether something exists in a collection of objects. For example:

```python
my_set = set(["a"])
my_set.add("b")

"a" in my_set # -> True
"b" in my_set # -> True
"c" in my_set # -> False
```

Every item in a set is unique, which is a useful property when you want to remove duplicates. `sorted(set([0, 1, 1, 2, 3, 3, 4]))` gives `[0, 1, 2, 3, 4]`, for instance.
