---
layout: post
title: "Understanding Python Data Structures"
comments: true
keywords: "learnpython"
date: 2023-09-20 23:41:00 +05:30
tags: learnpython 
---

## Table of Content

1. [[^String]]
2. [[^List]]
3. [[^Set]] 
4. [[^Tuple]]

## [^String]: String

Strings are immutable in Python.

```

x = 'banana'

for idx in range (0,5):
    print x[idx], "=", id(x[idx])

b = 91909376
a = 91836864
n = 91259888
a = 91836864
n = 91259888
```

**NOTE** : We have printed addresses of each character from the string, note that a and a, n and n point to the same location.

Since Python 3, the str type uses Unicode representation. Unicode strings can take up to 4 bytes per character depending on the encoding, which sometimes can be expensive from a memory perspective.<br/>

To reduce memory consumption and improve performance, Python uses three kinds of internal representations for Unicode strings:<br/><br/>

`
**1 byte per char (Latin-1 encoding)** | If all characters in a string can fit in ASCII range, then they are encoded using 1-byte Latin-1 encoding. Basically, Latin-1 represents the first 256 Unicode characters
**2 bytes per char (UCS-2 encoding)** | Non-Latin languages, such as Chinese, Japanese, Hebrew, Cyrillic
**4 bytes per char (UCS-4 encoding)** | The 4-byte (UCS-4) encoding is used when a string contains special symbols, emojis or rare languages
`
<br/><br/>

When programming in Python all strings behave the same, and most of the time we don't notice any difference. However, the difference can be very remarkable and sometimes unexpected when working with large amounts of text.<br/>

To see the difference in internal representations, we can use the sys.getsizeof function, which returns the size of an object in bytes:
```
>>> import sys
>>> string = 'hello'
>>> sys.getsizeof(string)
54
>>> # 1-byte encoding
>>> sys.getsizeof(string+'!')-sys.getsizeof(string)
1
>>> # 2-byte encoding
>>> string2  = '你'
>>> sys.getsizeof(string2+'好')-sys.getsizeof(string2)
2
>>> sys.getsizeof(string2)
76
>>> # 4-byte encoding
>>> string3 = '🐍'
>>> sys.getsizeof(string3+'💻')-sys.getsizeof(string3)
4
>>> sys.getsizeof(string3)
80
```

Depending on the content of a string, Python uses different encoding.<br/>
The standard Python version (Normallly called CPython) will identify the longest Unicode character in the string, and then store every character padded to that length; so a string with lots of ASCII (1 byte characters) with a single 4 byte character will be stored as a sequence of 4 bytes where each character is padded to fit into those 4 bytes (in this example).<br/>

The reason for this is that it makes comparisons and indexing very simple; strings are stored internally in contiguous memory so character N in a string will always be at address P + (N* K) where<br/>

P is the pointer to the first character in the string<br/>
K is the ‘kind’ of string - ie the padded length of the characters in the string<br/>

**NOTE** : Every string in Python takes additional 49-80 bytes of memory, where it stores supplementary information, such as hash, length, length in bytes, encoding type and string flags.<br/>


<br/>


## [^List]: Lists

## [^Set]: Set

## [^Tuple]: Tuple



