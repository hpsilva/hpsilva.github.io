---
layout: post
title: Dealing with Unicode Issues
subtitle: A simple way to
comments: false
show-avatar: true
---

Unicode issues are one of the difficult problems to deal with when it comes to i.e. parsing websites or even worst, when external hardware does not support it and throw nasty errors or silent bugs.

Usually the problems we have to tackle concern more data readability rather than the similarity to its origins, therefore some of the tricks we will advance below will do.

### List comprehensions
By keeping the `ord(char)` below 128 we assure that our characters will be only ascii, like so:

```python
unicode_string = 'Importação'
fix = ''.join([x for x in unicode_string if ord(x) < 128])

> 'Importao'
```


### String encode method
Another possibility is to make use of the built in library and it's encode/decode methods. It encodes a string to a given encoding, but note that it must be assured the arguments `ignore` or `replace` are passed:

```python
unicode_string = 'Importação'
unicode_string.encode('ASCII', 'ignore')

> 'Importao'


unicode_string.encode('ASCII', 'replace')

> 'Importa??o'
```


### Unicodedata library
In dealing with this unicode sort of issues, the best way we have found around here is to make use of the standard library `unicodedata`, that allow latin unicode characters to degrade nicely into ASCII.

Unicodedata contains a method named `normalize` that is used to return the normal form of the Unicode string. Furthermore it has several modes (NFC, NFKC, NFD, NFKD), but as of now we are just concerned to degrade from Unicode to ASCII so we'll be using this time around `NFKD` like so:

```python
import unicodedata

unicode_string = 'Importação'
unicode.normalize('NFKD', unicode_string).encode('ASCII', 'ignore')

> 'Importacao'
```


As you could see this methods of sorting unicode issues are fairly simple and of straight forward application thus avoiding the Unicode characters pain.

For your further reference i'd suggest you to have a look at the <a href='https://docs.python.org/2/library/unicodedata.html'>unicodedata</a> documents.
