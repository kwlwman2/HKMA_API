# HKMA_API
Import Data From HKMA API

I want to try to extract the data from HKMA API and convert the data format into dataframe so that I can do some baisc EDA on the data and plot the data to get some insights

Here are the code for the project

```python

# This example is given by HKMA API, but it is not sufficient enough to do our data analysis. We need to convert it to dataframe format

import urllib.request

url = 'https://api.hkma.gov.hk/public/market-data-and-statistics/monthly-statistical-bulletin/financial/economic-statistics'

with urllib.request.urlopen (url) as req:
    print (req.read())
    
```

I try to optimize the workflow to make sure that it can automate the download and conversion of the data

```python

import pandas as pd

# import requests package
import requests 

# set the url 
url = 'https://api.hkma.gov.hk/public/market-data-and-statistics/monthly-statistical-bulletin/financial/economic-statistics'

# get the url response
r = requests.get(url)

# load it as json-readable format
json_data = r.json()

# results is one of the two keys of the json file, 
# records is also the keys of the results that we target, now we can get the real-time economic data via json format

# get all the data
data = json_data['result']['records']

# get the column headers for the dataframe 
headers = list(data[0].keys())

# set a empty list to store the value
dataList = []

# get the data one by one, and store it as a list in a list
for i in data:
    lista = list(i.values())
    dataList.append(lista)
 
# import the data into DataFrame
df = pd.DataFrame(dataList, columns = headers)

# print(df)
print(df) 

```

For more details, please view my jupyter notebook! Thank you for your time.
