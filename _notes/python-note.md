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
 
