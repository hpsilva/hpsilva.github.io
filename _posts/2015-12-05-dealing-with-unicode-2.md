---
layout: post
title: Dealing with Unicode Issues
subtitle: A simple way to - take II
comments: false
show-avatar: true
published: true
---

In our <a href='http://hpsilva.io/2015-12-01-dealing-with-unicode/'>previous</a> article on unicode issues we dealt with the problem by taking simple steps to convert non-English characters to <a href=''> flat ASCII</a> ones. As mentioned, this is just fine in a context where special characters do not matter for the purpose of work to get done. But what if the task at hand comprises exchanging data with **Web** interfaces that deal with several languages? Being the case, unicode problematic must be cared of properly, and that is the motto for this article that will discuss the subject in bigger depth.

Essentially the issue is that <a href='https://en.wikipedia.org/wiki/ASCII'>ASCII</a> tables contain a limited number of characters, and within those characters are solely included those related to non-accented English. Unicode came to solve this problematic by basically allowing the use of a multitude of characters and therefore covering every existing language. The difficulty here is that we need to deal with strings by making use of a different approach and keeping the system informed of what encoding is being used.


In Python 2, there are few of rules that got to be followed by if we want to avoid having issues with encoding, as summarized here:

* Strings shall be always processed internally as `unicode` rather then `str` objects. First time the system is given a `str` object, it shall get converted right away to `unicode` object by calling the method `.decode('utf-8')`, where the system gets information about what the encoding is.
* Next, every time the system outputs content by i.e. storing out to a file, use the method `.encode('utf-8)` to encode the content correctly.

If this convention is not followed, likely is that we will see lots of strange characters in those strings with non-English content. Note that the approach is simple: `strings` must be converted to `unicode` objects in first place!

More, note that there are several types of encoding, and the generally accepted and currently used nowadays is `UTF-8`. According to <a href='https://en.wikipedia.org/wiki/UTF-8'>UTF-8</a>, it is a character encoding standard capable of encoding all possible characters, or code points, as defined by Unicode standard.

Now let's walk through a couple of examples so that the task at hand will get evidenced. To start with, download this file <a href='https://raw.githubusercontent.com/hpsilva/hpsilva.github.io/master/_posts/data/string.txt'>here</a>.

# # Getting External Content

Inside a Python console let's read the file from disk, check its `type` and `print` the content to screen.

```python
# Read file content
with open('string.txt', 'r') as data:
    string = data.read()
    data.close()

# Check variable type
type(string)
> <type 'str'>

# Check content
string
> 'Ol\xc3\xa1'

# Print content to screen
print(string)
> Ol├í
```

As we can see, the file is read from disk as a `str` type as expected. Next by checking `string` variable content we arrive into our first issue: the file's content is `Olá`, but after being imported to Python it became `Ol\xc3\xa1`. Further on, by printing `string` variable to screen we are shown `Ol├í`. Now do you understand why you find all over the internet comments about the **unicode pain**? Right, let's elaborate a bit more and try to debunk what is happening under the hood.


When Python read the file from disk, it did not had available any information about what it was the encoding of our file's content in first place. Therefore it assumed the content to be the default set in the system, which most probably is `ASCII`. 


We can check what the default encoding is:

```python
import sys

sys.getdefaultencoding()
> 'ascii'
```

All this is fine, because every character in a string is a single byte, and the `ASCII` table translates each byte value into a unique character, thus the need to fallback to an encoding. Now what we want to do is to inform Python about that variable's encoding so that it can correctly assign the right caracters for our file content, like so:

```python
# Decode the variable
string_decoded = string.decode('utf-8')

# Check the variable type
type(string_decoded)
> <type 'unicode'>

# Variable content
string_decoded
> u'Ol\xe1'

# Display to screen
print(string_decoded)
> Olá
```

Cool! Now that `string` variable was converted to `unicode object` and Python got informed about its content encoding, we have the correct representation of the text `Olá`. Pretty simple, ein!


# # Exporting Content
The process to output content from the system is similar to the previously described, just this time around we are going to make use of the `.encode('utf-8')` method. The logic behind is to inform the system how we want our variable content to be encoded for output, like so:

```python
# Encode the variable
string_encoded = string_decoded.encode('utf-8')

# Display its content
string_encoded
> 'Ol\xc3\xa1'

# Print to screen
print(string_encoded)
>Ol├í

# Store to disk
with open('encoded_string.txt', 'w') as data:
    data.write(string_encoded)
    data.close()
```

And voilà, note how after encoding `string_encoded` content went back to its original representation `Ol├í`, and that is just fine. Furthermore, upon writing the file to disk we can check that `Olá` was properly stored by opening the file. Cool!

# # Final thoughts

As we hopefully demonstrated, to deal with the diversity of languages present nowadays out there thoughout the Web does not need to be complicated, so long we take the necessary steps as demonstrated above to deal with new information that arrive or leave the system.

Lastly we would like to point you to a further reading, actually an oldie but goldie article on why all this unicode mess emerged. It can be read <a href='http://www.joelonsoftware.com/articles/Unicode.html'>here</a>.
