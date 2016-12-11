# python-observations

## Method look-up overhaed

Based on https://docs.python.org/release/2.6.6/faq/programming.html#my-program-is-too-slow-how-do-i-speed-it-up
**Python 2**
```
$ ipython
Python 2.7.12 (default, Sep 11 2016, 21:48:40) 
Type "copyright", "credits" or "license" for more information.

In [21]: from timeit import timeit

In [22]: setup1 = "a = {1: 'a'}"

In [23]: setup2 = """\
    ...: a = {1: 'a'}
    ...: a_get = a.get"""

In [24]: stmt1 = """\
    ...: for i in range(1000000):
    ...:     a.get(1, 0)
    ...: """

In [25]: stmt2 = """\
    ...: for i in range(1000000):
    ...:     a_get(1, 0)
    ...: """

In [26]: timeit(stmt1, setup1, number=1000)
Out[26]: 125.40199017524719

In [27]: timeit(stmt2, setup2, number=1000)
Out[27]: 87.49684882164001
```
**Python 3**
```
$ ipython3
Python 3.4.5 (default, Sep 11 2016, 21:45:49) 
Type "copyright", "credits" or "license" for more information.

In [1]: setup1 = "a = {1: 'a'}"

In [2]: setup2 = """\
   ...: a = {1: 'a'}
   ...: a_get = a.get"""

In [3]: stmt1 = """\
   ...: for i in range(1000000):
   ...:     a.get(1, 0)
   ...: """

In [4]: stmt2 = """\
   ...: for i in range(1000000):
   ...:     a_get(1, 0)
   ...: """

In [6]: from timeit import timeit

In [7]: timeit(stmt1, setup1, number=1000)
Out[7]: 121.0638571190002

In [8]: timeit(stmt2, setup2, number=1000)
Out[8]: 85.85463693700058
```

