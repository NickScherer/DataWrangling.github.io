# 6 - Pivot Table
In this sixth step I'll show you how to reshape your data using a pivot table.

This will provide a nice condensed version. 

We'll reshape the data so that we can see how much each customer spent in each category.


```python
import pandas as pd 
import numpy as np

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



Taking a quick look using the <code>.head()</code> function, we can see all of the columns, and the first few rows of the data.

For this example, let's just use the first 50 rows of the data. 


```python
df_subset = df[0:50]
df_subset
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
    <tr>
      <th>5</th>
      <td>29.16</td>
      <td>outdoor</td>
      <td>San Diego</td>
      <td>100116</td>
      <td>6-Jan-14</td>
      <td>fertilizer</td>
      <td>33.143,-117.03</td>
      <td>lawn mower</td>
      <td>rakes</td>
      <td>CA</td>
      <td>92027</td>
    </tr>
    <tr>
      <th>6</th>
      <td>50.71</td>
      <td>outdoor</td>
      <td>Dallas</td>
      <td>100105</td>
      <td>7-Jan-14</td>
      <td>bbq sauce</td>
      <td>32.745,-96.46</td>
      <td>grill</td>
      <td>grill cleaner</td>
      <td>TX</td>
      <td>75126</td>
    </tr>
    <tr>
      <th>7</th>
      <td>35.03</td>
      <td>household</td>
      <td>San Antonio</td>
      <td>100148</td>
      <td>8-Jan-14</td>
      <td>spray bottles</td>
      <td>29.502,-98.306</td>
      <td>household cleaner</td>
      <td>spray bottles</td>
      <td>TX</td>
      <td>78109</td>
    </tr>
    <tr>
      <th>8</th>
      <td>30.55</td>
      <td>appliances</td>
      <td>Philadelphia</td>
      <td>100118</td>
      <td>9-Jan-14</td>
      <td>pot holders</td>
      <td>39.953,-75.166</td>
      <td>slow cooker</td>
      <td>tupperware</td>
      <td>PA</td>
      <td>19102</td>
    </tr>
    <tr>
      <th>9</th>
      <td>92.01</td>
      <td>electronics</td>
      <td>Dallas</td>
      <td>100106</td>
      <td>10-Jan-14</td>
      <td>camera lens</td>
      <td>32.917,-96.973</td>
      <td>camera</td>
      <td>lens cleaner</td>
      <td>TX</td>
      <td>75126</td>
    </tr>
    <tr>
      <th>10</th>
      <td>31.79</td>
      <td>outdoor</td>
      <td>New York City</td>
      <td>100109</td>
      <td>11-Jan-14</td>
      <td>gloves</td>
      <td>40.699,-74.041</td>
      <td>snow shovel</td>
      <td>boots</td>
      <td>NY</td>
      <td>10004</td>
    </tr>
    <tr>
      <th>11</th>
      <td>96.87</td>
      <td>clothing</td>
      <td>Chicago</td>
      <td>100153</td>
      <td>12-Jan-14</td>
      <td>dress shoes</td>
      <td>41.86,-87.619</td>
      <td>shoes</td>
      <td>dress shoes</td>
      <td>IL</td>
      <td>60605</td>
    </tr>
    <tr>
      <th>12</th>
      <td>41.91</td>
      <td>outdoor</td>
      <td>San Diego</td>
      <td>100116</td>
      <td>13-Jan-14</td>
      <td>bbq sauce</td>
      <td>33.143,-117.03</td>
      <td>grill</td>
      <td>propane tank</td>
      <td>CA</td>
      <td>92027</td>
    </tr>
    <tr>
      <th>13</th>
      <td>61.99</td>
      <td>appliances</td>
      <td>San Antonio</td>
      <td>100151</td>
      <td>14-Jan-14</td>
      <td>fruit</td>
      <td>29.363,-98.49</td>
      <td>blender</td>
      <td>pitcher</td>
      <td>TX</td>
      <td>78214</td>
    </tr>
    <tr>
      <th>14</th>
      <td>36.11</td>
      <td>clothing</td>
      <td>Chicago</td>
      <td>100191</td>
      <td>15-Jan-14</td>
      <td>t shirt</td>
      <td>41.86,-87.619</td>
      <td>shirts</td>
      <td>t-shirt</td>
      <td>IL</td>
      <td>60605</td>
    </tr>
    <tr>
      <th>15</th>
      <td>75</td>
      <td>appliances</td>
      <td>San Antonio</td>
      <td>100185</td>
      <td>16-Jan-14</td>
      <td>bagels</td>
      <td>29.363,-98.49</td>
      <td>toaster</td>
      <td>cream cheese</td>
      <td>TX</td>
      <td>78214</td>
    </tr>
    <tr>
      <th>16</th>
      <td>87.08</td>
      <td>electronics</td>
      <td>Chicago</td>
      <td>100153</td>
      <td>17-Jan-14</td>
      <td>headphones</td>
      <td>41.86,-87.619</td>
      <td>laptop</td>
      <td>charger</td>
      <td>IL</td>
      <td>60605</td>
    </tr>
    <tr>
      <th>17</th>
      <td>41.34</td>
      <td>household</td>
      <td>San Antonio</td>
      <td>100151</td>
      <td>18-Jan-14</td>
      <td>fabric softener</td>
      <td>29.363,-98.49</td>
      <td>detergent</td>
      <td>fabric softener</td>
      <td>TX</td>
      <td>78214</td>
    </tr>
    <tr>
      <th>18</th>
      <td>27.37</td>
      <td>clothing</td>
      <td>New York City</td>
      <td>100196</td>
      <td>19-Jan-14</td>
      <td>shoe laces</td>
      <td>40.699,-74.041</td>
      <td>shoes</td>
      <td>dress shoes</td>
      <td>NY</td>
      <td>10004</td>
    </tr>
    <tr>
      <th>19</th>
      <td>38.61</td>
      <td>electronics</td>
      <td>Chicago</td>
      <td>100124</td>
      <td>20-Jan-14</td>
      <td>surround sound</td>
      <td>41.88,-87.63</td>
      <td>tv</td>
      <td>surround sound</td>
      <td>IL</td>
      <td>60603</td>
    </tr>
    <tr>
      <th>20</th>
      <td>53.8</td>
      <td>household</td>
      <td>New York City</td>
      <td>100188</td>
      <td>21-Jan-14</td>
      <td>paper towels</td>
      <td>40.717,-73.987</td>
      <td>paper products</td>
      <td>toilet paper</td>
      <td>NY</td>
      <td>10002</td>
    </tr>
    <tr>
      <th>21</th>
      <td>85</td>
      <td>appliances</td>
      <td>San Jose</td>
      <td>100192</td>
      <td>22-Jan-14</td>
      <td>butter</td>
      <td>37.536,-122.034</td>
      <td>toaster</td>
      <td>bread</td>
      <td>CA</td>
      <td>94560</td>
    </tr>
    <tr>
      <th>22</th>
      <td>85.92</td>
      <td>house</td>
      <td>SD</td>
      <td>100140</td>
      <td>23-Jan-14</td>
      <td>batteries</td>
      <td>32.839,-117.262</td>
      <td>tools</td>
      <td>screws</td>
      <td>CA</td>
      <td>92037</td>
    </tr>
    <tr>
      <th>23</th>
      <td>91.98</td>
      <td>clothing</td>
      <td>San Jose</td>
      <td>100159</td>
      <td>24-Jan-14</td>
      <td>sneakers</td>
      <td>37.189,-121.705</td>
      <td>shoes</td>
      <td>dress shoes</td>
      <td>CA</td>
      <td>95115</td>
    </tr>
    <tr>
      <th>24</th>
      <td>64.86</td>
      <td>appliances</td>
      <td>San Antonio</td>
      <td>100182</td>
      <td>25-Jan-14</td>
      <td>cookbook</td>
      <td>29.852,-98.729</td>
      <td>slow cooker</td>
      <td>tongs</td>
      <td>TX</td>
      <td>78006</td>
    </tr>
    <tr>
      <th>25</th>
      <td>86.05</td>
      <td>outdoor</td>
      <td>Hou</td>
      <td>100158</td>
      <td>26-Jan-14</td>
      <td>rakes</td>
      <td>29.718,-95.428</td>
      <td>lawn mower</td>
      <td>gardening gloves</td>
      <td>TX</td>
      <td>77005</td>
    </tr>
    <tr>
      <th>26</th>
      <td>78.81</td>
      <td>clothing</td>
      <td>San Antonio</td>
      <td>100185</td>
      <td>27-Jan-14</td>
      <td>wallet</td>
      <td>29.363,-98.49</td>
      <td>pants</td>
      <td>wallet</td>
      <td>TX</td>
      <td>78214</td>
    </tr>
    <tr>
      <th>27</th>
      <td>78.61</td>
      <td>electronics</td>
      <td>Houston</td>
      <td>100103</td>
      <td>28-Jan-14</td>
      <td>headphones</td>
      <td>29.72,-95.279</td>
      <td>audio</td>
      <td>headphones</td>
      <td>TX</td>
      <td>77012</td>
    </tr>
    <tr>
      <th>28</th>
      <td>36.21</td>
      <td>clothing</td>
      <td>Philadelphia</td>
      <td>100150</td>
      <td>29-Jan-14</td>
      <td>sunglasses</td>
      <td>40.002,-75.118</td>
      <td>shorts</td>
      <td>t-shirts</td>
      <td>PA</td>
      <td>19019</td>
    </tr>
    <tr>
      <th>29</th>
      <td>66.56</td>
      <td>clothing</td>
      <td>Phoenix</td>
      <td>100183</td>
      <td>30-Jan-14</td>
      <td>collared shirt</td>
      <td>33.451,-112.071</td>
      <td>shirts</td>
      <td>shortsleeve</td>
      <td>AZ</td>
      <td>85004</td>
    </tr>
    <tr>
      <th>30</th>
      <td>77.28</td>
      <td>outdoor</td>
      <td>Phoenix</td>
      <td>100111</td>
      <td>31-Jan-14</td>
      <td>gloves</td>
      <td>33.512,-112.142</td>
      <td>snow shovel</td>
      <td>mittens</td>
      <td>AZ</td>
      <td>85019</td>
    </tr>
    <tr>
      <th>31</th>
      <td>89.36</td>
      <td>electronics</td>
      <td>San Jose</td>
      <td>100160</td>
      <td>1-Feb-14</td>
      <td>surround sound</td>
      <td>37.536,-122.034</td>
      <td>tv</td>
      <td>speakers</td>
      <td>CA</td>
      <td>94560</td>
    </tr>
    <tr>
      <th>32</th>
      <td>23.69</td>
      <td>clothing</td>
      <td>Los Angeles</td>
      <td>100133</td>
      <td>2-Feb-14</td>
      <td>dress shirt</td>
      <td>34.066,-118.309</td>
      <td>shirts</td>
      <td>collared shirt</td>
      <td>CA</td>
      <td>90020</td>
    </tr>
    <tr>
      <th>33</th>
      <td>85.69</td>
      <td>outdoor</td>
      <td>Houston</td>
      <td>100158</td>
      <td>3-Feb-14</td>
      <td>sand</td>
      <td>29.718,-95.428</td>
      <td>snow shovel</td>
      <td>mittens</td>
      <td>TX</td>
      <td>77005</td>
    </tr>
    <tr>
      <th>34</th>
      <td>97.59</td>
      <td>appliances</td>
      <td>San Jose</td>
      <td>100193</td>
      <td>4-Feb-14</td>
      <td>egg cooker</td>
      <td>37.189,-121.705</td>
      <td>microwave</td>
      <td>popcorn</td>
      <td>CA</td>
      <td>95115</td>
    </tr>
    <tr>
      <th>35</th>
      <td>32.89</td>
      <td>appliances</td>
      <td>New York City</td>
      <td>100167</td>
      <td>5-Feb-14</td>
      <td>vegetable peeler</td>
      <td>40.699,-74.041</td>
      <td>food processor</td>
      <td>vegetable peeler</td>
      <td>NY</td>
      <td>10004</td>
    </tr>
    <tr>
      <th>36</th>
      <td>70.66</td>
      <td>house</td>
      <td>Houston</td>
      <td>100102</td>
      <td>6-Feb-14</td>
      <td>loofah</td>
      <td>29.793,-95.367</td>
      <td>soap</td>
      <td>shampoo</td>
      <td>TX</td>
      <td>77009</td>
    </tr>
    <tr>
      <th>37</th>
      <td>76.69</td>
      <td>house</td>
      <td>New York City</td>
      <td>100167</td>
      <td>7-Feb-14</td>
      <td>loofah</td>
      <td>40.699,-74.041</td>
      <td>soap</td>
      <td>body wash</td>
      <td>NY</td>
      <td>10004</td>
    </tr>
    <tr>
      <th>38</th>
      <td>54.64</td>
      <td>electronics</td>
      <td>San Antonio</td>
      <td>100185</td>
      <td>8-Feb-14</td>
      <td>camera case</td>
      <td>29.363,-98.49</td>
      <td>camera</td>
      <td>editing software</td>
      <td>TX</td>
      <td>78214</td>
    </tr>
    <tr>
      <th>39</th>
      <td>85.23</td>
      <td>appliances</td>
      <td>San Diego</td>
      <td>100140</td>
      <td>9-Feb-14</td>
      <td>vegetables</td>
      <td>32.839,-117.262</td>
      <td>food processor</td>
      <td>vegetable peeler</td>
      <td>CA</td>
      <td>92037</td>
    </tr>
    <tr>
      <th>40</th>
      <td>70.18</td>
      <td>appliances</td>
      <td>San Jose</td>
      <td>100162</td>
      <td>10-Feb-14</td>
      <td>tupperware</td>
      <td>37.536,-122.034</td>
      <td>food processor</td>
      <td>vegetables</td>
      <td>CA</td>
      <td>94560</td>
    </tr>
    <tr>
      <th>41</th>
      <td>34.57</td>
      <td>appliances</td>
      <td>Los Angeles</td>
      <td>100123</td>
      <td>11-Feb-14</td>
      <td>serving spoon</td>
      <td>34.066,-118.309</td>
      <td>slow cooker</td>
      <td>cookbook</td>
      <td>CA</td>
      <td>90020</td>
    </tr>
    <tr>
      <th>42</th>
      <td>63.54</td>
      <td>appliances</td>
      <td>Houston</td>
      <td>100186</td>
      <td>12-Feb-14</td>
      <td>tupperware</td>
      <td>29.793,-95.367</td>
      <td>slow cooker</td>
      <td>tongs</td>
      <td>TX</td>
      <td>77009</td>
    </tr>
    <tr>
      <th>43</th>
      <td>76.43</td>
      <td>clothing</td>
      <td>San Antonio</td>
      <td>100198</td>
      <td>13-Feb-14</td>
      <td>wallet</td>
      <td>29.438,-98.462</td>
      <td>pants</td>
      <td>khakis</td>
      <td>TX</td>
      <td>78206</td>
    </tr>
    <tr>
      <th>44</th>
      <td>95.85</td>
      <td>outdoor</td>
      <td>New York City</td>
      <td>100188</td>
      <td>14-Feb-14</td>
      <td>sand</td>
      <td>40.717,-73.987</td>
      <td>snow shovel</td>
      <td>mittens</td>
      <td>NY</td>
      <td>10002</td>
    </tr>
    <tr>
      <th>45</th>
      <td>79.43</td>
      <td>clothing</td>
      <td>Chicago</td>
      <td>100136</td>
      <td>15-Feb-14</td>
      <td>wallet</td>
      <td>41.883,-87.629</td>
      <td>pants</td>
      <td>khakis</td>
      <td>IL</td>
      <td>60602</td>
    </tr>
    <tr>
      <th>46</th>
      <td>76.08</td>
      <td>clothing</td>
      <td>San Jose</td>
      <td>100162</td>
      <td>16-Feb-14</td>
      <td>dress shirt</td>
      <td>37.536,-122.034</td>
      <td>shirts</td>
      <td>t-shirt</td>
      <td>CA</td>
      <td>94560</td>
    </tr>
    <tr>
      <th>47</th>
      <td>57.33</td>
      <td>clothing</td>
      <td>Chicago</td>
      <td>100191</td>
      <td>17-Feb-14</td>
      <td>button down shirt</td>
      <td>41.86,-87.619</td>
      <td>shirts</td>
      <td>shortsleeve</td>
      <td>IL</td>
      <td>60605</td>
    </tr>
    <tr>
      <th>48</th>
      <td>86.29</td>
      <td>clothing</td>
      <td>Dallas</td>
      <td>100120</td>
      <td>18-Feb-14</td>
      <td>winter gloves</td>
      <td>32.961,-96.838</td>
      <td>jackets</td>
      <td>scarfs</td>
      <td>TX</td>
      <td>75001</td>
    </tr>
    <tr>
      <th>49</th>
      <td>91.87</td>
      <td>electronics</td>
      <td>Dallas</td>
      <td>100106</td>
      <td>19-Feb-14</td>
      <td>cell phone case</td>
      <td>32.917,-96.973</td>
      <td>cell phone</td>
      <td>screen cleaner</td>
      <td>TX</td>
      <td>75063</td>
    </tr>
  </tbody>
</table>
</div>



Let's take a look at the types for each column using the <code>.dtypes</code> method.


```python
df_subset.dtypes
```




    amount                        object
    category                      object
    city                          object
    customer_id                    int64
    date                          object
    frequently_bought_together    object
    lat_lon                       object
    purchase                      object
    related_items                 object
    state                         object
    zip_code                       int64
    dtype: object



The amount column should be a numeric type, but Pandas thinks it's an <code>object</code>. Let's go ahead and change that column to a numeric <code>float</code> type using the <code>.astype()</code> method.


```python
df_subset["amount"] = df_subset["amount"].astype(float)
df_subset.dtypes
```

    C:\Users\NickScherer\Anaconda3\lib\site-packages\ipykernel_launcher.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      """Entry point for launching an IPython kernel.
    




    amount                        float64
    category                       object
    city                           object
    customer_id                     int64
    date                           object
    frequently_bought_together     object
    lat_lon                        object
    purchase                       object
    related_items                  object
    state                          object
    zip_code                        int64
    dtype: object



Now we can see that the <code>amount</code> column is a numeric <code>float</code> type. 

We don't need all of the columns, just the <code>customer_id</code>, <code>category</code>, and <code>amount</code> columns.

Here's what that smaller dataframe would look like.


```python
df_subset[["customer_id", "category", "amount"]]
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
      <th>customer_id</th>
      <th>category</th>
      <th>amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>100191</td>
      <td>household</td>
      <td>24.64</td>
    </tr>
    <tr>
      <th>1</th>
      <td>100199</td>
      <td>clothing</td>
      <td>35.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>100170</td>
      <td>outdoor</td>
      <td>89.72</td>
    </tr>
    <tr>
      <th>3</th>
      <td>100124</td>
      <td>electronics</td>
      <td>51.32</td>
    </tr>
    <tr>
      <th>4</th>
      <td>100173</td>
      <td>outdoor</td>
      <td>81.75</td>
    </tr>
    <tr>
      <th>5</th>
      <td>100116</td>
      <td>outdoor</td>
      <td>29.16</td>
    </tr>
    <tr>
      <th>6</th>
      <td>100105</td>
      <td>outdoor</td>
      <td>50.71</td>
    </tr>
    <tr>
      <th>7</th>
      <td>100148</td>
      <td>household</td>
      <td>35.03</td>
    </tr>
    <tr>
      <th>8</th>
      <td>100118</td>
      <td>appliances</td>
      <td>30.55</td>
    </tr>
    <tr>
      <th>9</th>
      <td>100106</td>
      <td>electronics</td>
      <td>92.01</td>
    </tr>
    <tr>
      <th>10</th>
      <td>100109</td>
      <td>outdoor</td>
      <td>31.79</td>
    </tr>
    <tr>
      <th>11</th>
      <td>100153</td>
      <td>clothing</td>
      <td>96.87</td>
    </tr>
    <tr>
      <th>12</th>
      <td>100116</td>
      <td>outdoor</td>
      <td>41.91</td>
    </tr>
    <tr>
      <th>13</th>
      <td>100151</td>
      <td>appliances</td>
      <td>61.99</td>
    </tr>
    <tr>
      <th>14</th>
      <td>100191</td>
      <td>clothing</td>
      <td>36.11</td>
    </tr>
    <tr>
      <th>15</th>
      <td>100185</td>
      <td>appliances</td>
      <td>75.00</td>
    </tr>
    <tr>
      <th>16</th>
      <td>100153</td>
      <td>electronics</td>
      <td>87.08</td>
    </tr>
    <tr>
      <th>17</th>
      <td>100151</td>
      <td>household</td>
      <td>41.34</td>
    </tr>
    <tr>
      <th>18</th>
      <td>100196</td>
      <td>clothing</td>
      <td>27.37</td>
    </tr>
    <tr>
      <th>19</th>
      <td>100124</td>
      <td>electronics</td>
      <td>38.61</td>
    </tr>
    <tr>
      <th>20</th>
      <td>100188</td>
      <td>household</td>
      <td>53.80</td>
    </tr>
    <tr>
      <th>21</th>
      <td>100192</td>
      <td>appliances</td>
      <td>85.00</td>
    </tr>
    <tr>
      <th>22</th>
      <td>100140</td>
      <td>house</td>
      <td>85.92</td>
    </tr>
    <tr>
      <th>23</th>
      <td>100159</td>
      <td>clothing</td>
      <td>91.98</td>
    </tr>
    <tr>
      <th>24</th>
      <td>100182</td>
      <td>appliances</td>
      <td>64.86</td>
    </tr>
  </tbody>
</table>
</div>



Let's finish up by creating our <code>pivot_table</code>.

We'll set the index to <code>customer_id</code>, the columns to <code>category</code>, and the values to <code>amount</code>. This will reshape the data so that we can see how much each customer spent in each category. Let's create this using a new dataframe called <code>df_pivot</code>.

The final important point before we reshape the data is the <code>aggfunc</code> parameter. Since customers probably spent multiple purchase in the same categories, we'll want to collect all of the purchase. We'll do that using Numpy's <code>sum</code> method. I've shorted the Numpy library name to <code>np</code>, so that's why I've set the <code>aggfunc</code> to <code>np.sum</code>.


```python
# pivot table; aggregation function "sum"

df_pivot = df_subset.pivot_table(index="customer_id", columns="category", values="amount", aggfunc=np.sum)
print(df_pivot)
```

    category     appliances  clothing  electronics  house  household  outdoor
    customer_id                                                              
    100102              NaN       NaN          NaN  70.66        NaN      NaN
    100103              NaN       NaN        78.61    NaN        NaN      NaN
    100105              NaN       NaN          NaN    NaN        NaN    50.71
    100106              NaN       NaN       183.88    NaN        NaN      NaN
    100109              NaN       NaN          NaN    NaN        NaN    31.79
    100111              NaN       NaN          NaN    NaN        NaN    77.28
    100116              NaN       NaN          NaN    NaN        NaN    71.07
    100118            30.55       NaN          NaN    NaN        NaN      NaN
    100120              NaN     86.29          NaN    NaN        NaN      NaN
    100123            34.57       NaN          NaN    NaN        NaN      NaN
    100124              NaN       NaN        89.93    NaN        NaN      NaN
    100133              NaN     23.69          NaN    NaN        NaN      NaN
    100136              NaN     79.43          NaN    NaN        NaN      NaN
    100140            85.23       NaN          NaN  85.92        NaN      NaN
    100148              NaN       NaN          NaN    NaN      35.03      NaN
    100150              NaN     36.21          NaN    NaN        NaN      NaN
    100151            61.99       NaN          NaN    NaN      41.34      NaN
    100153              NaN     96.87        87.08    NaN        NaN      NaN
    100158              NaN       NaN          NaN    NaN        NaN   171.74
    100159              NaN     91.98          NaN    NaN        NaN      NaN
    100160              NaN       NaN        89.36    NaN        NaN      NaN
    100162            70.18     76.08          NaN    NaN        NaN      NaN
    100167            32.89       NaN          NaN  76.69        NaN      NaN
    100170              NaN       NaN          NaN    NaN        NaN    89.72
    100173              NaN       NaN          NaN    NaN        NaN    81.75
    100182            64.86       NaN          NaN    NaN        NaN      NaN
    100183              NaN     66.56          NaN    NaN        NaN      NaN
    100185            75.00     78.81        54.64    NaN        NaN      NaN
    100186            63.54       NaN          NaN    NaN        NaN      NaN
    100188              NaN       NaN          NaN    NaN      53.80    95.85
    100191              NaN     93.44          NaN    NaN      24.64      NaN
    100192            85.00       NaN          NaN    NaN        NaN      NaN
    100193            97.59       NaN          NaN    NaN        NaN      NaN
    100196              NaN     27.37          NaN    NaN        NaN      NaN
    100198              NaN     76.43          NaN    NaN        NaN      NaN
    100199              NaN     35.00          NaN    NaN        NaN      NaN
    

Now we have a new dataframe showing how much each customer spent in each category. 

There's a lot of <code>NaN</code> values because a lot of customers didn't spend any money in certain categories.

You should also note that there's a <code>house</code> and <code>household</code> column. We need to clean the data so that we have consistent strings before we reshape it. Look back at <strong>Step 3 - Consistent Strings</strong> to help you with that.
