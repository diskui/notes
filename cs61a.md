
conputer programs consist of instructions to either:
* compute some value
* carry out some actions

statements describe actions, and expressions describe conputations.

> computer = power+ stupid

Don't repeat yourself。

If you find yourself copying and pasting a block of code, you have probably found an opportunity for functional abstraction.

the parent frame of a function depends on the location where the function is **defined** but not called.

to find a key in a dictionary we can use get method:
```python
words = {
"más": "more",
"otro": "other",
"agua": "water"
}

>>> words.get("pavo", "something") #the key we are looking for doesn't exist, we got the second argument
something
```

a key in the dictionary can't be a list or dictionary or any mutable other object, and they have to be distinct, but the value can be any type

immutable types: int, float, string, tuple

mutable types: list, dict

An immutable sequence may still be changable if it contains a mutable value as an element.

the scope rules of python:
![the scope rules of python](https://raw.githubusercontent.com/shelinfff/picpool/main/python_scope_rules.png)

`iter(iterable)` returns an iterator over the elements of an iterable

`next(iterator)` returns the next element in an iterator.

```python
toppings = ["pineapple", "pepper", "mushroom", "roasted red pepper"]

topperator = iter(toppings)
next(iter) # 'pineapple'
next(iter) # 'pepper'
next(iter) # 'mushroom'
next(iter) # 'roasted red pepper'
next(iter) # ❌ StopIteration exception
```

Calling iter() on an iterator just returns the iterator

inheritance is best for representing "is-a" relationship, and composition(one has references to other objects) is best for representing "has-a" relationship