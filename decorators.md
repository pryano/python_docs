## Decorators

Decorators provide an easy way to modify functions. An example decorator:
```python
@staticmethod
def my_open_class_method():
  print("I'm Static!")
  return True
```

*_Decorators are run at import time_

#### Simple
For a decorator of the form `@my_decorator`:

```python
from functools import wraps

def my_decorator(func):
  @wraps(func)  # lets the function retain its __doc__
  def wrapper(*args, **kwargs):
    return func(*args, **kwargs)
  return wrapper
```

Example:
```python
@my_decorator
def run(name, distance):
  pass
```

#### Accept Parameters
For a decorator of the form `@my_decorator('param')`:

```python
from functools import wraps

def my_decorator(param):

  def func_wrapper(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
      return func(*args, **kwargs)
    return wrapper
    
  return func_wrapper
```

Example:
```python
@my_decorator('car')
def run(name, distance):
  pass
```
