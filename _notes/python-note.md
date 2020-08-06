---
title: "Python notes"
collection: notes
permalink: /projects/python-note
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

def fun4()
    x=1
    fun3()

fun4() #this will return error since there is no x outside the scope of def fun3()

# Case 3: improper use of default mutable argument
def fun5(i, arg=[]):
    arg.append(i)
    return arg
# In this example, arg will grow everytime you call fun5(i) since the defalut argument is only defined when the function is defined and it is mutable. Following is the correct way.
def fun6(i, arg=None):
    if arg==None:
        arg=[]
    arg.append(i)
    return arg
~~~

9. <b>What does *arg, **kwarg do</b><br/>
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