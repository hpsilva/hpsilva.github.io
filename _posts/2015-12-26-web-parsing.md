---
layout: post
title: Web Scraping
subtitle: A Powerfull Business Tool
comments: false
show-avatar: true
published: true
---

When it comes to Business Intelligence, more and more the Internet provides with abundant sources of data for industry practicioners. 
Extracting data from websites however, can at times be a tedious and dauting task especially when the selected data source does not provide with a formal <a href='https://en.wikipedia.org/wiki/Web_API'>API</a>, and here is where web scraping comes to rescue.

Web <a href='https://en.wikipedia.org/wiki/Web_scraping'>scraping</a>, essentially are the techniques employed programatically so that we extract information from web places, information that in first place was arranged to be read by human eye rather than in a computer friendly format way.

When it comes to Python universe, there is a number of very powerful tools that can be used to handle such parsing tasks, being the most prominent <a href='https://pypi.python.org/pypi/beautifulsoup4'>BeautifulSoup</a>, <a href='https://pypi.python.org/pypi/selenium'>Selenium</a>, <a href='https://pypi.python.org/pypi/Scrapy'>Scrapy</a> and <a href='https://pypi.python.org/pypi/lxml'>Lxml</a>. The first two are simpler to use, while the two latest are for the more advanced user. Actually note that Scrapy is of a diferent breed from all others, being a complete framework that allows for parsing and web-crawling pretty much alike the main search engines use in their world-wide crawling routines.

Cool! But what real world examples can evidence the usefulness of this libraries? To mention a few:
* Getting companies' financial data;
* Obtaining stock market live prices;
* Check competitors' products pricing;
* Read weather forecasts;
* Set alerts based on threshold triggers for any of the above examples...


## # Parsing Example

Now let's stick to an example to expand further. If you are a stock market follower, you can find financial information all over the web, and the diversity of data sources available it is very extensive.

Getting closing prices everyday can be a pain, especially when you have to open several webpages to record them regularly. \

In this article, we will show you how to make your data extraction from easier by building your own web scraper to retrieve stock indices automatically from the Internet using Python to help us group the data. 



## # Selecting Information

The selected data source for the example was <a href='http://www.teletrader.com/'>Teletrader</a>, and we will be obtaining data pertaining to <a href='http://www.teletrader.com/dax/index/tts-514562'>DAX contituents</a>.

<IMAGE0>

To start with we need to select the data to be targeted, by having a peep into the webpage code. To do so, browsers nowadays have built-in a tool that can be found by right clicking over the page element we wish to observe and selecting `Inspect` in the context menu.

<IMAGE1>

<IMAGE2>

So far we have identified where data will be parsed from, and spotted the elements in the webpage html that we will be targeting by our script. Note that it is a `<span>` element that we can reference by the class name `class="last last-delayed"`.


## # Extracting that Data 




## # Transforming
