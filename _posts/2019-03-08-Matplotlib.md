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

As a Python 2D plotting library, Matplotlib provides a MATLAB-like interface. Here we will show some basic plottings in terms of the popular 'pyplot' library. Take the Titanic dataset as example, 

### subplot2grid ###
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

![Alt text](https://oi1126.photobucket.com/albums/l608/zhl/passenger%20info_01_zpsdu1y1xyh.jpg)


```python
    import matplotlib.pyplot as plt
    fig = plt.figure(figsize=(15, 4))
    fig.set() 

    plt.subplot2grid((1,3),(0,0),colspan=2)                ## means 2 images in total, and the first one takes 2 spaces
    data_train.Age[data_train.Pclass==1].plot(kind='kde')
    data_train.Age[data_train.Pclass==2].plot(kind='kde')
    data_train.Age[data_train.Pclass==3].plot(kind='kde')
    plt.xlabel("Age",size=15)
    plt.ylabel("Density",size=15)
    plt.title("Age distribtion in each Class",size=15)
    plt.legend(("P1","P2","P3"),loc='best')

    plt.subplot2grid((1,3),(0,2))
    data_train.Embarked.value_counts().plot(kind='bar')
    plt.ylabel("Number",size=15)
    plt.title("The number in each Embarkation",size=15)
    plt.grid(b=True)
```

![Alt text](https://oi1126.photobucket.com/albums/l608/zhl/passenger%20info_02_zps6gn6jfsx.jpg)
