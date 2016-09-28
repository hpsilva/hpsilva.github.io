---
layout: post
title: Web Scraping
subtitle: A Powerful Business Tool
comments: false
show-avatar: true
published: true
---

When it comes to Business Intelligence, more and more the Internet provides with abundant sources of data for industry practicioners. 
Extracting data from websites however, can at times be a tedious and dauting task especially when the selected data source do not provide with a formal <a href='https://en.wikipedia.org/wiki/Web_API'>API</a>, and here is where web scraping comes to rescue.

Web <a href='https://en.wikipedia.org/wiki/Web_scraping'>scraping</a>, essentially are the techniques employed programatically so that we extract information from web places, information that in first place was arranged to be read by human eye rather than in a computer friendly format way.

Within Python universe, there is a number of powerful tools that can be used to handle such parsing tasks, being the most prominent <a href='https://pypi.python.org/pypi/beautifulsoup4'>BeautifulSoup</a>, <a href='https://pypi.python.org/pypi/selenium'>Selenium</a>, <a href='https://pypi.python.org/pypi/Scrapy'>Scrapy</a> and <a href='https://pypi.python.org/pypi/lxml'>Lxml</a>. The first two are simpler to use, while the two latest are for the more advanced user. Actually note that Scrapy is of a diferent breed from all others, being a complete framework that allows for parsing and web-crawling pretty much alike the main search engines use in their world-wide crawling routines.

Cool! But what real world examples can be solved by this libraries? To mention a few:

* Getting companies' financial data;
* Obtaining stock market live prices;
* Check competitors' products pricing;
* Read weather forecasts;
* Set alerts based on threshold triggers for any of the above examples...


## # Parsing Example

Now let's stick to an example to expand further. If you are a stock market follower, you can find financial information all over the web, and the diversity of data sources available it is quite extensive nowadays.

Getting closing prices everyday can be a pain, especially when you have to open several webpages to record them often.

In this article, we will show you how to make your data extraction from easier by building your own web scraper to retrieve stock indices automatically from the Internet using Python to help us group the data. 



## # Selecting Information

The selected data source for the example was <a href='http://www.teletrader.com/'>Teletrader</a>, and we will be obtaining data pertaining to <a href='http://www.teletrader.com/dax/index/tts-514562'>German DAX index</a>.

![alt text](https://raw.githubusercontent.com/hpsilva/hpsilva.github.io/master/img/posts/2015-12-26-web-parsing_0.png "Teletrader Platform")

To start with, we need to select the data to be targeted, by having a peep into the webpage code. To do so, browsers nowadays have a built-in tool that can be found by right clicking over the page element we wish to observe and selecting `Inspect` in the context menu.


![alt text](https://raw.githubusercontent.com/hpsilva/hpsilva.github.io/master/img/posts/2015-12-26-web-parsing_1.png "Data to Parse")

![alt text](https://raw.githubusercontent.com/hpsilva/hpsilva.github.io/master/img/posts/2015-12-26-web-parsing_2.png "Page HTML")


So far we have identified where data will be parsed from, and spotted the elements in the webpage html that we will be targeting by our script. Note that it is a `span` element that we can reference by the class name `last last-delayed`.


## # Extracting Data 

```python

# Import Libraries
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

## # Transforming

```python

# Target <div> with table
div = soup.find(name='div', attrs={'class': 'component index-members clearfix'})

# Select Table Body
tBody = div.table.tbody

# Select Table Rows tr
tRows = tBody.findAll(name='tr')
```

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
df
```

<div>
	<table border="0" class="dataframe">  <thead>    <tr style="text-align: center;">      <th></th>      <th>stock</th>      <th>price</th>    </tr>  </thead>  <tbody>    <tr>      <th>0</th>      <td>ALLIANZ SE NA O.N.</td>      <td>132.00</td>    </tr>    <tr>      <th>1</th>      <td>BASF SE NA O.N.</td>      <td>73.28</td>    </tr>    <tr>      <th>2</th>      <td>BAY.MOTOREN WERKE AG ST</td>      <td>73.93</td>    </tr>    <tr>      <th>3</th>      <td>BAYER AG NA O.N.</td>      <td>89.48</td>    </tr>    <tr>      <th>4</th>      <td>BEIERSDORF AG O.N.</td>      <td>84.26</td>    </tr>  </tbody></table>

</div>
