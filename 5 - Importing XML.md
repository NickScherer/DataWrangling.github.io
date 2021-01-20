# 5 - Importing XML
In this fifth step I'll show you how to import and parse the XML data.


```python
import pandas as pd
import xml.etree.ElementTree as ET

tree = ET.parse("data-set.xml")
root = tree.getroot()

print(root.tag)
```

    data-set
    

Taking a look we can see that the root tag is <code>data-set</code>.


```python
print(root[0].tag)
```

    record
    

The next child sub element tag is <code>record</code>.


```python
# How many child elements?

child_tags = []
for child in root:
    child_tags.append(child.tag)

len(child_tags)
```




    50



Looping through all of the <code>record</code> children sub element tags, we can see that we have 50. This corresponds to 50 records of data.

Let's take a look at the children element tags contained in <code>record</code>.


```python
print(root[0][0].tag)
```

    City
    

Taking a quick look, we can see that the first is <code>City</code>. Let's look for all of the tags, as well as their corresponding data.


```python
for child in root[0]:
    print(child.tag, child.text)
```

    City New York City
    Zipcode 10012
    Latitude_Longitude 40.726,-73.998
    

Taking a look we can see that our first record contains <code>City</code>, <code>Zipcode</code>, and <code>Latitude_Longitude</code> tags.

The data in these tags is <code>New York City</code>, <code>10012</code>, and <code>40.726,-73.998</code>.

If we open up the <code>data-set.xml</code> file in a text editor, we can confirm that this is in fact the first record.

Let's start parsing and gathering all of the data. We'll start by making a list of the tags to use for the columns.


```python
# getting all of the child tags for column names

names = []

for child in root[0]:
    names.append(child.tag)

print(names)
```

    ['City', 'Zipcode', 'Latitude_Longitude']
    

Next, let's gather all of the data.

We'll create a dictionary using the list entries <code>['City', 'Zipcode', 'Latitude_Longitude']</code> as the keys. These will be our columns.

We'll collect the actual data using lists. These lists will be the values in our dictionary. 


```python
# creating the dictionary to build the columns

d = {}


# using the sub children tags as the dictionary keys

for i in range(0,len(names)):
    d[names[i]] = []
#print(d)


# collecting all of the data

for i in range(0,50):
    for j in range(0,3):
        #print(root[i][j].text)
        value = root[i][j].text
        d[names[j]].append(value)

print(d)
```

    {'City': ['New York City', 'New York City', 'New York City', 'New York City', 'New York City', 'Los Angeles', 'Los Angeles', 'Los Angeles', 'Los Angeles', 'Los Angeles', 'Chicago', 'Chicago', 'Chicago', 'Chicago', 'Chicago', 'Houston', 'Houston', 'Houston', 'Houston', 'Houston', 'Philadelphia', 'Philadelphia', 'Philadelphia', 'Philadelphia', 'Philadelphia', 'Phoenix', 'Phoenix', 'Phoenix', 'Phoenix', 'Phoenix', 'San Antonio', 'San Antonio', 'San Antonio', 'San Antonio', 'San Antonio', 'San Diego', 'San Diego', 'San Diego', 'San Diego', 'San Diego', 'Dallas', 'Dallas', 'Dallas', 'Dallas', 'Dallas', 'San Jose', 'San Jose', 'San Jose', 'San Jose', 'San Jose'], 'Zipcode': ['10012', '10013', '10004', '10128', '10002', '90001', '90016', '90008', '90020', '90029', '60610', '60611', '60605', '60602', '60603', '77001', '77005', '77009', '77004', '77012', '19019', '19102', '19110', '19115', '19118', '85001', '85004', '85015', '85019', '85027', '78006', '78109', '78206', '78214', '78073', '91911', '92037', '92102', '92107', '92027', '75001', '75043', '75063', '75089', '75126', '94088', '95002', '95103', '95115', '94560'], 'Latitude_Longitude': ['40.726,-73.998', '40.721,-74.005', '40.699,-74.041', '40.782,-73.95', '40.717,-73.987', '33.973,-118.249', '34.03,-118.353', '34.01,-118.337', '34.066,-118.309', '34.09,-118.295', '41.899,-87.637', '41.905,-87.625', '41.86,-87.619', '41.883,-87.629', '41.88,-87.63', '29.813,-95.31', '29.718,-95.428', '29.793,-95.367', '29.729,-95.366', '29.72,-95.279', '40.002,-75.118', '39.953,-75.166', '39.95,-75.164', '40.093,-75.041', '40.072,-75.208', '33.704,-112.352', '33.451,-112.071', '33.507,-112.103', '33.512,-112.142', '33.699,-112.114', '29.852,-98.729', '29.502,-98.306', '29.438,-98.462', '29.363,-98.49', '29.227,-98.609', '32.609,-117.061', '32.839,-117.262', '32.715,-117.125', '32.741,-117.244', '33.143,-117.03', '32.961,-96.838', '32.855,-96.602', '32.917,-96.973', '32.924,-96.547', '32.745,-96.46', '37.189,-121.705', '37.427,-121.975', '37.189,-121.705', '37.189,-121.705', '37.536,-122.034']}
    

The final step is to convert the dictionary to a dataframe with Pandas.


```python
df = pd.DataFrame(data=d)
print(df)
```

                 City Zipcode Latitude_Longitude
    0   New York City   10012     40.726,-73.998
    1   New York City   10013     40.721,-74.005
    2   New York City   10004     40.699,-74.041
    3   New York City   10128      40.782,-73.95
    4   New York City   10002     40.717,-73.987
    5     Los Angeles   90001    33.973,-118.249
    6     Los Angeles   90016     34.03,-118.353
    7     Los Angeles   90008     34.01,-118.337
    8     Los Angeles   90020    34.066,-118.309
    9     Los Angeles   90029     34.09,-118.295
    10        Chicago   60610     41.899,-87.637
    11        Chicago   60611     41.905,-87.625
    12        Chicago   60605      41.86,-87.619
    13        Chicago   60602     41.883,-87.629
    14        Chicago   60603       41.88,-87.63
    15        Houston   77001      29.813,-95.31
    16        Houston   77005     29.718,-95.428
    17        Houston   77009     29.793,-95.367
    18        Houston   77004     29.729,-95.366
    19        Houston   77012      29.72,-95.279
    20   Philadelphia   19019     40.002,-75.118
    21   Philadelphia   19102     39.953,-75.166
    22   Philadelphia   19110      39.95,-75.164
    23   Philadelphia   19115     40.093,-75.041
    24   Philadelphia   19118     40.072,-75.208
    25        Phoenix   85001    33.704,-112.352
    26        Phoenix   85004    33.451,-112.071
    27        Phoenix   85015    33.507,-112.103
    28        Phoenix   85019    33.512,-112.142
    29        Phoenix   85027    33.699,-112.114
    30    San Antonio   78006     29.852,-98.729
    31    San Antonio   78109     29.502,-98.306
    32    San Antonio   78206     29.438,-98.462
    33    San Antonio   78214      29.363,-98.49
    34    San Antonio   78073     29.227,-98.609
    35      San Diego   91911    32.609,-117.061
    36      San Diego   92037    32.839,-117.262
    37      San Diego   92102    32.715,-117.125
    38      San Diego   92107    32.741,-117.244
    39      San Diego   92027     33.143,-117.03
    40         Dallas   75001     32.961,-96.838
    41         Dallas   75043     32.855,-96.602
    42         Dallas   75063     32.917,-96.973
    43         Dallas   75089     32.924,-96.547
    44         Dallas   75126      32.745,-96.46
    45       San Jose   94088    37.189,-121.705
    46       San Jose   95002    37.427,-121.975
    47       San Jose   95103    37.189,-121.705
    48       San Jose   95115    37.189,-121.705
    49       San Jose   94560    37.536,-122.034
    
