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



**Python** provides an inbuilt function for creating, writing and reading files. In this post we first introduce the various mode of reading, writing and appending, then will give some examples on how to write to text files or database aa outputs.

- File Access Modes

Access modes refers to how the file will be used once its opened. These modes also define the location of the File Handle in the file. File handle is like a cursor, which defines from where the data has to be read or written in the file. There are 6 access modes in python:

| Mode | Function | Description |

| 'r' | Read Only | This is the default mode. It Opens file for reading. |
| 'r+' | Read and Write | The handle is positioned at the beginning of the file. Raises I/O error if the file does not exists. |
| 'w' | Write Only | For existing file, the data is truncated and over-written. The handle is positioned at the beginning of the file. Creates the file if the file does not exists. |
| 'w+' | Write and Read | For existing file, data is truncated and over-written. The handle is positioned at the beginning of the file. |
| 'a' | Append Only | The file is created if it does not exist. The handle is positioned at the end of the file. The data being written will be inserted at the end, after the existing data. |
| 'a+' | Append and Read  | The file is created if it does not exist. The handle is positioned at the end of the file. The data being written will be inserted at the end, after the existing data. |

- Output / Write as the 'Text' file

```python

    filename ='mappingresults.txt'
    for i in df_retailer.index:
        for j in df_supplier.index:
            ratio = SequenceMatcher(None, df_retailer['Trade Name'][i], df_supplier['Product Name'][j]).ratio()
            if (ratio >= 0.75) and (ratio <= 0.9):
                with open(filename,'a') as file_object:
                    file_object.write(str(df_retailer['Index(Original)'][i]) + ';'
                                      + str(df_retailer['Trade Name'][i]) + ';'
                                      + str(df_supplier['Index'][j]) + ';'
                                      + df_supplier['Product Name'][j] + ';' + str(ratio) + '\n')

```
