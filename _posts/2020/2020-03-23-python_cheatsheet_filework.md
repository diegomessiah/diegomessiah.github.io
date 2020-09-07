---
layout: single
title: "Python - Cheat Sheet - FileWork"
excerpt: "This handy cheat sheet gives you all the information you need at a glance."
permalink:
tags: 
  - Python
  - Cheat_Sheet
categories:
published: true
comments: true
header:
  teaserlogo:
  teaser: ''
  image: images/headers/mountain01_1920x500.jpg
  caption:
gallery:
  - image_path: ''
    url: ''
    title: ''
toc: true
toc_label: "Table of content"
toc_sticky: true
toc_icon: "terminal"
classes: wide
---

{% capture mynote%}
**Tested on** Python 3.8
{% endcapture %}
{{mynote}}{: .notice--info}

## FileWork : Cheat Sheet

This handy cheat sheet gives you all the information you need at a glance. 

### Module OS
- Remove file
```
>>> import os
>>> os.remove("filename")
```
- Rename file
```
>>> import os
>>> os.rename("actual_name", "new_name")
```


### Module OS.Path
- Check if file exist
```
>>> import os
>>> os.path.exists("Filename" or "Path")
Return Bolean
```
- Size of file
```
>>> import os
>>> os.path.getsize("Filename" or "Path")
Return Size in bytes
```
- Last modification 
```
>>> import os
>>> os.path.getmtime("Filename" or "Path")
Return TimeStamp
```
<b>Remember:  Timestamp, it represents the number of seconds since January 1st, 1970.</b>
-- Convert TimeStamp to Date 
```
>>> import os
>>> import datetime
>>> timestamp = os.path.getmtime("Filename" or "Path")
>>> file_date_time = datetime.fromtimestamp(timestamp)
# Convert timestamp to Date
## Type Mon Sep 30 07:06:05 2013
>>> d = date_time.strftime("%c")
print("Date:", d)	
## Type Date 09/30/13
>>> d = date_time.strftime("%x")
print("Date :", d)
## Type Hour 07:06:05
>>> d = date_time.strftime("%X")
print("Date :", d)
```
- Get Absolute Path
```
>>> import os
>>> os.path.abspath("filename" or "path)
Return 'Path'
```

### More Information 
Check out the following links for more information:
- <a href="https://docs.python.org/3/library/os.html" target="_blank">Module OS</a>
- <a href="https://docs.python.org/3/library/os.path.html" target="_blank">Module OS.Path</a>
- <a href="https://en.wikipedia.org/wiki/Unix_time" target="_blank">TimeStamp</a>

