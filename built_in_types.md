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

It's worth noting that calling `int(0.5)` as a function will round downwards to `0`, while `round(0.5)` will round up to `1`. You can also use the `int` function to convert a string with an integer in it, e.g. `int("5")` will give `5`. This function doesn't like floating point numbers inside strings, so in these cases you'll need to convert to a float beforehand, e.g. `int(float(5.0))` also gives `5`.

<b>Warning:</b> While most of the time you will encounter ordinary python `int`s, some other popular libraries like `numpy` or `pymongo` have their own custom fixed-bit integer/float types which don't behave exactly the same as the builtin ones. These can need special handling when trying to do things like encode them using the `json` module or arithmetic operations, and it's often safer to explicitly coerce them using `int(x)` or `float(x)`. 

## strings/bytes

### strings

Python 3 strings are Unicode, which means they can represent a large majority of the characters in use in the world today. Many programming languages and web browsers only have 2-byte unicode support (UCS-2), which means that characters above ordinal 65535 (such as many emoji) will be represented as two characters. In python 3.3 and up, whether strings take up 1, 2, or 4 bytes per character depends on whether there are characters in your strings which need to use that many bytes. This means for the most part you shouldn't need to worry about this, however note some external libraries could have trouble dealing with these characters.

Python isn't particular about whether you use single quotes (`'my string'`) or double quotes (`"my string"`), although it's best to be consistent. If you want to include a single quote character inside a single-quoted string (or a double quote character inside a double-quoted string), you can use a slash before it: `"\""` or `'\''`. A good alternative if you'd like to use these characters in strings is to use triple quotes (`"""my string"""` or `'''my string'''`), which are known as "string literals". Triple double quotes are often used as "docstrings", which document python code for other people reading your code.

There are three common ways of formatting strings:

* <b>`printf`-style formatting:</b> `"Hello, %s!" % ("World",)`. `%s` (the equivalent of calling `str(o)` on the object) works in many cases, but the full reference is [here](https://docs.python.org/3/library/stdtypes.html#printf-style-string-formatting).
* <b>Formatting using `str.format()`:</b> `"Hello, {}!".format("World")`. See also the [full reference](https://docs.python.org/3/library/stdtypes.html#str.format).
* <b>`f`-string formatting (python expressions):</b> `"Hello, {'World'}!"`

There are lots of [convenient methods](https://docs.python.org/3/library/stdtypes.html#string-methods), too:

* <b>Casing:</b> `capitalize`/`lower`/`swapcase`/`casefold`/`title`
* <b>Join `str` objects in a `list`/`tuple` to make a single `str`:</b> `join`
* <b>Split by characters:</b> `split`/`rsplit`/`splitlines`
* <b>Split by first instance of characters:</b> `partition`/`rpartition`
* <b>Trim characters (often whitespace):</b> `strip`/`lstrip`/`rstrip`
* <b>Get whether the string starts with/ends with characters:</b> `endswith`/`startswith`
* <b>Find/count occurences of characters:</b> `find`/`index`/`rfind`/`rindex`/`count`
* <b>Convert to `bytes` in a given encoding:</b> `encode`
* <b>Padding:</b> `center`/`expandtabs`/`ljust`/`rjust`
* <b>Character translation:</b>: `maketrans`/`translate`
* `isalnum`/`isalpha`/`isascii`/`isdecimal`/`isdigit`/`islower`/`isnumeric`/`isprintable`/`isspace`/`istitle`/`isupper`

You might see different prefix characters such as `b`, `r`, `u` or `f` before strings:

* In python 2, `u""` specified a unicode string, but in python 3 it's ignored, and you safely can too.
* `r""` prefixes are intended for regular expressions, eliminating the need to double-escape backslashes. For example, `r"\b"` is the same as `"\\b"` and will physically contain two characters "\" and "b". 
* `f""` ("format prefixes") allow for embedding any python expression inside them. For instance, `f"Hello {'world'}, I'm {22}!"` will give "Hello world, I'm 22!".
* `b""` "byte prefixes" signify what follows isn't actually a string, but binary byte data. 

### bytes

The `bytes` type stores arbitrary binary data, where each character is a single byte (ordinals from 0 to 255 inclusive for each character), as the name might suggest.

To convert to bytes type from `str`, you can use the `.encode()` method, e.g. `"my data".encode('ascii')` will give binary data encoded as ascii. Similarly `b"my data".decode('ascii')` will decode binary ascii data and give a string. 

(There is also the `bytearray` type which is like a mutable `bytes` type which can be used with `memoryview` for higher performance, but it's best not to prematurely optimize!) 

<b>Warning:</b> `byte` type indexing doesn't behave the same as strings. For example `b"my string"[0]` will give `109` (the ordinal code of "m" as an `int`), while `b"my string"[0:2]` will return a `bytes` object of `b"my"`. Similarly, iterating through a `bytes` type will output integers, e.g. `for i in b"ab": print(i)` will output `97` and `98`. Also note that bytes methods such as `replace` need `bytes`, not string arguments (e.g. `b"my string".replace(b"my", b"your")` will give `b'your string'`.

### tuple/list

Tuples do pretty much the same as lists, except they aren't mutable (you can't change them once you've created them). 

* e.g. `[50, 'my string']` creates a list.
* e.g. `(50, 'my string')`, `50, 'my string'`, `(50,)` or `50,` create tuples. The syntax is ambiguous with the syntax for function arguments, so you must include parenthesis in function calls e.g. `print((50,))` will output `(50,)`. Because a comma at the end of the line will create a tuple and is valid syntax, it's easy to enter e.g. `my_num = 50,` by accident, and this can be a source of bugs.

See also:

* the `array` module for memory-efficient representations of basic (numeric/character) types.
* `ndarray` from the external `numpy` module provides similar functions and is very commonly used, with a focus on linear algebra and math/scientific functions. 

#### list comprehensions

List comprehensions allow compact creating a new list from something that can also be iterated through (that could be another `list`/`tuple`, characters in a `string`, keys in a `dict`, etc). For example, `my_new_list` will be `[0, 1, 3, 4]`:


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

#### slicing lists and tuples

### range

### dict

### 
