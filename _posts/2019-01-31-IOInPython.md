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

- Output / Write to Database (SQL Server as example)

**Step 1**: Ensure you already have a table in your aimed database, creating the table like this:

```sql
CREATE TABLE test.dbo.MappingResult (
	ID int IDENTITY(1,1) NOT NULL,
	ProductCode varchar(120) NULL,
	RetProdName varchar(255) NULL,
	RetailerGTIN nvarchar(200) NULL,
	RetSupplierProductCode varchar(120) NULL,
	RetSupplierName varchar(255) NULL,
	SupSupplierProductCode varchar(120) NULL,
	SupProdName varchar(255) NULL,
	SupplierGTIN nvarchar(200) NULL,
	SupplierName varchar(255) NULL,
	Imagepath varchar(200) NULL,
	Ratio float NULL,
	Editor varchar(255) NULL,
	cdate datetime DEFAULT getdate() NULL,
	ApproveStatus bit NULL,
	Reject bit NULL, 
)
```

**Step 2**:  Define a connection to your table and database, choose *executemany* to insert the values to your database, like this:

```python
## Define a function 
    def WriteDatatoDB(ProductCode, RetProdName, RetailerGTIN, RetSupplierProductCode, RetSupplierName, SupSupplierProductCode, SupProdName, SupplierGTIN, SupplierName, Ratio):
        conn = pymssql.connect(server, user, password, database) ## input your db info
        cursor = conn.cursor()
        cursor.executemany("INSERT INTO dbo.MappingResult (ProductCode, RetProdName, RetailerGTIN, RetSupplierProductCode, RetSupplierName, SupSupplierProductCode, SupProdName, SupplierGTIN, SupplierName, Ratio) VALUES (%d, %s, %d, %d, %s, %d, %s, %d, %s, %d)", 
        [(ProductCode, RetProdName, RetailerGTIN, RetSupplierProductCode, RetSupplierName, SupSupplierProductCode, SupProdName, SupplierGTIN, SupplierName, Ratio)])    
        conn.commit()
        conn.close()
```

**Step 3**: Write the execution results to your database.

```python
    for i in df_RetProd.index:
        for j in df_SupProd.index:
            ratio = round(SequenceMatcher(lambda x: x == " ", df_RetProd['NewName'][i], df_SupProd['NewSupProdName'][j]).ratio(),4)
            if ratio >= 0.65:
                if len(re.findall(r"\d+\.?\d*", df_RetProd['NewName'][i])) == len(re.findall(r"\d+\.?\d*",df_SupProd['SupProdName'][j])):
                    if (operator.eq(re.findall(r"\d+\.?\d*", df_RetProd['NewName'][i]), re.findall(r"\d+\.?\d*", df_SupProd['SupProdName'][j])) == False):
                        ratio = ratio * 0.7
                    else:
                        ratio = ratio
                else:
                    ration = ratio
                WriteDatatoDB(str(df_RetProd['ProductCode'][i]), str(df_RetProd['RetProductName'][i]),
                              str(df_RetProd['RetailerGTIN'][i]), str(df_RetProd['RetSupplierProductCode'][i]),
                              str(df_RetProd['RetSupplierName'][i]),
                              str(df_SupProd['SupSupplierProductCode'][j]), str(df_SupProd['SupProductName'][j]), 
                              str(df_SupProd['SupplierGTIN'][j]), str(df_SupProd['SupplierName'][j]), str(ratio))
 ```                         
