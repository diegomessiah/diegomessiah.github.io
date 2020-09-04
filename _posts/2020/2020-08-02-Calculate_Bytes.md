---
layout: single
title: "Python - Calculate Storage"
excerpt: "This article explain how write script than calculate weight storage"
permalink:
tags:
  - Python
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
---

{% capture mynote%}
**Test environment** Python 3.7
{% endcapture %}
{{mynote}}{: .notice--info}

## Calculate Storage
On typical <b>ext4</b> file system (what most people use), the default inode size is 256 bytes, block size is 4096 bytes.
A directory is just a special file which contains an array of filenames and inode numbers. When the directory was created, the file system allocated 1 inode to the directory with a "filename" (dir name in fact). The inode points to a single data block (minimum overhead), which is 4096 bytes. 

If a filesystem has a block size of 4096 bytes, this means that a file comprised of only one byte will still use 4096 bytes of storage. A file made up of 4097 bytes will use 4096*2=8192 bytes of storage. Knowing this, can you fill in the gaps in the calculate_storage function below, which calculates the total number of bytes needed to store a file of a given size?

```
def calculate_storage(filesize):

    block_size = 4096
    # Use floor division to calculate how many blocks are fully occupied
    full_blocks = filesize//block_size
    # Use the modulo operator to check whether there's any remainder
    partial_block_remainder = filesize%block_size
    # Depending on whether there's a remainder or not, return
    # the total number of bytes required to allocate enough blocks
    # to store your data.
    if partial_block_remainder > 0:
        return block_size*full_blocks+block_size
    return block_size*full_blocks
```
```
print(calculate_storage(1))    # Should be 4096
```
```
print(calculate_storage(4096)) # Should be 4096
```
```
print(calculate_storage(4097)) # Should be 8192
```


