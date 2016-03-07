
## TL;DR ##
List comprehension, dictionary comprehension, and generator expression, all with filters
```python
list_comp_results = [num * 2     for num in list_a  if num % 2 == 0]
dict_comp_results = {num: num*2  for num in list_a  if num % 2 == 0}
genrtr_expression = (num * 2     for num in list_a  if num % 2 == 0)
```
The comprehensions will have the format 'result | iteration | filter'. \
The generator expression will have the same format, but returns a generator instead of a set of results.

# Comprehensions #
### List Comprehensions ###
The typical way of creating a new list from an old list:
```python
list_a = [1, 2, 3, 4, 5]
list_b = []
for num in list_a:             # iteration
    list_b.append( num * 2)    # result
```
Can be replaced with a list comprehension:
```python
#         result    iteration
list_b = [num * 2   for num in list_a]
```

This can be done even if tuples are returned from the iterator:
```python
#       result          iteration
temp = [index + val     for index, val in enumerate(list_a)]
>>> [1, 3, 5, 7, 9]
```

### Dictionary Comprehensions ###
A dictionary can be built in-place the same way:
```python
#       result       iteration
temp = {num: num*2   for num in list_a}
```

### Comprehensions may also have filters ###
```python
list_b = []
for num in list_a:              # iteration
    if num % 2 == 0:            # filter
        list_b.append(num * 2)  # result
```
Can be rewritten in the form of a comprehension with a filter:
```python
#         result        iteration            filter
list_b = [num * 2       for num in list_a    if num % 2 == 0]
dict_b = {num: num * 2  for num in list_a    if num % 2 == 0}
```

# Generator Expressions #
The same syntax can be used to make generators in-place:
```python
#        result    iteration          filter
gen_b = (num * 2   for num in list_a  if num % 2 == 0)
```
This creates a generator that can be used in iteration. A Generator looks like this:
```python
# a generator function
def function_a():
    for letter in list_a:
        if letter in 'AEIOU':
            yield letter

generator = function_a()
for a in generator:
    print(a)
```
```python
# generator expression
gen_b = (x**x for x in range(10000))
print(gen_b)
next(gen_b)
```

A Generator Expression can be used in a function that expects an iterable
```python
total = sum(ord(letter) for letter in 'AEIOU')
```

