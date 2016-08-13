---
layout: post
title:  "Chapter01"
tags: python
permalink: /tech/python/chapter01
---

arkDown Test
------
> This is a paragraph inside
a blockquote.
>
> > This is a nested paragraph
that continues here
> and here
> > and here

~~~~~~~~ python
def factorial(x):
     if x == 0:
         return 1
     else:
         return x * factorial(x - 1)
~~~~~~~~

definition term 2
: This is the first line. Since the first non-space characters appears in
column 3, all other lines have to be indented 2 spaces (or lazy syntax may
  be used after an indented line). This tells kramdown that the lines
  belong to the definition.
:       This is the another definition for the same term. It uses a
        different number of spaces for indentation which is okay but
        should generally be avoided.
   : The definition marker is indented 3 spaces which is allowed but
     should also be avoided.


     | First cell|Second cell|Third cell
     | First | Second | Third |

     First | Second | | Fourth |
