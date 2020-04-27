---
title: "Data Wrangling Project"
date: 2020-04-08
tags: [data wrangling, data science, messy data]
header:
  image: "/images/perceptron/percept.jpg"
excerpt: "Data Wrangling, Data Science, Messy Data"
mathjax: "true"
---

# H1 Heading
In this project i am going to be cleaning a messy dataset. Assume that you work on a data science team at an ecommerce company, which sells products ranging from technology, to home goods, to clothing.
Your company is very focused on user experience. Happy customers are much more likely to return to your website and purchase things.
## H2 Heading
It’s my job to clean the messy data set provided, and reshape it in to an easier to read format. This dataset would then be provided to the hypothetical analytics team. Obviously this is a made up scenario, so there’s not really an analytics team that is going to look at this data.
### H3 Heading
There’s no right answer to this project, so don’t worry about catching everything. I’ve provided numerous hints in the next modules to help you along with your cleaning tasks. Even if you don’t catch all the messy data, that’s okay! Be sure to tackle several different cleaning tasks, and then write your project up.

Here's a bulleted list:
* First Step
- Import the Data
The first step is to import the data. The first file is a JSON file containing the customer information.
This dataset contains the following columns:

customer_id
date
purchase
category
amount
related_items
frequently_bought_together
city
state
zip_code
lat_lon
The other file is an XML file. This file contains accurate location data. You’ll need this to check for accuracy in the zip_code column.

You can get a copy of this accurate location data here:

+ Second Step
- Clean the Data
After you’ve imported the data, you’ll need to clean the customer data.

Remember the following four cleaning tasks that we learned about:

Missing Values
Consistency
Correct Types
Accuracy
The only column that you will be able to check for accuracy is the zip_code column in the customer data set. All of the other columns are accurate. To check for accuracy, use the lat_lon column to cross reference the data in the location_data.xml file.

+ Third Step
- Reshape the Data
After you’ve cleaned the data, make sure to reshape it.

You'll need to use pivot_table to reshape the data using customer_id as the index, category for the columns, and amount for the values.

You’ll also need to change the aggfunc parameter to np.sum so that you sum the total for each category.

Here's a numbered list:
1. First
2. Second
3. Third

Python code block:
```python
    import numpy as np

    def test_function(x, y):
      z = np.sum(x,y)
      return z
```

R code block:
```r
library(tidyverse)
df <- read_csv("some_file.csv")
head(df)
```

Here's some inline code `x+y`.

Here's an image:
<img src="{{ site.url }}{{ site.baseurl }}/images/perceptron/linsep.jpg" alt="linearly separable data">

Here's another image using Kramdown:
![alt]({{ site.url }}{{ site.baseurl }}/images/perceptron/linsep.jpg)

Here's some math:

$$z=x+y$$

You can also put it inline $$z=x+y$$
