---
layout: post
title: Web Scraping
subtitle: A Powerful Business Tool
comments: false
show-avatar: true
published: true
---

When it comes to Business Intelligence, more and more the Internet provides with abundant sources of data for industry practitioners. 
Extracting data from websites however, can at times be a tedious and daunting task especially when the selected data source does not provide with a formal <a href='https://en.wikipedia.org/wiki/Web_API'>API</a>, and here is where web scraping comes to rescue.

Web <a href='https://en.wikipedia.org/wiki/Web_scraping'>scraping</a>, essentially are the techniques employed programmatically so that information is extracted from web places, information that in first place was arranged to be read by human eye rather than by computers.

Within Python universe, there is a number of powerful tools that can be used to handle such parsing tasks, being the most prominent <a href='https://pypi.python.org/pypi/beautifulsoup4'>BeautifulSoup</a>, <a href='https://pypi.python.org/pypi/selenium'>Selenium</a>, <a href='https://pypi.python.org/pypi/Scrapy'>Scrapy</a> and <a href='https://pypi.python.org/pypi/lxml'>Lxml</a>. The first two are simpler to use, while the two latest are for the more advanced user. Actually, note that Scrapy is of a different breed from all others, being a complete framework that allows for parsing and web-crawling pretty much alike search engines in their world-wide crawling routines.

Cool! But what real world examples can be solved by this libraries? To mention a few:

* Getting companies' financial data;
* Obtaining stock market live prices;
* Check competitors' products pricing;
* Read weather forecasts;
* Grab entire websites...


## # Parsing Example

Now let's grab an example to expand further. If you are a stock market follower, you can find financial information all over the web, and the diversity of data sources available it is quite extensive nowadays.

In this article, we will show you how to make your data extraction by building a web scraper to retrieve stock indices automatically from the Internet. The selected data source for the example was <a href='http://www.teletrader.com/'>Teletrader</a>, and we will be obtaining data pertaining to <a href='http://www.teletrader.com/dax/index/tts-514562'>German DAX index</a>.

<p align='center'>
	<img src='https://raw.githubusercontent.com/hpsilva/hpsilva.github.io/master/img/posts/2015-12-26-web-parsing_0.png' title="Website view">
</p>

To start with, we need to select the data to be targeted, by having a peep into the webpage code. To do so, browsers nowadays have a built-in tool that can be found by right clicking over the page element we wish to observe and selecting `Inspect` in the context menu.

<p align='center'>
	<img src='https://raw.githubusercontent.com/hpsilva/hpsilva.github.io/master/img/posts/2015-12-26-web-parsing_1.png' title="Data to be parsed">
</p>

And this is how the code looks like for that particular `url`:
<p align='center'>
	<img src='https://raw.githubusercontent.com/hpsilva/hpsilva.github.io/master/img/posts/2015-12-26-web-parsing_2.png' title="webpage HTML">
</p>

So far we have identified where data will be parsed from, and spotted the elements in the webpage html to target with our script. Note that it is a `span` element that we can reference by the class name `last last-delayed` and this information will be relevant in the next step.


## # Extracting Data with Beautiful Soup

BeautifulSoup library provides in a simple way methods for navigating HTML trees and extracting required data in just a few lines of code. Another important magic it runs under the hood, is that it automatically handles Unicode document conversions from/to UTF-8 encoding system. As we have seen in our previous articles (<a href='http://hpsilva.io/2015-12-01-dealing-with-unicode/'>here</a> and <a href='http://hpsilva.io/2015-12-05-dealing-with-unicode-2/'>here</a>) this is a really handy feature by helping to avoid troublesome operations. Just out of curiosity, BeautifulSoup is built on top of other popular Python parsers like lxml and html5lib, thus 
allowing selection of different parsing engines and related speed advantages.

To start with, we must install the required libraries:

```linux
$ pip install BeautifulSoup

$ pip install urllib2
```

Next, in a Python console we run the following commands:

```python

# Libraries Import
import urllib2
import BeautifulSoup as bs

# Set the target URL
url = 'http://www.teletrader.com/dax/index/tts-514562'

# GET URL Data
data = urllib2.urlopen(url)

# Check Server response
data.code
> 200

# Parse data with BeautifulSoup
soup = bs.BeautifulSoup(data)
```

By now, our script loaded the required libraries, successfully downloaded the code sitting at referenced `url`, and parsed that html code into a BeautifulSoup object.

Next we instruct BeautifulSoup to find the `span` element with a class named `last last-delayed`, and extract the resulting text content:

```python

# Target HTML element
price = soup.find(name='span', attrs={'class':'last last-delayed'})

# Print to Screen
print(price)
> <span class="last last-delayed">10,481.91</span>

# Target the string
price.text
> u'10,481.91'
```

Great! Note that in very few steps we built up a script to read German DAX index price at any given time. 

## # More BeautifulSoup

But what if we want to obtain price data for all German DAX index constituents? Being the case, we need to point our script to the table  element present within the same page, thus no need for additional data download as it make part of the current BS object.

```python
# Target <div> with table
div = soup.find(name='div', attrs={'class': 'component index-members clearfix'})

# Select Table Body
tBody = div.table.tbody

# Select Table Rows tr
tRows = tBody.findAll(name='tr')
```

In first place the script search for the `div` containing the target table with class name `component index-members clearfix`, next it goes down on the html tree to find `tbody` tag. Once selected, it looks for all table rows `tr` tags that contain the desired data.

```python
# Initialize DataFrame
df = pd.DataFrame(columns=['stock', 'price'])

# Iterate Table entries and store to DataFrame
for item in tRows:
    # Pick Data
    try:
        stock = item.find(name='td', attrs={'class': 'cell-first name'}).text
        price = item.find(name='td', attrs={'class': 'last'}).text
    except:
        pass
    
    # Add to DataFrame
    df = df.append({'stock': stock,
                   'price': price},
                  ignore_index=True)
    
# Display results
df.head()
```

Lastly our script iterate over each parsed table row stored under the variable `tRows` and store related data to a pandas dataframe for convenience. We close this article by displaying the head of our neat dataframe:

<div>
<table border="0" class="dataframe">  <thead>    <tr style="text-align: center;">      <th></th>      <th>stock</th>      <th>price</th>    </tr>  </thead>  <tbody>    <tr>      <th>0</th>      <td>ALLIANZ SE NA O.N.</td>      <td>132.00</td>    </tr>    <tr>      <th>1</th>      <td>BASF SE NA O.N.</td>      <td>73.28</td>    </tr>    <tr>      <th>2</th>      <td>BAY.MOTOREN WERKE AG ST</td>      <td>73.93</td>    </tr>    <tr>      <th>3</th>      <td>BAYER AG NA O.N.</td>      <td>89.48</td>    </tr>    <tr>      <th>4</th>      <td>BEIERSDORF AG O.N.</td>      <td>84.26</td>    </tr>  </tbody></table>
</div>
<br>
For article simplicity, the demonstration here developed covers a small part of the parsing functionalities available to the user. Nonetheless, and from our point of view it provides the reader with great hints of what tasks can get done at ease. Obviously the code could be developed much further with things like error control routines, multiprocessing, throtling, etc., steps that essentially **must be** present in a bigger scrapping projects. 

Now we leave you to experiment your own example. Happy scrapping!
<br>
