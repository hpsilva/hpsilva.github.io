---
layout: post
title: (i)Regular Expressions
subtitle: Difficult to grasp, but very useful - take 2
comments: false
show-avatar: false
published: true
---

If you got thru my last article about <a href='http://hpsilva.io/2015-12-12-regular-expressions/'>RegEx</a>, you might got wondering on why i have addressed to regular expressions as 'difficult to grasp'.
Well, the reason being that on the previous article we essentially covered the <a href='https://docs.python.org/2/library/re.html'>tool</a> Python provides on its standard library to deal with RegEx, however the examples covered were just introductory.

If you are curious about the power of what can get done with RegEx, just bear with me a bit more as i'll provide few more information this time around focusing on regEx patterns.

To start with it should be remarked that there are various characters which would have special meaning for `Python` when they are used in regular expressions. 
To avoid conflicting situations while dealing with regEx in Python, we shall then make use of **raw strings** instead as `r'expression'`.

### # RegEx Patterns

|Modifier|Description|
|:-|:-|
|re.I|Case-insensitive matching|
|re.L|Interprets words according to the current locale. This interpretation affects the alphabetic group (\w and \W), as well as word boundary behavior (\b and \B)|
|re.M|Makes $ match the end of a line (not just the end of the string) and makes ^ match the start of any line (not just the start of the string)|
|re.S|Makes a period (dot) match any character, including a newline|
|re.U|Interprets letters according to the Unicode character set. This flag affects the behavior of \w, \W, \b, \B|
|re.X|Permits "cuter" regular expression syntax. It ignores whitespace (except inside a set [] or when escaped by a backslash) and treats unescaped # as a comment marker|

### # RegEx Modifiers
Except for control characters `(+ ? . * ^ $ ( ) [ ] { } | \)` all other characters match themselves. Control characters can be escaped by preceding it with a backslash `\`.

Following table presents regular expression syntax available in Python:

|Pattern|Description|
|:-|:-|
|^|Match beginning of line|
|$|Match end of line|
|.|Match any single character except newline|
|[...]|Match any single character inside the brackets|
|[^...]|Match any single character not inside the brackets|
|re*|Match 0 or more occurrences of preceding expression|
|re+|Match 1 or more occurrence of preceding expression|
|re?|Match 0 or 1 occurrence of preceding expression|
|re{ n}|Match exactly n number of occurrences of preceding expression|
|re{ n,}|Match n or more occurrences of preceding expression|
|re{ n, m}|Match at least n and at most m occurrences of preceding expression|
|a \| b|Match either a or b|
|(re)	|Group regular expressions and remembers matched text|
|(?imx)|Temporarily toggle on i, m, or x options within a regular expression. When inside parentheses, only that area is affected|
|(?-imx)|Temporarily toggle off i, m, or x options within a regular expression. When inside parentheses, only that area is affected|
|(?: re)|Group regular expressions without remembering matched text|
|(?imx: re)|Temporarily toggle on i, m, or x options within parentheses|
|(?-imx: re)|Temporarily toggle off i, m, or x options within parentheses|
|(?#...)|A comment|
|(?= re)|Specify position using a pattern regardless range|
|(?! re)|Specify position using pattern negation regardless range|
|(?> re)|Match independent pattern without backtracking|
|\w|Match word characters|
|\W|Match nonword characters|
|\s|Match whitespace similarly to [\t\n\r\f]|
|\S|Match nonwhitespace|
|\d|Match digits similarly to [0-9]|
|\D|Match nondigits|
|\A|Match beginning of string|
|\Z|Match end of string. If a newline exists will do match just before newline|
|\z|Match end of string|
|\G|Match point where last match finished|
|\b|Match word boundaries when outside brackets. Match backspace (0x08) when inside brackets|
|\B|Match nonword boundaries|
|\n, \t, etc.|Match newlines, carriage returns, tabs, etc.|
|\1...\9|Match nth grouped subexpression|
|\10|Match nth grouped subexpression if matched already. Otherwise refers to the octal representation of a character code|

### # Making use of the Pattern Matching
```python
import re

# Find 'Python' or 'python'
print re.findall(r'[Pp]ython', 'A Python string under test')

> ['Python']


# Find 'Python or pythom'
print re.findall(r'[Pp]ytho[nm]', 'A Pythom string under test')

> ['Pythom']


# Find 'Python' or 'Pytho'
print re.findall(r'Python?', 'A Pytho string under test')

> ['Pytho']


# Find 'Python' or 'Perl'
print re.findall(r'Python|Perl', 'A Perl string under test')

> ['Perl']


# Find 'Python' and 'Pearl'
print re.findall(r'([Pp])ython&\1aerl', 'A Python&Perl string under test')

> ['Python&Pearl']
```

As regEx by itself is a very interesting chellenge at times, i have found great help <a href='http://pythex.org/'>here</a> and <a href='https://www.regexone.com/lesson/introduction_abcs'>here</a> in solving this type of string manipulation issues.


#### Sources:

* <a href='https://docs.python.org/2/library/re.html'>Regular Expression Operations</a>
* <a href='https://docs.python.org/2/howto/regex.html#regex-howto'>Regular Expressions HOW TO</a>
