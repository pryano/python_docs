# Python params #

### Default param ###
Default parameters can be specified with = syntax:
```python

def print_params(a, b, c=4):
    print('{}:{}:{}'.format(a,b,c))

print_params(1,2,3)
print_params(1,2)
```


### Required key param ###
Use the unnamed tuple catchall shortcut to enable required keywords.
Anything following a * is a required keyword unless it has a default value:
```python

def print_params(a, *, b, c=False):
    print('{}:{}'.format(a,b))

print_params(1, b=2)
```

    
### Catchall param ###
To catch all parameters into a tuple, use the * syntax:
```python

def print_params(*b):
    for i in b:
        print(i)
    
print_params(1,2,3,4)
```


### Catchall key params ###
To catch all of the keyword params, use the dict unpacking syntax **:
```python

def print_params(**keys):
    for k,v in keys.items():
        print('{}={}'.format(k,v))
    
print_params(**dict(a=1,b=2,c=3))
print_params(a=1,b=2,c=3)
```

### Gotchas ###
Don't use mutable types as default values, they will keep the state between calls:
```python

def print_params(informations={}):
    test = informations
    print(informations)
    test['empty'] = 0

>>>print_params()
{}
>>>print_params()
{'empty': 0} 
```

Instead use None:
```python

def print_params(informations=None):
    if informations is None:
        test = {}
    else:
        test = informations
    print(informations)
    test['empty'] = 0

>>>print_params()
None
>>>print_params()
None
```
