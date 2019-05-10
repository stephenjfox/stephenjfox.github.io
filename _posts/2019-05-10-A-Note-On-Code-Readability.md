---
title: "A Note on Code Readability"
date: 2019-05-10T18:28:30-04:00
categories:
  - blog
  - python
tags:
  - update
---

You'll find this post in the `_posts` directory.

## If you had a choice

Given some utility function:

```python
def is_even(x: int): return x % 2 == 0
```

and usage 

```python
quantify(range(50), is_even) # => 25
```


Which of the following would you like to stumble across in the codebase?


Exhibit A:

```python
def quantify(iterable, predicate=bool) -> int:
    "Count the number of items in iterable for which the predicate is true."
    return sum(map(predicate, iterable))
```

Exhibit B:

```python
def quantify(iterable, predicate=bool) -> int:
    "Count the number of items in iterable for which the predicate is true."
    return sum((predicate(x) for x in iterable))
```

---

## Why it matters

I stumbled across Exhibit A in one of [Peter Norvig's pytudes][] (which he says he got from the [itertools docs][])
and thought
> but that can be done with implicit generator syntax. Why call `map`?

As Norvig's pytudes are a something of a high watermark (actually _quality_ code) in published, **free** Python resources,
  I wonder why he and I thought differently.

Still haven't reached an answer, but thought I would put it out there...


[Peter Norvig's pytudes]: https://github.com/norvig/pytudes/blob/master/ipynb/How%20To%20Count%20Things.ipynb
[itertools docs]: https://docs.python.org/3/library/itertools.html
