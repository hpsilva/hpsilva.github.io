---
layout: post
title: Dealing with Unicode Issues II
subtitle: A simple way to
comments: false
show-avatar: true
published: true
---


In our <a href='http://hpsilva.io/2015-12-01-dealing-with-unicode/'>previous</a> article on unicode issues we dealt with the problem by taking simple steps to convert non-English characters to <a href=''>ASCII</a>. As mentioned, this is just fine in a context where special characters do not matter for the purpose of work to get done. But what if the task at hand comprises exchanging data with **Web** interfaces that deal with several languages? Being the case, unicode problematic must be cared of properly, and that is what will get covered in this article in bigger depth.

Essentially the issue is that <a href='https://en.wikipedia.org/wiki/ASCII'>ASCII</a> tables contain a limited number of characters, and within those characters are solely included those related to non accented English. Unicode came to solve this problematic by basically allowing the use of a multitude of characters and therefore languages. The difficulty here is that we need to deal with strings by making use of a different approach and keeping the system informed of what encoding is being used.


In Python 2, there are a number of rules that got to be followed by if we want to avoid having issues with unicode, as summarized here:

* Strings shall be always processed internally as `unicode` rather then `str` objects. First time the system is given a `str` object, it shall get converted right away to `unicode` object by calling the method `.decode('utf-8')`, where the system gets information about what the encoding is.
* Next, everytime the system outputs content by i.e. storing out to a file, use the method `.encode('utf-8)` to encode the content correctly.

If this convention is not followed, likely is that we will see lots of strange characters in those strings with non-English content. Note that the approach is simple: `strings` must be converted to `unicode` objects in first place!

Let's walk through a couple of examples so that our unicode will get evidenced. To start with download this file <a href='https://raw.githubusercontent.com/hpsilva/hpsilva.github.io/master/_posts/data/string.txt'>here</a>.

# # Reading Content
Next, inside Python command line read the file from disk, check its `type` and `print` the content to screen.

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
> 'Ol\xe1'

# Print content to screen
print(string)
> Olß
```

As we can see, the file is read from disk as a `str` type as expected. Next by checking `string` variable content we arrive into our first issue: the file's content is `Olá`, but after being imported to Python is became `Ol\xe1`. Further on, by printing `string` variable to screen we are shown `Olß`. Now do you understand why you find all over the internet comments about the **unicode pain**? Right, let's elaborate a bit more and try to debunk what is happening under the hood.


When Python read the file from disk, we did not informed about what it was the encoding of our file's content in first place. Therefore it assumed the content to be the default set in the system, which most probably is 'ASCII'. 



We can check what our default encoding is by running:

```python
import sys

sys.getdefaultencoding()
> 'ascii'
```

In my case, the default set is `ascii`.

All this is fine, because every character in a string is a single byte, and the `ASCII` table translates each byte value into a unique character, thus the need to fallback to an encoding. Now what we want to do is to inform python about that variable's encoding so that it can correctly assing the right caracters for our file content, like so:

```python


```



# # Unicode



Sources: 
Actually an oldie but goldie article on why all this unicode mess emerged and keeps going on today during current moderm computing can be found <a href='http://www.joelonsoftware.com/articles/Unicode.html'>here</a>!
