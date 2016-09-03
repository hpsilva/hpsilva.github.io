---
layout: post
title: Regular Expressions
subtitle: Difficult to grasp, but very useful
comments: false
show-avatar: false
published: true
---

**Regular expressions** are a powerful tool to deal with various kinds of string coding challenges.

They are a domain spacific language (DSL) that is present as library in most modern programming languages, not only Python. Regular expressions are quite a popular DSL language example along with the famous SQL for database operations.

Regular exressions or RegEx are usefull for two main tasks:

* Verifying that strings match a pattern, and for instance that a string has the format of an email address i.e.;
* Performing replacements in a string as i.e. fixing spelling issues.


### Python
Regular expressions in Python can be accessed using the `re` module that is part of Python standard library.
After we've defined a regular expression, python `re.match` method ca be used i.e to determine wether it matches at the beginning of a string. If it does, `match` returns an object representing the match, otherwise returns `None`.

To avoid any confusions while working with regular expressions, we would make use of raw strings as `r"expression"`.
Raw strings don't escape anything, which makes use of regular expressions easier.

The next example checks if the pattern 'span' match the string and prints 'Match!' if it does so:

```python
import re

pattern = r'spam'

if re.match(pattern, 'spamspamspam'):
  print('Match!')
else:
  print('No match...')
  
> Match
```

Other functions to match patterns are `re.search` and `re.findall`. The first finds a match of a pattern anywhere in the string, while the second function returns a list of a all substrings that match a pattern, as the next example demonstrate:

``` python
import re

pattern = r'spam'

if re.match(pattern, 'eggspamsausagespam'):
  print('Match!')
else:
  print('No match...')
  
> No match...


if re.search(pattern, 'eggspamsausagespam'):
  print('Match')
else:
  print('No match...')

> Match


print(re.findall(pattern, 'eggspamsausagespam'))

> ['spam', 'spam']
```

In the example above, the `match` function did not match the pattern, as it looks at the beggining of the string only. On the other hand the `search` function found a match in the string.
