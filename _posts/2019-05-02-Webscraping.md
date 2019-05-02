---
layout:     post                    # 使用的布局（不需要改）
title:      Extracting Place Data and Details From Google Place API            # 标题 
subtitle:      #副标题
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

It's free to apply for the Place API from Google, and will be provided \$300 for one year
1- Login to your [Google Cloud Console](https://console.cloud.google.com/ "Google Cloud Console"). 
2- From top navigation bar by clicking “Select a project”
