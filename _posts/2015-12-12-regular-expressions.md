---
layout: post
title: Regular Expressions
subtitle: Difficult to grasp, but very useful
comments: false
show-avatar: true
---

**Regular expressions** are a powerful tool to deal with various kinds of string coding challenges.

They are a domain spacific language (DSL) that is present as library in most modern programming languages, not only Python. Regular expressions are quite a popular DSL language example along with the famous SQL for database operations. Private DSL languages are often used for specific industrial purposes.

As for regular exressions or RegEx, they are usefull for two main tasks:
* Verifying that strings match a pattern, and for instance that a string has the format of an email address i.e.;
* Performing replacements in a string as i.e. fixing spelling issues.


###python
Regular expressions in Python can be access using the `re` module that is part of Python standard library.
After we've defined a regular expression, python `re.match` method ca be used i.e to determine wether it matches at the beginning of a string. If it does, `match` returns an object representing the match, otherwise returns `None`.

To avoid any confusions while working with regular expressions, we would make use of raw strings as r"expression".
Raw strings don't escape anything, which makes use of regular expressions easier.

The next example checks if the pattern 'span' match the string and prints 'Match!' if it does:
```python
import re

pattern = r'spam'

if re.match(pattern, 'spamspamspam'):
  print('Match!')
else:
  print('No match...')
  
> Match
```
