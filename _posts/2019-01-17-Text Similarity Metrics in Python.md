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


During my master study, I spent nearly 1 year on the research of Recommender Systems(RSs). Based on the current industry research, I proposed 2 papers related to Context-Aware Recommender System (CARS), in terms of two different modeling. We'll focus on this topic to share my understandings for RSs and CARS from academic and practice. With my background in Machine Learning, I'll explain the working of RSs using example and practice.

In this article, we will learn about the traditional RSs and relevant algrithms, creating them in Python from scratch. We will also introduce the evaluation matrics approaches, and finally we will build a recommendation engine/system using matrix factorization.

**Contents**
- What are recommendation engines?
- How does a recommendation engine work?
   1. Data collection
   2. Data storage
   3. Filtering the data
       1. Content based filtering
       2. Collaborative filtering
- Case study in Python using the MovieLens dataset
- Building collaborative filtering model from scratch
- Building Simple popularity and collaborative filtering model using Turicreate
- Introduction to matrix factorization
- Building a recommendation engine using matrix factorization
- Evaluation metrics for recommendation engines
   1. Recall
   2. Precision


