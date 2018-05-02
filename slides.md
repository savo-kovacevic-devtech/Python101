---
title: Python 101
separator: ///s
verticalSeparator: ///v
theme: moon
revealOptions:
    transition: 'slide'
---

# Python 101

![logo](img/python_logo.png)

///s


![guido](img/guido.jpg)

Guido van Rossum <!-- .element: class="fragment" -->


///s

## What is python?

* High-level, interpreted programming language
* First appeared in 1991. (Java 1995, C# 2000)


*Also not a snake.*  <!-- .element: class="fragment" -->

///s


## Python is

* Dynamically typed
* Strongly typed

///v

## Dynamically typed?

Python
```python
a = 5
a = "Something"
b = a.length()
```
Java
```java
String a = "Something";
a = 14; // Nope
```

///v

## Strongly typed?

Python
```python
> 5 + "Nope"
>>> Traceback (most recent call last):
>>>   File "<stdin>", line 1, in <module>
>>>TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

JavaScript
```javascript
> 0 + "h God Why?"
>>> "0h God Why?"
```

///s

# Why python?

* Easy to learn <!-- .element: class="fragment" -->
* Clear, concise syntax <!-- .element: class="fragment" -->
* Fast development time <!-- .element: class="fragment" -->
* Huge standard library (batteries included) <!-- .element: class="fragment" -->
* Huge community <!-- .element: class="fragment" -->
* No curly braces <!-- .element: class="fragment" -->

///v

![essay](img/python_java.jpg)

///v

## Rise of Python

> Python has risen in the ranks, surpassing C# this year, much like it surpassed PHP last year. Python has a solid claim to being the fastest-growing major programming language.

[Stack Overflow Survey 2018](https://insights.stackoverflow.com/survey/2018/#most-loved-dreaded-and-wanted)

///s

## What is Python used for?

* Web development (django, flask, tornado) <!-- .element: class="fragment" -->
* Machine learning (tensorflow) <!-- .element: class="fragment" -->
* Science (scipy, numpy, jupyter) <!-- .element: class="fragment" -->
* Big data, data gathering (web scraping) <!-- .element: class="fragment" -->
* Scripting (devops, testing) <!-- .element: class="fragment" -->
* IoT <!-- .element: class="fragment" -->

///s

## Who uses Python?

Splunk, Google, Facebook, Spotify, Reddit, Netflix, Quora, Instagram, NASA, Toyota, Evernote, Nasdaq, Lego, Atlassian, Dropbox, Mozilla, Yahoo...

///s

# But Python is slow!

* Benchmark performance vs real world performance <!-- .element: class="fragment" -->
* Development time <!-- .element: class="fragment" -->

///s

## Instagram

* Written in Python (Django)
* 3B+ registered users
* 800 million monthly active users

///s

# Python interpreters

* **CPython**
* Jython - compiles into Java byte code <!-- .element: class="fragment" -->
* IronPython - .NET Common Language Runtime <!-- .element: class="fragment" -->
* Cython - compiles Python to C and C++  <!-- .element: class="fragment" -->
* Google's Grumpy - compiles Python to Go <!-- .element: class="fragment" -->
* Skulpt - In-browser implementation of Python <!-- .element: class="fragment" -->
* ... <!-- .element: class="fragment" -->

///s

# CPython

///v

```bash
$ python3 app.py
Hello World!
```

*Magic!*

///v

![code_execution](img/python_code_execution.png)

///v

![in_depth_execution](img/in_depth_execution.png)

///v

CPython Compiler Output (for humans)

```bash
$ python3 -m dis app.py 
  1           0 LOAD_NAME                0 (print)
              2 LOAD_CONST               0 ('Hello world!')
              4 CALL_FUNCTION            1
              6 POP_TOP
              8 LOAD_CONST               1 (None)
             10 RETURN_VALUE
```

///v

CPython Interpreter
```c
// ceval.c
main_loop:
    // ...
    for (;;) {
        switch (opcode) {
        TARGET(LOAD_FAST) {
            PyObject *value = GETLOCAL(oparg);
            if (value == NULL) {
                format_exc_check_arg(PyExc_UnboundLocalError,
                                     UNBOUNDLOCAL_ERROR_MSG,
                                     PyTuple_GetItem(co->co_varnames, oparg));
                goto error;
            }
            Py_INCREF(value);
            PUSH(value);
            FAST_DISPATCH();
        }

        PREDICTED(LOAD_CONST);
        TARGET(LOAD_CONST) {
            PyObject *value = GETITEM(consts, oparg);
            Py_INCREF(value);
            PUSH(value);
            FAST_DISPATCH();
        }

        PREDICTED(STORE_FAST);
        TARGET(STORE_FAST) {
            PyObject *value = POP();
            SETLOCAL(oparg, value);
            FAST_DISPATCH();
        }

        TARGET(POP_TOP) {
            PyObject *value = POP();
            Py_DECREF(value);
            FAST_DISPATCH();
        }
// ...
```
///s

## PYTHON2 OR PYTHON3

* Python 2.7 will not be maintained past 2020. <!-- .element: class="fragment" -->

///s

## Now some code

///s

### Variable types

///v

Numeric Types
```python
a = 5  # int
b = 5.0 # float
c = 2-2j # complex
```
///v

Sequence Types

* List
* Tuple (immutable list, kind of)
* Range (immutable sequence of numbers)

///v

```python
a = [1, 2, "Hello"] # List
b = ("World", 3) # Tuple
c = range(3, 9) # Range
```

```python
>>> for i in range(3): 
...     print(i)
0
1
2
```

///v

Common Sequence Operations
```python
x in s
x not in s
s + t # concatenates s and t
s * n # equivalent to adding s to itself n times
s[i]
s[i:j]
len(x)
min(x)
max(x)
s.index("Hello")
s.count("World")
```

///v

Text Sequence Type (str)
```python
a = "Hi"
b = 'Use double quotes "here"'
multiline = '''Henlo
It is me'''
```

* Immutable

///v

Set

```python
a = {1, 2, "Hello"}
a[0] # TypeError: 'set' object does not support indexing
b = {[1, 2], 2, 3} # TypeError: unhashable type: 'list'
```

* Unordered
* Unique

///v

Mapping Type - Dictionary

```python
a = {'one': 1, 'two': 2, 'three': 3}
b = dict(one=1, two=2, three=3)
b['one'] # 1
b['two'] = 6 # {'one': 1, 'two': 6, 'three': 3}
del b['one'] # {'two': 6, 'three': 3}
```

///v

Other Types

* Null Object - `None`
* Boolean Values - `True` / `False`
* And many more

///v

Collections module

* namedtuple
* deque
* Counter
* defaultdict

///s
# Sources

* [StackOverflow survey 2018](https://insights.stackoverflow.com/survey/2018/)
* [Number of instagram users](https://www.statista.com/statistics/253577/number-of-monthly-active-instagram-users/)
* [Instagram at PyCon](https://www.youtube.com/watch?v=66XoCk79kjM)
* [CPython on Github](https://github.com/python/cpython)
* [Python 2.7 EOL countdown](https://pythonclock.org/)
* [Python3 Standard Types](https://docs.python.org/3/library/stdtypes.html)
* [Hashables in Python](https://docs.python.org/3/glossary.html#term-hashable)
* [Collections Module](https://docs.python.org/3/library/collections.html#module-collections)
///s
