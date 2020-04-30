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
