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


### Data with initial spaces
Some CSV files can have a space character after a delimiter. When we use the default csv.reader() function to read these CSV files, we will get spaces in the output as well.

To remove these initial spaces, we need to pass an additional parameter called skipinitialspace. 
```
import csv
with open('people.csv', 'r') as csvfile:
    reader = csv.reader(csvfile, skipinitialspace=True)
    for row in reader:
        print(row)
```

<b> reader = csv.reader(csvfile, skipinitialspace=True) </b> this allows the reader object to know that the entries have initial whitespace. As a result, the initial spaces that were present after a delimiter is removed.

### Data with quotes
Some CSV files can have quotes around each or some of the entries.

Writer, Mark Twain, "Travel is fatal to prejudice, bigotry, and narrow-mindedness."
```
import csv
with open('quates.csv', 'r') as file:
    reader = csv.reader(file, quoting=csv.QUOTE_ALL)
    for row in reader:
        print(row)
```

reader = csv.reader(file, quoting=csv.QUOTE_ALL), we have passed csv.QUOTE_ALL to the quoting parameter. 

It is a constant defined by the csv module.

csv.QUOTE_ALL specifies the reader object that all the values in the CSV file are present inside quotation marks.

There are 3 other predefined constants you can pass to the quoting parameter:

csv.QUOTE_MINIMAL - Specifies reader object that CSV file has quotes around those entries which contain special characters such as delimiter, quotechar or any of the characters in lineterminator.
csv.QUOTE_NONNUMERIC - Specifies the reader object that the CSV file has quotes around the non-numeric entries.
csv.QUOTE_NONE - Specifies the reader object that none of the entries have quotes around them.
