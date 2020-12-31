---
title: "Python notes"
collection: notes
permalink: /notebook/python-note
---
1. <b>How to check the version and path of python?</b><br/>
    ~~~ python
    import sys
    print(sys.version) #python version
    print(sys.executable) #python path
    ~~~

2. <b>How to speed up calculations which cannot avoid using 'for' loop?</b><br/>
    Numba may be a good option. 
    ~~~ python
    from numba import jit
    @jit(nopython=True)
    def my_function(): #expect to take numpy arrays as arguments
    ~~~

3. <b>Trick of unpacking</b><br/>
    Use underscore (\_) for unneeded values and use asterisk (\*) for multiple values.

4. <b>What does 'python -m xx' do?</b><br/>
    Call module/script 'xx' from sys.path. Following 'xx' one can provide arguments for this module/script.

5. <b>How to create different variable names while in a loop?</b><br/>
    Use a dict or list. Not a good idea to use exec/globals().
  
6. <b>Time running time in python</b><br/>
    There are different approaches, using modules such as time, datetime, timeit. Following is one of the approaches.
    ~~~ python
    import timeit
    start = timeit.default_timer()
    #Your statements here
    stop = timeit.default_timer()
    print('Time: ', stop - start)
    ~~~

7. <b>What is the benefit of using generator? How to use it?</b><br/>
Save memory and time. Fetch value only when needed.
    ~~~ python
    def function_name(nums):
        for i in nums:
            yield i*i
    generator=function_name(nums)
    # or using list comprehension
    generator=(i*i for i in nums)
    ~~~

8. <b>What is the LEGB rule in terms of scope? Some common mistakes when working with functions.</b><br/>
    LEGB stands for Local, Enclosing, Global, Builtin, which determines the order in which Python looks up names. Following are some common mistakes.
    ~~~ python
    # Case 1: reference before assignment
    x=1
    def fun1():
      x=x
      print(x)
    # fun1 is wrong since x is considered as local variable because of assignment statement. fun2 works.
    def fun2():
      print(x)
    # Case 2: nexted definition != nested function call
    def fun3():
      print(x)
    def fun4():
      x=1
      fun3()
    fun4() #this will return error since there is no x outside the scope of def fun3()
    # Case 3: improper use of default mutable argument
    def fun5(i, arg=[]):
      arg.append(i)
      return arg
    # In this example, arg will grow everytime you call fun5(i) since the defalut argument is only defined when the    function is defined and it is mutable. Following is the correct way.
    def fun6(i, arg=None):
      if arg==None:
        arg=[]
      arg.append(i)
      return arg
    ~~~

9. <b>What does *arg, **kwarg do?</b><br/>
    When defined in functions, *arg and **kwarg allow a vairable number of arguments and a variable number of key-value pairs to pass to a function. When used in calling a function, * and ** unpack a tuple and a dictionary, respectively.

10. <b>How to set path?</b><br/>
    Hardcoding is not good. Following are two potential ways.
    ~~~ python
    #using os.path
    import os.path
    folder_ = os.path.join("folderA", "folderB")
    file_ = os.path.join(folder_, "fileC")
    #using pathlib
    from pathlib import Path
    folder_ = Path("folderA/folderB/")
    file_ = folder_/"fileC"
    ~~~

11. <b>How to import modules not in current directory?</b><br/>
    One way is to add module path to sys.path and the other way is to add PYTHONPATH to system variable.

12. <b>When to use 'is', 'is not' and when to use '==', '!='</b><br/>
    When comparing the values of two objects, using <code>==</code> and <code>!=</code>. When comparing whether two variables refer to the same object in memory, use <code>is</code> and <code>is not</code>. The main use for <code>is</code> and <code>is not</code> is to compare with <code>None</code>, which is interned at a specific address. Other objects that are interned by default are <code>True</code>, <code>False</code>, small integers and simple strings.

13. <b>Why does max() sometimes return nan and sometimes ignores it?</b><br/>
    The reason is that <code>max()</code> works by taking the first value as the "max seen so far", and then checking each other value to see if it is bigger than the "max seen so far". But <code>nan</code> is defined so that comparisons with it always return <code>False</code>. Max methods from different modules behave differently, so be careful.

14. <b>What is the difference between iterable, iterator and generator?</b><br/>
    Iterator is a subclass of iterable, and generator is a subclass of iterator. Iterable has <code>__iter__</code> method and iterator/generator has <code>__next__</code> method.

15. <b>Syntax of decorator</b><br/>
    ~~~ python
    #using function decorator
    def decorator_function(original_function):
        def wrapper_function(*args, **kwargs):
            print('wrapper executed this before {}'.format(original_dunction.__name__))
            return original_function(*args, **kwargs)
        return wrapper_function
    #then use one of the two
    def original_function():
        pass
    original_function=decorator_function(original_function)

    @decorator_function
    def original_function():
        pass
    #using class decorator
    class decorator_class(object):
        def __init__(self, original_function):
            self.original_function = original_function
        def __call__(self, *args, **kwargs):
            print('call method before {}'.format(self.original_function.__name__))
            self.original_function(*args, **kwargs)
    #then use one of the two
    def original_function():
        pass
    original_function=decorator_class(original_function)

    @decorator_class
    def original_function():
        pass
    ~~~

16. <b>How to customize comparison in sorted() or list.sort()</b><br/>
    ~~~ python
    #to customize objects to compare, use function(such as lambda) or operator module (examples below)
    from operator import itemgetter, attrgetter
        sorted(tuple_to_sort, key=itemgetter(2))
        sorted(object_to_sort, key=attrgetter('name'))
    #to change 1-to-1 comparison rules, either define the rules in a class (either define a class by building from scratch or decorating a function).
    class reverse_numeric_class:
        def __init__(self, obj):
            self.obj=obj
        def __lt__(self, other):
            return self.obj>other.obj
    sorted(nums, key=reverse_numeric_class)
    
    from functools import cmp_to_key
    @cmp_to_key
    def reverse_numeric_function(x, y):
        return y - x
    sorted(nums, key=reverse_numeric_function)
    ~~~

16. <b>Utilities from functools package</b><br/>
    ~~~ python
    #reduce
    from functools import reduce #reduce(function, iterable[, initializer])
    d={"a":{"b":{"c":4}}}
    l=["a","b","c"]
    from operator import getitem #getitem(x,y)->x[y]
    reduce(getitem, l, d) #return 4
    #lru_cache
    from functools import lru_cache
    @lru_cache(None) #memorization
    def my_function():
    ~~~
