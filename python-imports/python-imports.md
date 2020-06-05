≈- [Modules](#sec-1)
- [Namespaces](#sec-2)
- [Global Variables](#sec-3)
- [Module Execution](#sec-4)
- [`from module import`](#sec-5)
- [`from module import *`](#sec-6)
- [Commentary](#sec-7)
- [Module Names](#sec-8)
- [Naming Conventions](#sec-9)
- [Module Search Path](#sec-10)
- [Module Cashe](#sec-11)


# Modules<a id="orgheadline1"></a>

-   Any Python source file is a module

```python
# spam.py
def grok(x):
    ...

def blah(x):
    ...
```

-   You use import to execute and access it

```python
a = spam.grok('hello')

from spam import grok
a = grok('hello')
```

# Namespaces<a id="orgheadline2"></a>

-   Each module is its own isolated world

```python
# spam.py

x = 42

def blah():
    print(x)

# eggs.py

x = 37 

def foo():
    print(x)
```

-   These definitions of x are different
-   What happens in Module, stays in a module

# Global Variables<a id="orgheadline3"></a>

-   Global variables bind inside the same module

```python
# spam.py

x = 42

def blah():
    print(X)
```

-   Fuctions record their definition environment

```python
>>> from spam import blah
>>> blah.__module__
'spam'
>>> blah.__globals__
{ 'x': 42, ...}
>>>
```

# Module Execution<a id="orgheadline4"></a>

-   When a module is imported, `all of the statements in the module execute` one after another until the end of the file is reached
-   The contents of the module namespace are of the global names that are still defined at the end of the execution process
-   If there are scripting statements that carry out tasks in the global scope (printing, creating files, etc.), yout will see them run on import

# `from module import`<a id="orgheadline5"></a>

-   Lifts selected symbols out of a module **after importing it** and makes them available locally

```python
from math import sin, cos

def rectangular(r, theta):
    x = r * cos(theta)
    y = r * sin(theta)
    return x, y
```

-   Allows parts of module to be used without having to type the module prefix

# `from module import *`<a id="orgheadline6"></a>

-   Takes **all symbols** from a module and places them into local scope

```python
from math import *

def rectangular(r, theta):
    y = x * cos(theta)
    y = r * sin(theta)
    return x, y
```

-   Sometimes useful
-   Usually considered bad style (try to avoid)

# Commentary<a id="orgheadline7"></a>

-   Variations on import do not change the way that modules work

```python
import math as m
from math import cos, sin
from math import *
...
```

-   import always executes the **entire** file
-   Modules are still isolated environments
-   These variations are just manipulating names

# Module Names<a id="orgheadline8"></a>

-   File names have to follow the rules

```python
# good.py

...

# 2bad.py

...
```

-   Comment: This mistake comes up a lot when teaching Python to newcomers
-   Must be a valid identifier name
-   Also: avoid non-ASCII characters

# Naming Conventions<a id="orgheadline9"></a>

-   It is standard practice for package and module names to be concise and lowercase
-   `foo.py`
-   **not** `MyFooModule.py`

# Module Search Path<a id="orgheadline10"></a>

-   If a file isn&rsquo;t on the path, it won&rsquo;t import

```python
>>> import sys >>> sys.path ['',
      '/usr/local/lib/python34.zip',
      '/usr/local/lib/python3.4',
      '/usr/local/lib/python3.4/plat-darwin',
      '/usr/local/lib/python3.4/lib-dynload',
      '/usr/local/lib/python3.4/site-packages']
```

-   Sometimes you might hack it&#x2026;although doing so feels &ldquo;dirty&rdquo;

```python
import sys
      sys.path.append("/project/foo/myfiles")
```

# Module Cashe<a id="orgheadline11"></a>

-   Modules only get loaded once
-   There&rsquo;s a cache behind the scenes

```python
>>> import spam
>>> import sys
>>> 'spam' in sys.modules
True
>>> sys.modules['spam']
<module 'spam' from 'spam.py'>
```

-   **Consequence:** If you make a change to the source and repeat the import, nothing happens (often furstrating to newcomers)
