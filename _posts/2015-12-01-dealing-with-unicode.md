---
layout: post
title: Dealing with Unicode Issues
subtitle: A simple way to
comments: false
show-avatar: true
---

Unicode issues have been one of the difficult problems to deal with when it comes to external libraries, and at times external hardware does not support it and throw nasty errors or silent bugs.

Usually the problems i have to tackle concern more data readability rather then to be kept like the original, and as such some of the tricks described below will do.

### List comprehension

By keeping the 'ord(char)' below 128 we assure that our characters will be only ascii, like so:

```
unicode_string = 'Importação'
fix = ''.join([x for x in unicode_string if ord(x) < 128])
```

### String method encode

Another possibility is to make use of the built in library and it's encode/decode methods. It encodes a string to a given encoding, but it must be assured that a special argument is passed that is ''ignore'' or ''replace'', like so

```
unicode_string = 'Importação'
unicode_string.encode('ASCII', 'ignore')
# 

unicode_string.encode('ASCII', 'replace')
# 
```


### Unicodedata library

In deaing with this unicode sort of issues, the best way i have found is to make use of the standard library 'unicodedata', that allow latin unicode characters to degrade nicely into ASCII.

Unicodedata contains a method 'normalize' that is used to return the normal form of the Unicode string. Furthermore it has several modes (NFC, NFKC, NFD, NFKD), but as we are just concerned to degrade from Unicode to ASCII, we'll be using 'NFKD', like so

```
unicode_string = 'Importação'
unicode.normalize('NFKD', unicode_string).encode('ASCII', 'ignore')
# 'Importacao'
```

As you could see this methods of sorting unicode issues are fairly simple and of straight forward application thus avoiding the Unicode characters pain.

For your further reference i' suggest you have a look at the unicodedata documents.
