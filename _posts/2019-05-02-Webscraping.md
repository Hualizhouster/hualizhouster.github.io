---
layout:     post                    # 使用的布局（不需要改）
title:      Google Places API             # 标题 
subtitle:   Extracting Place Data & Details with Python   #副标题
date:       2019-05-02              # 时间
author:     Sandy                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Web Scraping
    - Python
    - SQL  
---


Recently I am starting a new project on extracting data from websites like Google Maps. As we know, Google has heaps API that allows developers to access, for example, Google Place API is a helful resource with over 100 million places for developers, including place search, place details, photos, user ratings and reviews and more.

In this post, I will SHARE how to build the Function with Python by using a few modules: **requests, json, time and pymssql**, mainly to extract business’s name, address, phone number, website, and rating from Google Places API. 

The contents will be included:

- How to get an API key;
- Places search;
- Places details;
- Retrieving results to database;
- Limitations

**Step 1: How to get an API key**
