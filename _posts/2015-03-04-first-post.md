---
layout: post
title: Hello World!
subtitle: First post for stack test purposes
comments: false
show-avatar: true
bigimg: /img/banner-flying.jpg
---

###### This is my first post, how exciting!

# Header 1

## Header 2

### Header 3

#### Header 4

##### Header 5

###### Header 6

> Look, here it's a blockquote!

|Number|Another Number|Last Number|
|:-|:-|:-|
|One|Two|Three|
|Three|Two|One|

**Code Chunk:**

~~~
x = 1 + 2
~~~


**Another Code Chunck**

```python
print('Hello World')

class aclass:
  '''
  Class Constructor
  '''
  
  def __init__():
    print('The constructor')
    
object = aclass()

print(object)
```

```latex
\documentclass[a4paper]{article}
\usepackage{fontspec}
\usepackage{minted}

\setsansfont{Calibri}
\setmonofont{Consolas}

\begin{document}
\renewcommand{\theFancyVerbLine}{
  \sffamily\textcolor[rgb]{0.5,0.5,0.5}{\scriptsize\arabic{FancyVerbLine}}}

\begin{minted}[mathescape,
               linenos,
               numbersep=5pt,
               gobble=2,
               frame=lines,
               framesep=2mm]{csharp}
  string title = "This is a Unicode π in the sky"
  /*
  Defined as $\pi=\lim_{n\to\infty}\frac{P_n}{d}$ where $P$ is the perimeter
  of an $n$-sided regular polygon circumscribing a
  circle of diameter $d$.
  */
  const double pi = 3.1415926535
\end{minted}
\end{document}
```

**Lastly, a plot**
<iframe width="770" height="400" frameborder="0" scrolling="no" src="https://plot.ly/~hpsilva/5.embed"></iframe>
