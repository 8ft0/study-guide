# HackerRank Python

If you need to access python documentation during your assessment you can use these commands from within the test environment.


You can run these commands in your python 'window'. The output will be displayed in the **Failed Test** section, under `Your Output (stdout)`



## Get list of keywords

```python
help('keywords')
```

```
Here is a list of the Python keywords.  Enter any keyword to get more help.
False               class               from                or
None                continue            global              pass
True                def                 if                  raise
and                 del                 import              return
as                  elif                in                  try
assert              else                is                  while
async               except              lambda              with
await               finally             nonlocal            yield
break               for                 not    
```

## Get list of symbols

```python
help('symbols')
```

```
Here is a list of the punctuation symbols which Python assigns special meaning
to. Enter any symbol to get more help.
!=                  +                   <=                  __
"                   +=                  <>                  `
"""                 ,                   ==                  b"
%                   -                   >                   b'
%=                  -=                  >=                  f"
&                   .                   >>                  f'
&=                  ...                 >>=                 j
'                   /                   @                   r"
'''                 //                  J                   r'
(                   //=                 [                   u"
)                   /=                  \                   u'
*                   :                   ]                   |
**                  <                   ^                   |=
**=                 <<                  ^=                  ~
*=                  <<=                 _    
```
## Get list of topics

```python
help('topics')
```

```
Here is a list of available topics.  Enter any topic name to get more help.
ASSERTION           DELETION            LOOPING             SHIFTING
ASSIGNMENT          DICTIONARIES        MAPPINGMETHODS      SLICINGS
ATTRIBUTEMETHODS    DICTIONARYLITERALS  MAPPINGS            SPECIALATTRIBUTES
ATTRIBUTES          DYNAMICFEATURES     METHODS             SPECIALIDENTIFIERS
AUGMENTEDASSIGNMENT ELLIPSIS            MODULES             SPECIALMETHODS
BASICMETHODS        EXCEPTIONS          NAMESPACES          STRINGMETHODS
BINARY              EXECUTION           NONE                STRINGS
BITWISE             EXPRESSIONS         NUMBERMETHODS       SUBSCRIPTS
BOOLEAN             FLOAT               NUMBERS             TRACEBACKS
CALLABLEMETHODS     FORMATTING          OBJECTS             TRUTHVALUE
CALLS               FRAMEOBJECTS        OPERATORS           TUPLELITERALS
CLASSES             FRAMES              PACKAGES            TUPLES
CODEOBJECTS         FUNCTIONS           POWER               TYPEOBJECTS
COMPARISON          IDENTIFIERS         PRECEDENCE          TYPES
COMPLEX             IMPORTING           PRIVATENAMES        UNARY
CONDITIONAL         INTEGER             RETURNING           UNICODE
CONTEXTMANAGERS     LISTLITERALS        SCOPING             
CONVERSIONS         LISTS               SEQUENCEMETHODS     
DEBUGGING           LITERALS            SEQUENCES   
```

## Help on topic

```python
help('ASSERTION')
```

```
The "assert" statement
**********************
Assert statements are a convenient way to insert debugging assertions
into a program:
   assert_stmt ::= "assert" expression ["," expression]
The simple form, "assert expression", is equivalent to
 
```

## Get list of modules

```python
help('modules')
```

```
Please wait a moment while I gather a list of all available modules...
Crypto              _testinternalcapi   gc                  runpy
Solution            _testmultiphase     genericpath         sched
__future__          _thread             getopt              secrets
__hello__           _threading_local    getpass             select
__phello__          _tkinter            gettext             selectors
...
```

## Help on a class

```python
help(set)
```

```
Help on class str in module builtins:
class str(object)
 |  str(object='') -> str
 |  str(bytes_or_buffer[, encoding[, errors]]) -> str
 |  
 |  Create a new string object from the given object. If encoding or
 |  errors is specified, then the object must expose a data buffer
 |  that will be decoded using the given encoding and error handler.
 |  Otherwise, returns the result of object.__str__() (if defined)
 |  or repr(object).
 |  encoding defaults to sys.getdefaultencoding().
 |  errors defaults to 'strict'.
    ...
```


## Get list of functions
```python
print(dir(str))

```

```
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```

## Function Details
```python
help(str.replace)

```

```
Help on function replace:
replace(self, old, new, count=-1)
    S.replace(old, new[, count]) -> unicode
    
    Return a copy of S with all occurrences of substring
    old replaced by new.  If the optional argument count is
    given, only the first count occurrences are replaced.
```

Certainly! Here are some additional useful Python commands and techniques that can be helpful in various scenarios:

## Get list of built-in functions

```python
help('builtins')
```

```
Help on built-in module builtins:

NAME
    builtins

DESCRIPTION
    Built-in functions, exceptions, and other objects.

BUILT-IN FUNCTIONS
    abs(...)
    all(...)
    any(...)
    ascii(...)
    bin(...)
    bool(...)
    ...
```

## Documentation for a specific built-in function

```python
help(print)
```

```
Help on built-in function print in module builtins:

print(...)
    print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
    
    Prints the values to a stream, or to sys.stdout by default.
    Optional keyword arguments:
    file: a file-like object (stream); defaults to the current sys.stdout.
    sep:  string inserted between values, default a space.
    end:  string appended after the last value, default a newline.
    flush: whether to forcibly flush the stream.
```

## Get list of methods of an object

```python
dir([])
```

```
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```

## Documentation for a specific method of a class

```python
help([].append)
```

```
Help on built-in function append:

append(self, object, /)
    Append object to the end of the list.
```

## Check Python version

```python
import sys
print(sys.version)
```

```
3.8.5 (default, Aug  5 2020, 08:36:46) 
[GCC 7.3.0]
```

## List all attributes and methods of a module

```python
import math
print(dir(math))
```

```
['__doc__', '__loader__', '__name__', '__package__', '__spec__', 'acos', 'acosh', 'asin', 'asinh', 'atan', 'atan2', 'atanh', 'ceil', 'comb', 'copysign', 'cos', 'cosh', 'degrees', 'dist', 'e', 'erf', 'erfc', 'exp', 'expm1', 'fabs', 'factorial', 'floor', 'fmod', 'frexp', 'fsum', 'gamma', 'gcd', 'hypot', 'inf', 'isclose', 'isfinite', 'isinf', 'isnan', 'ldexp', 'lgamma', 'log', 'log10', 'log1p', 'log2', 'modf', 'nan', 'perm', 'pi', 'pow', 'prod', 'radians', 'remainder', 'sin', 'sinh', 'sqrt', 'tan', 'tanh', 'tau', 'trunc']
```

## Documentation for a specific module

```python
help(math)
```

```
Help on built-in module math:

NAME
    math

MODULE REFERENCE
    https://docs.python.org/3.8/library/math.html

    The following documentation is automatically generated from the Python
    source files. It may be incomplete, incorrect or include features that
    are considered implementation detail and may vary between Python
    implementations. When in doubt, consult the module reference at the
    location listed above.

DESCRIPTION
    This module provides access to the mathematical functions
    defined by the C standard.
```

## Search for a specific term in documentation

```python
help('string methods')
```

```
Help on topic string methods:

STRINGS

The str class is used to hold Unicode strings, and provides a variety of methods for working with and manipulating strings.

The methods on str are:

    str.capitalize
    str.casefold
    str.center
    str.count
    str.encode
    str.endswith
    str.expandtabs
    str.find
    str.format
    str.format_map
    str.index
    str.isalnum
    str.isalpha
    str.isdecimal
    str.isdigit
    str.isidentifier
    str.islower
    str.isnumeric
    str.isprintable
    str.isspace
    str.istitle
    str.isupper
    str.join
    str.ljust
    str.lower
    str.lstrip
    str.maketrans
    str.partition
    str.replace
    str.rfind
    str.rindex
    str.rjust
    str.rpartition
    str.rsplit
    str.rstrip
    str.split
    str.splitlines
    str.startswith
    str.strip
    str.swapcase
    str.title
    str.translate
    str.upper
    str.zfill
```

## Use of `pydoc` module

```python
import pydoc
pydoc.render_doc('str')
```

```
Help on class str in module builtins:

class str(object)
 |  str(object='') -> str
 |  str(bytes_or_buffer[, encoding[, errors]]) -> str
 |  
 |  Create a new string object from the given object. If encoding or
 |  errors is specified, then the object must expose a data buffer
 |  that will be decoded using the given encoding and error handler.
 |  Otherwise, returns the result of object.__str__() (if defined)
 |  or repr(object).
 |  encoding defaults to sys.getdefaultencoding().
 |  errors defaults to 'strict'.
    ...
```

These additional commands and techniques will provide comprehensive assistance and documentation within a Python environment, helping with everything from checking available modules and keywords to getting detailed help on functions and classes.