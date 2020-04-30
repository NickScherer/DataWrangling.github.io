# 1 - Consistent Dates
In this first Step I'll show you how to create consistent dates. You will always see: comment, then Python coding and follwed the results.


```python
import pandas as pd
import datetime

df = pd.read_json("customer_data.json")
```

Taking a quick look at the data with the <code>.head()</code> method.


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>amount</th>
      <th>category</th>
      <th>city</th>
      <th>customer_id</th>
      <th>date</th>
      <th>frequently_bought_together</th>
      <th>lat_lon</th>
      <th>purchase</th>
      <th>related_items</th>
      <th>state</th>
      <th>zip_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>24.64</td>
      <td>household</td>
      <td>Chicago</td>
      <td>100191</td>
      <td>2014-01-01</td>
      <td>towels</td>
      <td>41.86,-87.619</td>
      <td>soap</td>
      <td>towels</td>
      <td>IL</td>
      <td>60605</td>
    </tr>
    <tr>
      <th>1</th>
      <td>35</td>
      <td>clothing</td>
      <td>Dallas</td>
      <td>100199</td>
      <td>2014-01-02</td>
      <td>sandals</td>
      <td>32.924,-96.547</td>
      <td>shorts</td>
      <td>belts</td>
      <td>TX</td>
      <td>75089</td>
    </tr>
    <tr>
      <th>2</th>
      <td>89.72</td>
      <td>outdoor</td>
      <td>Philadelphia</td>
      <td>100170</td>
      <td>2014-01-03</td>
      <td>lawn bags</td>
      <td>40.002,-75.118</td>
      <td>lawn_mower</td>
      <td>shovels</td>
      <td>PA</td>
      <td>19019</td>
    </tr>
    <tr>
      <th>3</th>
      <td>51.32</td>
      <td>electronics</td>
      <td>Chicago</td>
      <td>100124</td>
      <td>2014-01-04</td>
      <td>headphones</td>
      <td>41.88,-87.63</td>
      <td>laptop</td>
      <td>headphones</td>
      <td>IL</td>
      <td>60603</td>
    </tr>
    <tr>
      <th>4</th>
      <td>81.75</td>
      <td>outdoor</td>
      <td>Philadelphia</td>
      <td>100173</td>
      <td>2014-01-05</td>
      <td>sponge</td>
      <td>39.953,-75.166</td>
      <td>car wash</td>
      <td>sponge</td>
      <td>PA</td>
      <td>19102</td>
    </tr>
  </tbody>
</table>
</div>



The original date format was changed, but I want to keep the original format. 

I'll import the data again, but this time set the <code>convert_dates</code> parameter to False.


```python
df = pd.read_json("customer_data.json", convert_dates=False)
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>amount</th>
      <th>category</th>
      <th>city</th>
      <th>customer_id</th>
      <th>date</th>
      <th>frequently_bought_together</th>
      <th>lat_lon</th>
      <th>purchase</th>
      <th>related_items</th>
      <th>state</th>
      <th>zip_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>24.64</td>
      <td>household</td>
      <td>Chicago</td>
      <td>100191</td>
      <td>1-Jan-14</td>
      <td>towels</td>
      <td>41.86,-87.619</td>
      <td>soap</td>
      <td>towels</td>
      <td>IL</td>
      <td>60605</td>
    </tr>
    <tr>
      <th>1</th>
      <td>35</td>
      <td>clothing</td>
      <td>Dallas</td>
      <td>100199</td>
      <td>2-Jan-14</td>
      <td>sandals</td>
      <td>32.924,-96.547</td>
      <td>shorts</td>
      <td>belts</td>
      <td>TX</td>
      <td>75089</td>
    </tr>
    <tr>
      <th>2</th>
      <td>89.72</td>
      <td>outdoor</td>
      <td>Philadelphia</td>
      <td>100170</td>
      <td>3-Jan-14</td>
      <td>lawn bags</td>
      <td>40.002,-75.118</td>
      <td>lawn_mower</td>
      <td>shovels</td>
      <td>PA</td>
      <td>19019</td>
    </tr>
    <tr>
      <th>3</th>
      <td>51.32</td>
      <td>electronics</td>
      <td>Chicago</td>
      <td>100124</td>
      <td>4-Jan-14</td>
      <td>headphones</td>
      <td>41.88,-87.63</td>
      <td>laptop</td>
      <td>headphones</td>
      <td>IL</td>
      <td>60603</td>
    </tr>
    <tr>
      <th>4</th>
      <td>81.75</td>
      <td>outdoor</td>
      <td>Philadelphia</td>
      <td>100173</td>
      <td>5-Jan-14</td>
      <td>sponge</td>
      <td>39.953,-75.166</td>
      <td>car wash</td>
      <td>sponge</td>
      <td>PA</td>
      <td>19102</td>
    </tr>
  </tbody>
</table>
</div>



It looks like the dates are in the day-month-year <code>%d-%b-%y</code> format. We can confirm this using the datetime method <code>.strptime()</code> which creates a datetime object.


```python
y = df.iloc[0]['date']
print(y)

# this is a datetime object
datetime.datetime.strptime(y, '%d-%b-%y')
```

    1-Jan-14
    




    datetime.datetime(2014, 1, 1, 0, 0)



If the date entry does not match this format, we'll get a <code>ValueError</code>.


```python
# example of an inconsistent date format
x = '1-January-2014'

# this is a datetime object
datetime.datetime.strptime(x, '%d-%b-%y')
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-5-b66fd0cbe194> in <module>()
          2 
          3 # this is a datetime object
    ----> 4 datetime.datetime.strptime(x, '%d-%b-%y')
    

    ~\AppData\Local\Continuum\anaconda3\lib\_strptime.py in _strptime_datetime(cls, data_string, format)
        563     """Return a class cls instance based on the input string and the
        564     format string."""
    --> 565     tt, fraction = _strptime(data_string, format)
        566     tzname, gmtoff = tt[-2:]
        567     args = tt[:6] + (fraction,)
    

    ~\AppData\Local\Continuum\anaconda3\lib\_strptime.py in _strptime(data_string, format)
        360     if not found:
        361         raise ValueError("time data %r does not match format %r" %
    --> 362                          (data_string, format))
        363     if len(data_string) != found.end():
        364         raise ValueError("unconverted data remains: %s" %
    

    ValueError: time data '1-January-2014' does not match format '%d-%b-%y'


We can use the <code>.strptime()</code> method to check our date formats. If we get an error, we can collect those dates for later on. I'll also collect the index location.


```python
cnt = 0
dates={}

for date in df["date"]:
    try:
        datetime.datetime.strptime(date, '%d-%b-%y')
    except ValueError:
        dates[cnt] = date
    cnt+=1
    
dates
```




    {98: '9-April-2014',
     99: '10-April-2014',
     100: '11-April-2014',
     101: '12-April-2014',
     102: '13-April-2014',
     103: '14-April-2014',
     104: '15-April-2014',
     105: '16-April-2014',
     106: '17-April-2014',
     107: '18-April-2014',
     108: '19-April-2014',
     151: '6/1/2014',
     152: '6/2/2014',
     153: '6/3/2014',
     154: '6/4/2014',
     155: '6/5/2014',
     156: '6/6/2014',
     157: '6/7/2014',
     158: '6/8/2014',
     159: '6/9/2014',
     160: '6/10/2014',
     161: '6/11/2014',
     243: '1-Sep-2014',
     244: '2-Sep-2014',
     245: '3-Sep-2014',
     246: '4-Sep-2014',
     247: '5-Sep-2014',
     248: '6-Sep-2014',
     249: '7-Sep-2014',
     250: '8-Sep-2014',
     251: '9-Sep-2014',
     252: '10-Sep-2014',
     253: '11-Sep-2014',
     254: '12-Sep-2014',
     255: '13-Sep-2014',
     283: '10/11/2014',
     284: '10/12/2014',
     285: '10/13/2014',
     286: '10/14/2014',
     287: '10/15/2014',
     288: '10/16/2014',
     289: '10/17/2014',
     290: '10/18/2014',
     291: '10/19/2014',
     292: '10/20/2014',
     293: '10/21/2014',
     294: '10/22/2014',
     295: '10/23/2014',
     296: '10/24/2014',
     297: '10/25/2014',
     298: '10/26/2014',
     299: '10/27/2014',
     300: '10/28/2014',
     301: '10/29/2014',
     302: '10/30/2014',
     303: '10/31/2014',
     304: '11/1/2014',
     305: '11/2/2014',
     306: '11/3/2014',
     307: '11/4/2014',
     308: '11/5/2014',
     309: '11/6/2014',
     577: '1-August-2015',
     578: '2-August-2015',
     579: '3-August-2015',
     580: '4-August-2015',
     581: '5-August-2015',
     582: '6-August-2015',
     583: '7-August-2015',
     584: '8-August-2015',
     585: '9-August-2015',
     586: '10-August-2015',
     587: '11-August-2015',
     588: '12-August-2015',
     589: '13-August-2015',
     590: '14-August-2015',
     591: '15-August-2015',
     799: '3/10/16',
     800: '3/11/16',
     801: '3/12/16',
     802: '3/13/16',
     803: '3/14/16',
     804: '3/15/16',
     805: '3/16/16',
     806: '3/17/16',
     807: '3/18/16',
     808: '3/19/16',
     809: '3/20/16',
     810: '3/21/16',
     1127: '2/1/2017',
     1128: '2/2/2017',
     1129: '2/3/2017',
     1130: '2/4/2017',
     1131: '2/5/2017',
     1132: '2/6/2017',
     1133: '2/7/2017',
     1134: '2/8/2017',
     1135: '2/9/2017',
     1136: '2/10/2017',
     1137: '2/11/2017',
     1138: '2/12/2017',
     1139: '2/13/2017',
     1140: '2/14/2017',
     1141: '2/15/2017',
     1142: '2/16/2017',
     1143: '2/17/2017',
     1144: '2/18/2017',
     1664: '7/23/2018',
     1665: '7/24/2018',
     1666: '7/25/2018',
     1667: '7/26/2018',
     1668: '7/27/2018',
     1669: '7/28/2018',
     1670: '7/29/2018',
     1671: '7/30/2018',
     1672: '7/31/2018',
     1673: '8/1/2018',
     1674: '8/2/2018',
     1675: '8/3/2018',
     1916: '4/1/2019',
     1917: '4/2/2019',
     1918: '4/3/2019',
     1919: '4/4/2019',
     1920: '4/5/2019',
     1921: '4/6/2019',
     1922: '4/7/2019',
     1963: '5/18/2019',
     1964: '5/19/2019',
     1965: '5/20/2019',
     1966: '5/21/2019',
     1967: '5/22/2019',
     1968: '5/23/2019',
     1969: '5/24/2019',
     1970: '5/25/2019',
     1971: '5/26/2019',
     1972: '5/27/2019',
     1973: '5/28/2019',
     1974: '5/29/2019',
     1975: '5/30/2019',
     1976: '5/31/2019'}



We have dates in multipe formats. I'll clean the day-Month-Year <code>%d-%B-%Y</code> format as an example. We can see that the entries for April 1st 2014 through April 10th 2014 are in this format. These are in row index 98 through row index 108.


```python
df[98:109]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>amount</th>
      <th>category</th>
      <th>city</th>
      <th>customer_id</th>
      <th>date</th>
      <th>frequently_bought_together</th>
      <th>lat_lon</th>
      <th>purchase</th>
      <th>related_items</th>
      <th>state</th>
      <th>zip_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>98</th>
      <td>61.33</td>
      <td>electronics</td>
      <td>Dallas</td>
      <td>100190</td>
      <td>9-April-2014</td>
      <td>dvd player</td>
      <td>32.924,-96.547</td>
      <td>tv</td>
      <td>speakers</td>
      <td>TX</td>
      <td>75089</td>
    </tr>
    <tr>
      <th>99</th>
      <td>90.48</td>
      <td>household</td>
      <td>Dallas</td>
      <td>100152</td>
      <td>10-April-2014</td>
      <td>drills</td>
      <td>32.745,-96.46</td>
      <td>tools</td>
      <td>hammers</td>
      <td>TX</td>
      <td>75126</td>
    </tr>
    <tr>
      <th>100</th>
      <td>86.52</td>
      <td>appliances</td>
      <td>Houston</td>
      <td>100103</td>
      <td>11-April-2014</td>
      <td>cookbook</td>
      <td>29.72,-95.279</td>
      <td>slow cooker</td>
      <td>pot holders</td>
      <td>TX</td>
      <td>77012</td>
    </tr>
    <tr>
      <th>101</th>
      <td>67.2</td>
      <td>electronics</td>
      <td>Philadelphia</td>
      <td>100194</td>
      <td>12-April-2014</td>
      <td>lens cleaner</td>
      <td>40.093,-75.041</td>
      <td>camera</td>
      <td>editing software</td>
      <td>PA</td>
      <td>19115</td>
    </tr>
    <tr>
      <th>102</th>
      <td>25.83</td>
      <td>appliances</td>
      <td>San Diego</td>
      <td>100130</td>
      <td>13-April-2014</td>
      <td>fruit</td>
      <td>32.741,-117.244</td>
      <td>blender</td>
      <td>pitcher</td>
      <td>CA</td>
      <td>92107</td>
    </tr>
    <tr>
      <th>103</th>
      <td>50.12</td>
      <td>outdoor</td>
      <td>Dallas</td>
      <td>100152</td>
      <td>14-April-2014</td>
      <td>wax</td>
      <td>32.745,-96.46</td>
      <td>car wash</td>
      <td>tire cleaner</td>
      <td>TX</td>
      <td>75126</td>
    </tr>
    <tr>
      <th>104</th>
      <td>53.09</td>
      <td>clothing</td>
      <td>San Diego</td>
      <td>100140</td>
      <td>15-April-2014</td>
      <td>button down shirt</td>
      <td>32.839,-117.262</td>
      <td>shirts</td>
      <td>t-shirt</td>
      <td>CA</td>
      <td>92037</td>
    </tr>
    <tr>
      <th>105</th>
      <td>32.78</td>
      <td>household</td>
      <td>San Jose</td>
      <td>100172</td>
      <td>16-April-2014</td>
      <td>shampoo</td>
      <td>37.189,-121.705</td>
      <td>soap</td>
      <td>body wash</td>
      <td>CA</td>
      <td>95103</td>
    </tr>
    <tr>
      <th>106</th>
      <td>70.07</td>
      <td>clothing</td>
      <td>Dallas</td>
      <td>100152</td>
      <td>17-April-2014</td>
      <td>belt</td>
      <td>32.745,-96.46</td>
      <td>pants</td>
      <td>jeans</td>
      <td>TX</td>
      <td>75126</td>
    </tr>
    <tr>
      <th>107</th>
      <td>53.92</td>
      <td>appliances</td>
      <td>New York City</td>
      <td>100181</td>
      <td>18-April-2014</td>
      <td>peanut butter</td>
      <td>40.699,-74.041</td>
      <td>toaster</td>
      <td>butter</td>
      <td>NY</td>
      <td>10004</td>
    </tr>
    <tr>
      <th>108</th>
      <td>99.06</td>
      <td>outdoor</td>
      <td>Philadelphia</td>
      <td>100173</td>
      <td>19-April-2014</td>
      <td>gloves</td>
      <td>39.953,-75.166</td>
      <td>snow shovel</td>
      <td>sand</td>
      <td>PA</td>
      <td>19102</td>
    </tr>
  </tbody>
</table>
</div>



We can clean these by applying the <code>.strftime()</code> method.


```python
cnt = 0

for date in df["date"]:
    try:
        x = datetime.datetime.strptime(date, '%d-%B-%Y').strftime('%d-%b-%y')
        df.loc[cnt, "date"] = x
    except ValueError:
        pass
    cnt+=1
```


```python
df[98:109]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>amount</th>
      <th>category</th>
      <th>city</th>
      <th>customer_id</th>
      <th>date</th>
      <th>frequently_bought_together</th>
      <th>lat_lon</th>
      <th>purchase</th>
      <th>related_items</th>
      <th>state</th>
      <th>zip_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>98</th>
      <td>61.33</td>
      <td>electronics</td>
      <td>Dallas</td>
      <td>100190</td>
      <td>09-Apr-14</td>
      <td>dvd player</td>
      <td>32.924,-96.547</td>
      <td>tv</td>
      <td>speakers</td>
      <td>TX</td>
      <td>75089</td>
    </tr>
    <tr>
      <th>99</th>
      <td>90.48</td>
      <td>household</td>
      <td>Dallas</td>
      <td>100152</td>
      <td>10-Apr-14</td>
      <td>drills</td>
      <td>32.745,-96.46</td>
      <td>tools</td>
      <td>hammers</td>
      <td>TX</td>
      <td>75126</td>
    </tr>
    <tr>
      <th>100</th>
      <td>86.52</td>
      <td>appliances</td>
      <td>Houston</td>
      <td>100103</td>
      <td>11-Apr-14</td>
      <td>cookbook</td>
      <td>29.72,-95.279</td>
      <td>slow cooker</td>
      <td>pot holders</td>
      <td>TX</td>
      <td>77012</td>
    </tr>
    <tr>
      <th>101</th>
      <td>67.2</td>
      <td>electronics</td>
      <td>Philadelphia</td>
      <td>100194</td>
      <td>12-Apr-14</td>
      <td>lens cleaner</td>
      <td>40.093,-75.041</td>
      <td>camera</td>
      <td>editing software</td>
      <td>PA</td>
      <td>19115</td>
    </tr>
    <tr>
      <th>102</th>
      <td>25.83</td>
      <td>appliances</td>
      <td>San Diego</td>
      <td>100130</td>
      <td>13-Apr-14</td>
      <td>fruit</td>
      <td>32.741,-117.244</td>
      <td>blender</td>
      <td>pitcher</td>
      <td>CA</td>
      <td>92107</td>
    </tr>
    <tr>
      <th>103</th>
      <td>50.12</td>
      <td>outdoor</td>
      <td>Dallas</td>
      <td>100152</td>
      <td>14-Apr-14</td>
      <td>wax</td>
      <td>32.745,-96.46</td>
      <td>car wash</td>
      <td>tire cleaner</td>
      <td>TX</td>
      <td>75126</td>
    </tr>
    <tr>
      <th>104</th>
      <td>53.09</td>
      <td>clothing</td>
      <td>San Diego</td>
      <td>100140</td>
      <td>15-Apr-14</td>
      <td>button down shirt</td>
      <td>32.839,-117.262</td>
      <td>shirts</td>
      <td>t-shirt</td>
      <td>CA</td>
      <td>92037</td>
    </tr>
    <tr>
      <th>105</th>
      <td>32.78</td>
      <td>household</td>
      <td>San Jose</td>
      <td>100172</td>
      <td>16-Apr-14</td>
      <td>shampoo</td>
      <td>37.189,-121.705</td>
      <td>soap</td>
      <td>body wash</td>
      <td>CA</td>
      <td>95103</td>
    </tr>
    <tr>
      <th>106</th>
      <td>70.07</td>
      <td>clothing</td>
      <td>Dallas</td>
      <td>100152</td>
      <td>17-Apr-14</td>
      <td>belt</td>
      <td>32.745,-96.46</td>
      <td>pants</td>
      <td>jeans</td>
      <td>TX</td>
      <td>75126</td>
    </tr>
    <tr>
      <th>107</th>
      <td>53.92</td>
      <td>appliances</td>
      <td>New York City</td>
      <td>100181</td>
      <td>18-Apr-14</td>
      <td>peanut butter</td>
      <td>40.699,-74.041</td>
      <td>toaster</td>
      <td>butter</td>
      <td>NY</td>
      <td>10004</td>
    </tr>
    <tr>
      <th>108</th>
      <td>99.06</td>
      <td>outdoor</td>
      <td>Philadelphia</td>
      <td>100173</td>
      <td>19-Apr-14</td>
      <td>gloves</td>
      <td>39.953,-75.166</td>
      <td>snow shovel</td>
      <td>sand</td>
      <td>PA</td>
      <td>19102</td>
    </tr>
  </tbody>
</table>
</div>



Now we can see that we've cleaned these dates to the correct format.

There's dates in other formats as well.

In these files, more data can be made consistent but here only shown as examples.
# 2 - Missing Values
In this second step I'll show you how to detect and clean missing values in the <code>purchase</code> column.

You will see: comment of action, python code and results.


```python
import pandas as pd

df = pd.read_json("customer_data.json", convert_dates = False)
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>amount</th>
      <th>category</th>
      <th>city</th>
      <th>customer_id</th>
      <th>date</th>
      <th>frequently_bought_together</th>
      <th>lat_lon</th>
      <th>purchase</th>
      <th>related_items</th>
      <th>state</th>
      <th>zip_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>24.64</td>
      <td>household</td>
      <td>Chicago</td>
      <td>100191</td>
      <td>1-Jan-14</td>
      <td>towels</td>
      <td>41.86,-87.619</td>
      <td>soap</td>
      <td>towels</td>
      <td>IL</td>
      <td>60605</td>
    </tr>
    <tr>
      <th>1</th>
      <td>35</td>
      <td>clothing</td>
      <td>Dallas</td>
      <td>100199</td>
      <td>2-Jan-14</td>
      <td>sandals</td>
      <td>32.924,-96.547</td>
      <td>shorts</td>
      <td>belts</td>
      <td>TX</td>
      <td>75089</td>
    </tr>
    <tr>
      <th>2</th>
      <td>89.72</td>
      <td>outdoor</td>
      <td>Philadelphia</td>
      <td>100170</td>
      <td>3-Jan-14</td>
      <td>lawn bags</td>
      <td>40.002,-75.118</td>
      <td>lawn_mower</td>
      <td>shovels</td>
      <td>PA</td>
      <td>19019</td>
    </tr>
    <tr>
      <th>3</th>
      <td>51.32</td>
      <td>electronics</td>
      <td>Chicago</td>
      <td>100124</td>
      <td>4-Jan-14</td>
      <td>headphones</td>
      <td>41.88,-87.63</td>
      <td>laptop</td>
      <td>headphones</td>
      <td>IL</td>
      <td>60603</td>
    </tr>
    <tr>
      <th>4</th>
      <td>81.75</td>
      <td>outdoor</td>
      <td>Philadelphia</td>
      <td>100173</td>
      <td>5-Jan-14</td>
      <td>sponge</td>
      <td>39.953,-75.166</td>
      <td>car wash</td>
      <td>sponge</td>
      <td>PA</td>
      <td>19102</td>
    </tr>
  </tbody>
</table>
</div>



Taking a look at unique values, and missing values.

The <code>.isna()</code> method will only find standard missing value types, so we'll need to use the <code>.unique()</code> method for identifying non-standard missing values.


```python
print(df["purchase"].unique())
print(sum(df["purchase"].isna()))
```

    ['soap' 'shorts' 'lawn_mower' 'laptop' 'car wash' 'lawn mower' 'grill'
     'household cleaner' 'slow cooker' 'camera' 'snow shovel' 'shoes'
     'blender' 'shirts' 'toaster' 'detergent' 'tv' 'paper products' 'tools'
     'pants' 'audio' 'microwave' 'food processor' 'jackets' 'cell phone'
     'flower pot' None '?' '__' 'na' '--' 'cell' 'cell_phone' 'lawnmower'
     '1111']
    36
    

Lets change the standard missing values to a new category called <code>unavailable</code>.

We can double check that it worked by summing for missing values using the <code>.isna()</code> method after we've changed the missing values using the <code>.fillna()</code> method. If it worked, the sum should be 0.

We can also take a look at the unique values again to see if this new <code>unavailable</code> shows up.


```python
# changing standard missing values to "unavailable"
df["purchase"].fillna("unavailable", inplace=True)

# double checking that it worked by summing for missing values, and looking at unique categories
print(sum(df["purchase"].isna()))
print(df["purchase"].unique())
```

    0
    ['soap' 'shorts' 'lawn_mower' 'laptop' 'car wash' 'lawn mower' 'grill'
     'household cleaner' 'slow cooker' 'camera' 'snow shovel' 'shoes'
     'blender' 'shirts' 'toaster' 'detergent' 'tv' 'paper products' 'tools'
     'pants' 'audio' 'microwave' 'food processor' 'jackets' 'cell phone'
     'flower pot' 'unavailable' '?' '__' 'na' '--' 'cell' 'cell_phone'
     'lawnmower' '1111']
    

We can see several non-standard missing value types.

Lets identify those by using a list of <code>missing_values</code> which contains the following <code>["?", "__", "na", "--"]</code>.

We'll replace them by looping through the <code>purchase</code> column, and replacing the non-standard missing values using the <code>.loc()</code> method.


```python
# list of non-standard missing values
missing_values = ["?", "__", "na", "--"]

# replacing the missing values with the new category, "unavailable"
cnt = 0
for i in df["purchase"]:
    if i in missing_values:
        df.loc[cnt, "purchase"] = "unavailable"
    cnt+=1

print(df["purchase"].unique())
```

    ['soap' 'shorts' 'lawn_mower' 'laptop' 'car wash' 'lawn mower' 'grill'
     'household cleaner' 'slow cooker' 'camera' 'snow shovel' 'shoes'
     'blender' 'shirts' 'toaster' 'detergent' 'tv' 'paper products' 'tools'
     'pants' 'audio' 'microwave' 'food processor' 'jackets' 'cell phone'
     'flower pot' 'unavailable' 'cell' 'cell_phone' 'lawnmower' '1111']
    

We could also convert missing values when we read in the data.

The <code>.read_json()</code> method does not have the <code>na_values</code> parameter like <code>.read_csv()</code> does. 

We'll need to read in the <code>json</code> file, convert it to a <code>csv</code> file, and then read it back in using <code>.read_csv()</code>.


```python
# reading in the json file
df = pd.read_json("customer_data.json", convert_dates = False)

# writing the json file to a csv file
df.to_csv("customer_data2.csv")

# reading the csv file back in, replacing missing values
df2 = pd.read_csv("customer_data2.csv", na_values=missing_values)

print(df2["purchase"].unique())
```

    ['soap' 'shorts' 'lawn_mower' 'laptop' 'car wash' 'lawn mower' 'grill'
     'household cleaner' 'slow cooker' 'camera' 'snow shovel' 'shoes'
     'blender' 'shirts' 'toaster' 'detergent' 'tv' 'paper products' 'tools'
     'pants' 'audio' 'microwave' 'food processor' 'jackets' 'cell phone'
     'flower pot' nan 'cell' 'cell_phone' 'lawnmower' '1111']
    

The non-standard missing values have all been changed to missing values.

Lets finish up by replacing the missing values with the new category, <code>unavailable</code>.


```python
# changing missing values to "unavailable"
df2["purchase"].fillna("unavailable", inplace=True)

# double checking that it worked by summing for missing values, and looking at unique categories
print(sum(df2["purchase"].isna()))
print(df2["purchase"].unique())
```

    0
    ['soap' 'shorts' 'lawn_mower' 'laptop' 'car wash' 'lawn mower' 'grill'
     'household cleaner' 'slow cooker' 'camera' 'snow shovel' 'shoes'
     'blender' 'shirts' 'toaster' 'detergent' 'tv' 'paper products' 'tools'
     'pants' 'audio' 'microwave' 'food processor' 'jackets' 'cell phone'
     'flower pot' 'unavailable' 'cell' 'cell_phone' 'lawnmower' '1111']
    
# 3 - Consistent Strings
In this third step I'll show you how to fix inconsistent strings in the <code>category</code> column.

You can use: comment of action, python coding and results.


```python
import pandas as pd 

df = pd.read_json("customer_data.json", convert_dates=False)
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>amount</th>
      <th>category</th>
      <th>city</th>
      <th>customer_id</th>
      <th>date</th>
      <th>frequently_bought_together</th>
      <th>lat_lon</th>
      <th>purchase</th>
      <th>related_items</th>
      <th>state</th>
      <th>zip_code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>24.64</td>
      <td>household</td>
      <td>Chicago</td>
      <td>100191</td>
      <td>1-Jan-14</td>
      <td>towels</td>
      <td>41.86,-87.619</td>
      <td>soap</td>
      <td>towels</td>
      <td>IL</td>
      <td>60605</td>
    </tr>
    <tr>
      <th>1</th>
      <td>35</td>
      <td>clothing</td>
      <td>Dallas</td>
      <td>100199</td>
      <td>2-Jan-14</td>
      <td>sandals</td>
      <td>32.924,-96.547</td>
      <td>shorts</td>
      <td>belts</td>
      <td>TX</td>
      <td>75089</td>
    </tr>
    <tr>
      <th>2</th>
      <td>89.72</td>
      <td>outdoor</td>
      <td>Philadelphia</td>
      <td>100170</td>
      <td>3-Jan-14</td>
      <td>lawn bags</td>
      <td>40.002,-75.118</td>
      <td>lawn_mower</td>
      <td>shovels</td>
      <td>PA</td>
      <td>19019</td>
    </tr>
    <tr>
      <th>3</th>
      <td>51.32</td>
      <td>electronics</td>
      <td>Chicago</td>
      <td>100124</td>
      <td>4-Jan-14</td>
      <td>headphones</td>
      <td>41.88,-87.63</td>
      <td>laptop</td>
      <td>headphones</td>
      <td>IL</td>
      <td>60603</td>
    </tr>
    <tr>
      <th>4</th>
      <td>81.75</td>
      <td>outdoor</td>
      <td>Philadelphia</td>
      <td>100173</td>
      <td>5-Jan-14</td>
      <td>sponge</td>
      <td>39.953,-75.166</td>
      <td>car wash</td>
      <td>sponge</td>
      <td>PA</td>
      <td>19102</td>
    </tr>
  </tbody>
</table>
</div>



Lets take a quick look at the data using the <code>.unique()</code> method.


```python
print(df["category"].unique())
```

    ['household' 'clothing' 'outdoor' 'electronics' 'appliances' 'house'
     'elect^ronics' '^electro$nics' 'outdo&or' 'household_' '?out$door' 'elec'
     'app' 'house_hold' '%appliances' '\\appliances' 'electronic']
    

Not all of the strings have consistent formats.

The <code>household</code> category shows up with the following inconsistent formats <code>["household_", "house", "house_hold"]</code>.


```python
inconsistent_format = ["household_", "house", "house_hold"]

cnt = 0

for row in df["category"]:
    if row in inconsistent_format:
        df.loc[cnt, "category"] = "household"
    cnt+=1
    
print(df["category"].unique())
```

    ['household' 'clothing' 'outdoor' 'electronics' 'appliances'
     'elect^ronics' '^electro$nics' 'outdo&or' '?out$door' 'elec' 'app'
     '%appliances' '\\appliances' 'electronic']
    

We now see that we have one consistent format for <code>household</code>.

Use this same process to clean the other inconsistent strings.
