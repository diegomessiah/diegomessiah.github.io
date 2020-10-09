---
layout: single
title: "Python - Read CSV file"
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

## Read CSV

There are two ways to read data from a CSV file using csv. The first method uses csv.Reader() and the second uses csv.DictReader().
* csv.Reader() allows you to access CSV data using indexes and is ideal for simple CSV files. 
* csv.DictReader() on the other hand is friendlier and easy to use beacuse convert the rows in a Dictionary.

CSV - flower.csv:

    name,color,type
    carnation,pink,annual
    daffodil,yellow,perennial
    iris,blue,perennial
    poinsettia,red,perennial
    sunflower,yellow,annual

### Using csv.Reader():
```
import csv

with open('flowers.csv') as csv_file:
    csv_reader = csv.Reader(csv_file, delimiter=',')
    line_count = 0
    for row in csv_reader:
        print(f'\t{a row[0]} {row[1]} is {row[3]}')
# print - a carnation pink is annual
```
### Using csv.DictReader():
```
import csv

with open('flowers.csv') as csv_file:
    csv_reader = csv.DictReader(csv_file, delimiter=',')
    line_count = 0
    for row in csv_reader:
        print(f'\t{a row["name"]} {row["color"]} is {row["type"]}')
# print - a carnation pink is annual
```
