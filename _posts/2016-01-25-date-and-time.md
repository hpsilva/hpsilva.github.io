---
layout: post
title: Date & Time tools
subtitle: A primer
comments: false
show-avatar: true
published: false
---

On the occasion that I am rebuilding part of my trading system, I felt that it was a good opportunity to shed some light on date and time manipulation in Python, as well to put a bit of order on my learnings. I consider that this is a very important topic not only in the context of trading but in computing in general. Just think for a bit about how much of what we do daily depend on the right time, particularly in computing!

If time objects were just about local time itself the task would be easy, however some challenges emerge when we add to the mixture two more factors required to be accounted for:
• Time is measured in relation to what?
•	Daylight Time Savings (DST) variation along an year;
•	Time zone differences between locales;

### INTRO TO TIME ZONES
**<a href='https://en.wikipedia.org/wiki/Time_zone'>Time zone</a>** is a relatively new concept in the long history of measuring time. During most of the 19th century pretty much each European city had its own definition of local time. It was not until 1880 that Greenwhich Mean Time was officially made the standard time in Great Britain. Much of the remaining wol had adopted the idea by the 1920s. Today, all countries in the world use standard time zones, though not everyone is using full-hour offsets to the GMS as it was orginally conceived.

The concept of summer time (daylight saving time) complicates thigs further: for example in European Union the member states will switch to summer time on the last Sunday of March at 01:00 GMT exact. The summer time lasts until the last Sunday of October, 01:00 GMT.

In Finland, this means that this year on 30th March the official time stopped from 02:59:59 EET to 04:00:00 EEST in an instant. Likewise, on 26th October this year, the summer time clocks will tick up to 03:59:59 EEST, and on the next second the local time will be 03:00:00 EET; amd almost an hour later, 03:59:59 EET. Thus, the number of seconds between 02:59:59 and 04:00:00 on a single day might be 1, 3601, or 7201; the difference between 02:59:59 and 03:00:01 might likewise be 2 or 3602 seconds...or might be undefined.

To alleviate obvious confusions and misunderstandings, a reference time scale can be used for calculations that concern different time zones. The obvious choice is Coordinated Universal Time (UTC) that replace Greenwich Mean Time as the standard reference time scale for civilian application in 1972. During the Internet era UTC has become increasingly important.


### TIME ZONE IN PYTHON
Suppose you have a shared web calendar application that is used by people all over the world. Each user wants to view the calendar in their respective local time, and you wish to use UTC on the server. The server has been set up with Europe/Helsinki as the local time zone. Ans you wish to use the facilities provided by Python standard library modules. Simple data arithmetic would be needed you might think! But soon you will find out it not at all simple. Actually is annoyingly complicated:

```python
from datetime import datetime

datetime.now()
>> datetime.datetime(2016, 11, 18, 13, 39, 29, 910000)

```

Fortunately Python datetimes can be made time zone aware, by supplying an instance of tzinfo in the constructor. Unfortuantely anough, the Python standard library does not provide ay concrete implementations. Then it enters Pytz, a Python library that supplies hundreds of concrete time zone definitions.

### OTHER LIBRARIES


### PANDAS


### CLOSING THOUGHTS
DATETIM VS TRADING


