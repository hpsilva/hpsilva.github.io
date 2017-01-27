---
layout: post
title: Dealing with Unicode Issues
subtitle: A simple way to
comments: false
show-avatar: true
---

Unicode issues are one of a kind problem to deal with when it comes to i.e. parsing websites, or even worst when throw silent bugs. This particular type of problem essentially arise when handling non-English languages which as opposed to unaccented English, they hold a much larger ammount of characters and special characters. Just think of Latin languages for instance, or the Cyrillic alphabet.

In the situation that the data under scrutiny is for own consumption, on this end we are usually more focused on its readability (by converting to <a href='https://en.wikipedia.org/wiki/ASCII'>ASCII</a>) rather than its similarity to origin. With that said, there is a number of very simple actions one can care of so that our data is easily readable:

# # List comprehensions
By keeping the `ord(char)` below 128 we assure that our characters will be only ascii, like so:

```python
unicode_string = u'Importação'
fix = ''.join([x for x in unicode_string if ord(x) < 128])

> 'Importao'
```
<br>


# # String encode method
Another possibility is to make use of the built in library and it's encode/decode methods. It encodes a string to a given encoding, but note that it must be assured the arguments `ignore` or `replace` are passed:

```python
unicode_string = u'Importação'
unicode_string.encode('ASCII', 'ignore')

> 'Importao'


unicode_string.encode('ASCII', 'replace')

> 'Importa??o'
```
<br>


# # Unicodedata library
In dealing with this unicode sort of issues, the simplest way found is to make use of the standard library `unicodedata`, that allow latin unicode characters to degrade nicely into ASCII.

Unicodedata contains a method named `normalize` that is used to return the normal form of the Unicode string. Furthermore it has several operating modes (NFC, NFKC, NFD, NFKD), but as of now we are just concerned to degrade from Unicode to ASCII so we'll be using this time around `NFKD` like so:

```python
import unicodedata as unicode

unicode_string = u'Importação'
unicode.normalize('NFKD', unicode_string).encode('ASCII', 'ignore')

> 'Importacao'
```
<br>


As you could see this methods of sorting unicode issues are fairly simple and of straight forward application thus avoiding the Unicode characters pain.

For your further reference i'd suggest you to have a look at <a href='https://docs.python.org/2/howto/unicode.html'>Python unicode</a> and <a href='https://docs.python.org/2/library/unicodedata.html'>unicodedata</a> docs.
