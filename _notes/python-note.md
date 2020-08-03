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
  3. <b>What is the trick of unpacking</b><br/>
  Use underscore(\_) for unneeded values and use asterisk(\*) for multiple values.

  4. <b>What does 'python -m xx' do</b><br/>
  Call module/script 'xx' from sys.path. Following 'xx' one can provide arguments for this module/script.

  5. <b>How to create different variable names while in a loop?
  Use a dict or list. Not a good idea to use exec/global().
