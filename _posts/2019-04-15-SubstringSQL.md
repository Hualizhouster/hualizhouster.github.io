---
layout:     post                    # 使用的布局（不需要改）
title:      Specific Functions in SQL            # 标题 
subtitle:     #副标题
date:       2019-04-15              # 时间
author:     Sandy                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - SQL
---


In this post, we will present some Syntax that used in SQL Server, like SUBSTRING, Len and other regular functions.

**SUBSTRING(string, start, length)**, for each attribute:
1. String is *The string to extract from*;
2. Start is *the start position*;
3. Length is *The number of characters to extract*;

For example (can be found on Hackerrank): Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates. The query can be like this in SQL Server:


```sql
SELECT DISTINCT CITY FROM STATION 
WHERE LOWER(SUBSTRING(CITY, 1, 1)) IN ('a','e','i', 'o','u')

```

