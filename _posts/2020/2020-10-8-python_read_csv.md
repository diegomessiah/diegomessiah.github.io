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
The Python csv module can be used for other file extensions (like: .txt) as long as their contents are in proper structure (commas for default).
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
    csv_reader = csv.reader(csv_file, delimiter=',')
    line_count = 0
    for row in csv_reader:
        print(f'\t{a row[0]} {row[1]} is {row[3]}')
# print - a carnation pink is annual
```
Here, we have opened the flowers.csv file in reading mode using open() function.

Then, the csv.reader() is used to read the file, which returns an iterable reader object.

The reader object is then iterated using a for loop to print the contents of each row.

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
### Custom Delimiters
A comma is used for default as a delimiter, however, some CSV files can use delimiters other than a comma. 

Few popular ones are | and Tab (\t).

Read CSV file Having Tab Delimiter
```
import csv
with open('flowers.csv', 'r') as file:
    reader = csv.reader(file, delimiter = '\t')
    for row in reader:
        print(row)
```
<b> reader = csv.reader(file, delimiter = '\t') </b> As we can see, the optional parameter delimiter = '\t' helps specify the reader object that the CSV file we are reading from, has tabs as a delimiter.
