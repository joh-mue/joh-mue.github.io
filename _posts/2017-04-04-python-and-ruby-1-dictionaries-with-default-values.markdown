---
title: Python and Ruby Ep.1 - Dictionaries with default values
layout: post
tags: pythonvruby, python, ruby
---

For some work that I doing at the moment I was forced (read: enticed) to learn and use python which is overall quite similar to ruby but obviously the two have different ways to go about things.


In Python 2.7 you have to import defaultdict first and instantiate a default dict with with a data type. Python then pics the default value of that type. Somehow.

```python
> score = {}  # or dict() for long
{}
> score["hans"]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'hans'
> from  collections import defaultdict

> score = defaultdict(int)
> score
defaultdict(<type 'int'>, {'dirk': 0})
> score["dirk"]
0
```

The same thing in Ruby. Just add the default value.

```ruby
> dict = {} # or 'Hash.new()' for long
=> {}
> dict[:dirk]
=> nil
> dict = Hash.new(0)
=> {}
> dict[:dirk]
=> 0
> dict[:alex] += 1
=> 1
```
