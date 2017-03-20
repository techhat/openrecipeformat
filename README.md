---
layout: default
permalink: /index.html
---

# Open Recipe Format

In the beginning, there was food. And then there were dishes. And somewhere down the line, people started writing down how to make the dishes. And most of them weren't very good at it. And then they got computers, and they still weren't very good at it.

The Open Recipe Format has been designed to solve some basic needs: accurate and flexible storage of recipes. While there have been attempts in the past to create standardized computer recipe formats, they have so far met with failure. This stems from several problems, all of which stem from a lack of understanding of the tasks at hand (and in most cases, ignorance of which tasks actually need to be addressed).

A significant portion of the population cooks at home, and so most solutions target home cooks. Commercial solutions exist, and address a host of new considerations that are not thought to relate to home cooks. The Open Recipe Format was initially created by a software engineer with a cooking degree and professional kitchen experience. Few, if any, other attempts at writing food software, much less standardized recipe data modeling, can make this claim.

At the heart of the Open Recipe Format is an established file format called YAML. This format was chosen for a variety of reasons:

-   It is text-based, and therefore human readable.
-   It mimics the internal data structures of several high-level programming languages.
-   It can easily be converted to and from other formats, such as the more popular JSON (in fact, JSON is syntactically-correct YAML).
-   It is more human readable than JSON.
-   It is far more light-weight than other chatty formats, like XML.
-   It is far more flexible than legacy formats like EDI.
-   As a text-based format, it can be easily managed by revision control software, such as git.

This repository is intended more for programmers than anyone else. As human-readable as the format is, it is likely to be confusing to many in its raw format. The job of the programmer is to use this spec in the development of their own software packages, websites, etc., and provide a friendly interface to the end-user.

Many of the files in this repository are intended to document the Open Recipe Format. Others are examples, to help programmers understand how to best use the format. And finally, sample source code will be provided to give programmers a jump-start in their coding efforts.

Getting Started
===============

This walkthrough is made to help individuals get started quickly and gain a foundational knowledge of the Open Recipe Format:

A Basic Recipe&lt;/topics/tutorials/walkthrough&gt;

In addition to an Open Recipe Format, an Open Nutrition Format is being established. These two formats are described in more detail here:

Developers References:  
-   Open Recipe Format Reference&lt;topics/reference/orf&gt;
-   Open Nutrition Format Reference&lt;topics/reference/onf&gt;


