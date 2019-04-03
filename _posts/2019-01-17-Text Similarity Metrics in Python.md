---
layout:     post                    # 使用的布局（不需要改）
title:      Text Similarity Metrics in Python             # 标题 
subtitle:     #副标题
date:       2019-01-17              # 时间
author:     Sandy                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - R
---

## Background
The social media is changing our world. The Ads really have tricks to be put in the social media like Facebook or Tweeter. From the artificial intelligence (AI) perspective, the advertiser definitely needs more support from data science team, helping them analysing the insights behind the postings. For instance:
- How similar are these two words?
- How similar are these two sentences?
- How similar are these two documents?

These above questions I mentioned can be solved in terms of the popular natural language processing (NLP). In this blog, we will present some general algorithms for sentence/words similarity. Normally, it will be displayed with examples in Python.

In this article, we will introduce some simple but useful algorithms for similarity calculation as follows:

**SequenceMatcher function**

Difflib.SequenceMatcher is a flexible class for comparing pairs of sequences of any type, so long as the sequence elements are hashable. The below instruction is from python.org: 

*The basic algorithm predates, and is a little fancier than, an algorithm published in the late 1980’s by Ratcliff and Obershelp under the hyperbolic name “gestalt pattern matching.” The idea is to find the longest contiguous matching subsequence that contains no “junk” elements (the Ratcliff and Obershelp algorithm doesn’t address junk). The same idea is then applied recursively to the pieces of the sequences to the left and to the right of the matching subsequence. This does not yield minimal edit sequences, but does tend to yield matches that “look right” to people.*

SequenceMatcher’s structure as below:
class difflib.SequenceMatcher(isjunk=None, a='', b='', autojunk=True). E.g.:
*from difflib import SequenceMatcher
s1 = “abcd”
s2 = “bcdf”
seq = SequenceMatcher(None, s1, s2)
ratio = seq.ratio()
print(ratio)*

The first parameter ‘isjunk’ should be ‘None’ (as default) or a function towards one of the parameters. For example,  
*seq = SequenceMatcher(lambda x: x == “ “, s1, s2) means the blank spaces will be considered as isjunk, or sometimes we can use it to verify some specific strings, like: seq = SequenceMatcher(lambda x: x in “**“, s1, s2)*

According to the ratio, it will return the sequences' similarity as a float in the range [0, 1]. In principle, the formula for ratio can be defined as:
Ratio = 2.0*M / T
Where T denotes the total number of elements in both sequences, and M is the number of matches. Also, if we’d like to keep the decimal part as we wanted, then it can be changed to (with the above example):
from difflib import SequenceMatcher
s1 = “abcd”
s2 = “bcdf”
seq = SequenceMatcher(None, s1, s2)
ratio = round(seq.ratio(),8)
print(ratio)

Generally, SequenceMatcher() is a very simple but with high confidence rating for the sentence/words similarity.

**Jaccard Index**

Jaccard Index, from the Wikipedia, is known as Jaccard similarity coefficient, which is defined as the size of intersection divided by size of union of two sets. 
The result will be ‘1’ when the two sets are same.





