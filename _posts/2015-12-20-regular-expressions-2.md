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

If you are curious about the power of what can get done with RegEx, just bear with me a bit more as i'll provide few more examples this time around focusing on regEx patterns.

To start with it should be remarked that there are various characters which would have special meaning for `Python` when they are used in regular expressions. 
To avoid conflicting situations while dealing with regEx in Python, we shall then make use of **raw strings** instead as `r'expression'`.

### RegEx Patterns

|Modifier|Description|
|:-|:-|
|re.I|Case-insensitive matching|
|re.L|Interprets words according to the current locale. This interpretation affects the alphabetic group (\w and \W), as well as word boundary behavior (\b and \B)|
|re.M|Makes $ match the end of a line (not just the end of the string) and makes ^ match the start of any line (not just the start of the string)|
|re.S|Makes a period (dot) match any character, including a newline|
|re.U|Interprets letters according to the Unicode character set. This flag affects the behavior of \w, \W, \b, \B|
|re.X|Permits "cuter" regular expression syntax. It ignores whitespace (except inside a set [] or when escaped by a backslash) and treats unescaped # as a comment marker|

### RegEx Modifiers
Except for control characters, (+ ? . * ^ $ ( ) [ ] { } | \), all characters match themselves. You can escape a control character by preceding it with a backslash.

Following table lists the regular expression syntax that is available in Python −

|Pattern|Description|
|:-|:-|
|^|Matches beginning of line|
|$|Matches end of line|
|.|Matches any single character except newline. Using m option allows it to match newline as well|
|[...]|Matches any single character in brackets.|
|[^...]|Matches any single character not in brackets|
|re*|Matches 0 or more occurrences of preceding expression.|
|re+|Matches 1 or more occurrence of preceding expression.|
|re?|Matches 0 or 1 occurrence of preceding expression.|
|re{ n}|Matches exactly n number of occurrences of preceding expression.|
|re{ n,}|Matches n or more occurrences of preceding expression.|
|re{ n, m}|Matches at least n and at most m occurrences of preceding expression.|
|a\| b|Matches either a or b.|
|(re)	|Groups regular expressions and remembers matched text.|
|(?imx)|Temporarily toggles on i, m, or x options within a regular expression. If in parentheses, only that area is affected.|
|(?-imx)|Temporarily toggles off i, m, or x options within a regular expression. If in parentheses, only that area is affected.|
|(?: re)|Groups regular expressions without remembering matched text.|
|(?imx: re)|Temporarily toggles on i, m, or x options within parentheses.|
|(?-imx: re)|Temporarily toggles off i, m, or x options within parentheses.|
|(?#...)|Comment.|
|(?= re)|Specifies position using a pattern. Doesn't have a range.|
|(?! re)|Specifies position using pattern negation. Doesn't have a range.|
|(?> re)|Matches independent pattern without backtracking.|
|\w|	Matches word characters.|
|\W|Matches nonword characters.|
|\s|Matches whitespace. Equivalent to [\t\n\r\f].|
|\S|Matches nonwhitespace.|
|\d|Matches digits. Equivalent to [0-9].|
|\D|Matches nondigits.|
|\A|Matches beginning of string.|
|\Z|Matches end of string. If a newline exists, it matches just before newline.|
|\z|Matches end of string.|
|\G|Matches point where last match finished.|
|\b|Matches word boundaries when outside brackets. Matches backspace (0x08) when inside brackets.|
|\B|Matches nonword boundaries.|
|\n, \t, etc.|Matches newlines, carriage returns, tabs, etc.|
|\1...\9|Matches nth grouped subexpression.|
|\10|Matches nth grouped subexpression if it matched already. Otherwise refers to the octal representation of a character code|


Sources:

* <a href='https://docs.python.org/2/library/re.html'>Regular Expression Operations</a>
* <a href='https://docs.python.org/2/howto/regex.html#regex-howto'>Regular Expressions HOW TO</a>


