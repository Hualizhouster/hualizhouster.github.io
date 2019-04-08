---
layout:     post                    # 使用的布局（不需要改）
title:      Matplotlib for Data Visualizations              # 标题 
subtitle:     #副标题
date:       2019-03-08              # 时间
author:     Sandy                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Python
---

### As a Python 2D plotting library, Matplotlib provides a MATLAB-like interface.

Here we will show some basic plottings in terms of the popular 'pyplot' library. Take the Titanic dataset as example, 

```python
    import matplotlib.pyplot as plt

    fig = plt.figure(figsize=(16, 4))    ## set the figsize
    fig.set()  

    plt.subplot2grid((1,3),(0,0))         ## subplot2grid is normally used to show the plots by grids     
    data_train.Survived.value_counts().plot(kind='bar') 
    plt.title("Saved Passengers", size=15) 
    plt.ylabel("number",size=10)  
    plt.grid()

    plt.subplot2grid((1,3),(0,1))          ## means have 3 plots and this is the second one
    data_train.Pclass.value_counts().plot(kind="bar")
    plt.ylabel("number",size=10)
    plt.title("Passenger Class",size=15)
    plt.grid()


    plt.subplot2grid((1,3),(0,2))
    plt.scatter(data_train.Survived, data_train.Age)
    plt.ylabel("Age",size=10)                         
    plt.title("Rescuedistribution",size=15)
    plt.grid()
```


