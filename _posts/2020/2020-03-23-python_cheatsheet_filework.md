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

### Comparison operators
```
a == b: a is equal to b
a != b: a is different than b
a < b: a is smaller than b
a <= b: a is smaller or equal to b
a > b: a is bigger than b
a >= b: a is bigger or equal to b
```
### More Information 
Check out the following links for more information:
- [Module OS] (https://docs.python.org/3/library/os.html)
- https://docs.python.org/3/library/os.path.html
- https://en.wikipedia.org/wiki/Unix_time
### Branching blocks

In Python, we branch our code using if, else and elif. This is the branching syntax:
```
1234567
if condition1:
	if-block
elif condition2:
	elif-block
else:
	else-block
```
<b>Remember: The if-block will be executed if condition1 is True. The elif-block will be executed if condition1 is False and condition2 is True. The else block will be executed when all the specified conditions are false. </b>
