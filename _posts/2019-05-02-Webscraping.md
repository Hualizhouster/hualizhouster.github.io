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

It's free to apply for the Place API from Google, and will be provided \$300 for one year as a new account. Just follow the beloow isntructions to apply:

- Login to your [Google Cloud Console](https://console.cloud.google.com/ "Google Cloud Console"); 
- From top navigation bar by clicking 'Select a project';
- Open 'New project' and create a new one;
- From left side navigation to 'APIs & Services > Library > Place API';
- Click on 'Enable' > 'Create Credentials' then get your API key;
- Ready to copy your key to whatever you want

**Step 2: Build your Place Search Code**

To get place details, firstly we need to search for the location and get the place IDs first. Google provides three approaches for place search: *Find Place, Nearby Search and Text Search*. We will take an example of 'Text Search' as follows:

```python
import requests
import json

URL = ('https://maps.googleapis.com/maps/api/place/textsearch/json?query='text search'&key='your API key'')
r = requests.get(URL)
response = r.text
python_object = json.loads(response)
dataList = python_object.get('results')
length = len(dataList)  

firstDataList = dataList[0:length]
total_results = []
for x in firstDataList:
    print('ADDRESS: ' + x['formatted_address'] + ' ' + 'NAME: '+ x['name'])
```

**Step 3: Get Place Details by Place ID**

Google developers mentioned, *"Once you have a place_id from a Place Search, you can request more details about a particular establishment or point of interest by initiating a Place Details request"*, that means we can build another function in terms of place_id and Place Details request.


```python
URL_maps = ('https://maps.googleapis.com/maps/api/place/textsearch/json?query='text search'&key='your API key'')
r = requests.get(URL)
response = r.text
python_object = json.loads(response)
dataList = python_object.get('results')
length = len(dataList) 
DataDetail = dataList[0:length]
for x in DataDetail:
     URL_id = 'https://maps.googleapis.com/maps/api/place/details/json?placeid={palceid}&fields=name,website,rating,formatted_phone_number&key='your API key''.format(palceid=x['place_id'])
     detailResponse=requests.get(URL_id)
     detailInfo = detailResponse.text
     detailInfoPython = json.loads(detailInfo)
     datadetailList = detailInfoPython.get('result')
     print(datadetailList)
```

**Step 4: Retrieving results to SQL Server database**

Once the Function for Place Search and Place Details finished, following we can decide to retrive the results as '.csv', '.txt' or to database as we mentioned in the previous post [Retrieving Data From Various Data Sources](https://hualizhouster.github.io/2019/04/09/Datasourceconnection/ "Retrieving Data From Various Data Sources").  

```sql
def adddatatoDB(keywords,name, address, phone_number, website, rating):
    conn = pymssql.connect('server name', 'user name', 'password', 'database')
    cursor = conn.cursor()
    cursor.executemany("INSERT INTO automotive(keywords,name, address, phone_number, website, rating) VALUES (%s, %s, %s, %s,%s, %s)", 
    [(keywords,name, address, phone_number,website, rating)])
    conn.commit()
    conn.close() 
```


**Final Step: Limitations and Completed Scripts**

Till now, we nearly complete the code for scraping the place info from Google Place API, WHILE there are some limitations to this API, that is to say, for each request, Google only returns a maximum of 60 results (see Google's answer). And These results are split into 20 results per page. If a request has more than 20 results, you’ll need to use the “next_page_token” method. Furthermore, if you need to request the next page of results, there is a short delay (nearly one second) before the token becomes valid.

![Alt text](https://i1126.photobucket.com/albums/l608/zhl/image_zpsjzzsaklg.png)


Finally I will put the completed code for any coders who like it, and thanks for some ideas from [GoTrained Python](https://python.gotrained.com/ "GoTrained Python") and [GoFishDigital](https://gofishdigital.com/local-link-building-python-places-api/ "GoFishDigital").

```python
import requests
import json
import time
import pymssql

api_key = 'your API key' 
fields2 ='name, website, rating, formatted_phone_number'
total_results = []


def adddatatoDB(keywords,name, address, phone_number, website, rating):
    conn = pymssql.connect('server name', 'user name', 'password', 'database')
    cursor = conn.cursor()
    cursor.executemany("INSERT INTO automotive(keywords,name, address, phone_number, website, rating) VALUES (%s, %s, %s, %s,%s, %s)", 
    [(keywords,name, address, phone_number,website, rating)])
    conn.commit()
    conn.close()       



def get_details(place_id):
    r = requests.get('https://maps.googleapis.com/maps/api/place/details/json?placeid={palceid}&fields={fields1}&key={key}'.format(palceid=place_id,fields1=fields2,key=api_key))
    response = r.text
    python_object = json.loads(response)
    try:
        place_details = python_object["result"]
        if 'website' in place_details:
            return (place_details['formatted_phone_number'],place_details['website'])
        else:
            return (place_details['formatted_phone_number'],"no website listed in API")
    except:
        print("error getting place details")
     
        
def get_places(business_type, next_page):
    URL = ('https://maps.googleapis.com/maps/api/place/textsearch/json?query='+ business_type + '&pagetoken=' + next_page + '&key='+ api_key)
    r = requests.get(URL)
    response = r.text
    python_object = json.loads(response)
    results = python_object['results']
 
    for result in results:
        place_id = result['place_id']
        rating = str(result['rating'])
        address = result['formatted_address'] 
        name = result['name'] 
        (phone_number,website) = get_details(place_id)
        # company name, address, phone number, url, and rating
        #total_results.append([name, address, phone_number, website, rating])
        #print(total_results)
        adddatatoDB(business_type, name, address, phone_number, website, rating)
        
    try:
        next_page_token = python_object["next_page_token"]
    except KeyError:
         #no next page
        return
    
    time.sleep(1)
    get_places(business_type, next_page_token) 
## your input info    
get_places('automotive parts Irving Texas', '')
```

