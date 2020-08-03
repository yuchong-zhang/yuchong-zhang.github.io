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
  There are different approaches, using modules such as time, datetime, timeit. Follow is one of the approaches.
~~~ python
import timeit
start = timeit.default_timer()
#Your statements here
stop = timeit.default_timer()
print('Time: ', stop - start)
~~~

  7. <b>What is the benefit of using generator? How to use it? </b><br/>
  Save memory and time. Fetch value only when needed.
~~~ python
def function_name(nums):
    for i in nums:
        yield i*i
generator=function_name(nums)
# or using list comprehension
generator=(i*i for i in nums)
~~~
