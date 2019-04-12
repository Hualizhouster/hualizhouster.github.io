---
layout:     post                    # 使用的布局（不需要改）
title:      Write Files to Text or Database in Python             # 标题 
subtitle:     #副标题
date:       2019-01-31              # 时间
author:     Sandy                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Python
---



## Python ## provides an inbuilt function for creating, writing and reading files.

| Mode | Function | Description |

| 'r' | Read Only | This is the default mode. It Opens file for reading. |
| 'r+' | Read and Write | The handle is positioned at the beginning of the file. Raises I/O error if the file does not exists. |
| 'w' | Write Only | For existing file, the data is truncated and over-written. The handle is positioned at the beginning of the file. Creates the file if the file does not exists. |
| 'w+' | Write and Read | For existing file, data is truncated and over-written. The handle is positioned at the beginning of the file. |
| 'a' | Append Only | The file is created if it does not exist. The handle is positioned at the end of the file. The data being written will be inserted at the end, after the existing data. |
| 'a+' | Append and Read  | The file is created if it does not exist. The handle is positioned at the end of the file. The data being written will be inserted at the end, after the existing data. |
