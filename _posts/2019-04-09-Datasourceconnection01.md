---
layout:     post                    # 使用的布局（不需要改）
title:      Retrieving Data From Various Data Sources (01)           # 标题 
subtitle:     #副标题
date:       2019-04-09              # 时间
author:     Sandy                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Python
---


In the Python world, it provides several approaches for connecting data sources, like **.xlsx**, **.csv**, **txt**, or **database** for data retrieving services. Today we will show some regular connecting methods with scripts.

- MS SQL Server for Retrieving Data To List 

Based on research, **Pymssql and Pyhon ODBC** are the basic solutions for connecting to MS SQL Server database. Here we will skip the library and the driver installations, including how to set up your Python environment in VScode, what you can find from Microsoft Offical website. 

As the Pyodbc is a similar library with Pymssql, so we just provide an example of **Pymssql Connecting SQL Server**:

**Step 1**: Connect to the server and database, including server name, user info like ID and PW, and the specific database you want to connect. Particularly, for the server info, we can connect it via IP (port number is optional) or Server Name.

**Step 2**: A connection can have only one cursor with an active query at any time. That means, for each connection, can have a query in progress, so multiple connections can execute multiple conccurent queries, and the fetchall() method of the cursor to recover all the results.

**Step 3**: Remember to close the connection after each execution.

```python
    import pymssql
    conn = pymssql.connect(server = '192.168.0.1', user = '***', password = '***', database = 'aaa')
    cursor1 = conn.cursor()
    cursor1.execute("""SELECT retprod.StoreID AS RetStoreID, retprod.ProductID AS RetProductID, 
                       retprod.ProductName AS RetProductName
                       FROM dbo.tProduct retprod, dbo.tProductSupplier mapping
                       WHERE retprod.ProductID = mapping.ProductId
                       AND mapping.SupplierProductID IS NULL""")
    c1_list = cursor1.fetchall()
    cursor2 = conn.cursor()
    cursor2.execute("""SELECT retprod.StoreID AS RetStoreID, retprod.ProductID AS RetProductID, 
                       retprod.ProductName AS RetProductName
                       FROM dbo.tProduct retprod, dbo.tProductSupplier mapping
                       WHERE retprod.ProductID = mapping.ProductId
                       AND mapping.SupplierProductID IS NULL
                       AND retprod.ProductStatusID!=4
                       AND retprod.StoreID=2""")
    c2_list = cursor2.fetchall()
    conn.close()
```

- MS SQL Server for Retrieving Data To DataFrame 

In this method, the executing results will be presented in terms of **List**, the next we will connect to the database and query the results in terms of Dataframe in Pandas.

```python
    import pymssql
    from pandas import Series, DataFrame
    import numpy
    import pandas as pd

    conn = pymssql.connect(server = '**', user = 'sa', password = '***', database = 'test')

    sql = "select ProductID as ProductCode, GTINCode as RetailerGTIN, SupplierName as RetSupplierName, SupplierProductCode as RetSupplierProductCode, ProductName as RetProductName, upper(ProductName) as RetProdName from dbo.BaysRetailer"    
    df_RetProd = pd.read_sql(sql, conn) 
    df_RetProd.head()
    conn.close()
```
**Reminder:** Close the connection after each execution or will affect the performance of the database. 




