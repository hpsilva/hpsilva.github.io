---
layout: post
title: Regular Expressions
subtitle: Difficult to grasp, but very useful
comments: false
show-avatar: false
published: true
---

<a href='https://en.wikipedia.org/wiki/Regular_expression'>**Regular expressions**</a> are a powerful tool to deal with various kinds of string coding challenges.

They are a domain spacific language (DSL) that is present as library in most modern programming languages, not only exclusive to Python. Actually regular expressions are quite a popular DSL language example along with famous others like SQL for database operations.

According to Python `re` documents we have that:

> Regular expressions are essentially a tiny, highly specialized programming language embedded inside Python and made available through the re module. 
Using this little language, you specify the rules for the set of possible strings that you want to match; this set might contain English sentences, or e-mail addresses, or TeX commands, or anything you like. 
You can then ask questions such as “Does this string match the pattern?”, or “Is there a match for the pattern anywhere in this string?”. 
You can also use REs to modify a string or to split it apart in various ways.


### Python re library
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

### Search and Findall

Other tools available on the `re` library to match patterns are `re.search` and `re.findall`. The first finds a match of a pattern anywhere in the string, while the second function returns a list of a all substrings that match a pattern, as the next example demonstrate:

``` python
import re

pattern = r'spam'

if re.match(pattern, 'eggspamsausagespam'):
  print('Match!')
else:
  print('No match...')
  
> No match...


if re.search(pattern, 'eggspamsausagespam'):
  print('Match!')
else:
  print('No match...')

> Match!


print(re.findall(pattern, 'eggspamsausagespam'))

> ['spam', 'spam']
```

In the example above, the `match` function did not match the pattern, as it looks at the beggining of the string only. On the other hand the `search` function found a match in the string.

### Other search methods

RegEx search returns an object with several methods that give details about it. This methods include `group` that returns the string matched, `start` and `end` that return the start and end positions of the match, and `span`that returns the start and end position as a tuple. Let´s see in the example below:

```python
import re

pattern = r'spam'

match = re.search(pattern, 'eggspamsausage')
if match:
  print(match.group())
  print(match.start())
  print(match.end())
  print(match.span())
  

> pam
> 4 
> 7
> (4, 7)
```


### Search & Replace

One of the most import `re`methods that use regular expressions is the `sub`.

This method replaces all occurences of the **pattern** in the string making use of repl thus substituting all occurences unless **max** limit is provided. This method returns the modified string.

```python
import re

str = 'My name is David. Hi David.'
pattern = r'David'
newstr = re.sub(pattern, 'Amy', str)
print(newstr)

> My name is Amy. Hi Amy.
```

Regular expressions are a deep topic, and in this thread we barely scratched the surface of its abilities. For your further reference i recommend you having a go at the <a href='https://docs.python.org/2/library/re.html'>Python re library</a>!


#### Sources:

* <a href='https://docs.python.org/2/library/re.html'>Regular Expression Operations</a>
* <a href='https://docs.python.org/2/howto/regex.html#regex-howto'>Regular Expressions HOW TO</a>
