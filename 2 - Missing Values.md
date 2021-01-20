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
    
