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

**Contents**
- SequenceMatcher function
- Jaccard Index



