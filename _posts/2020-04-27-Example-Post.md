Data Wrangling with Python - Example Project
Introduction
The purpose of this project was to clean a messy dataset for a marketing department at an ecommerce company. The marketing company analyzes the data in detail to provide business decisions. My task was to clean the data for them so that they would have a reliable dataset to analyze. The final deliverable to the marketing group was a clean dataset in tabular format that they could easily work with.

I worked with various data formats, including JSON and XML. To perform the data cleaning tasks I utilized Python, along with useful data cleaning libraries such as Pandas. All of my work was neatly documented and organized using Jupyter Notebooks. You can find a link to the full data cleaning notebook here *[this is where you provide a link to your github page]*.

Data Overview
In this project I worked with a JSON dataset and an XML dataset. The JSON dataset contained customer information with various fields. These fields included the following:

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
The JSON dataset with the customer information is the messy dataset that needs to be cleaned.

An XML file with location data was provided by a different part of the data cleaning team. This file contains the following fields:

City
Zipcode
Latitude_Longitude
The other members of the data cleaning team have assured me that this dataset is accurate. They also said that the "city", "state", and "lat_lon" fields are accurate in the JSON file, but the "zip_code" field is not. The "lat_lon" data in the JSON file will be cross-referenced with the location data in the XML file to correct innacurate zipcode data.

Data Cleaning Plan
To clean the data, I used a three step data cleaning plan that consisted of the following:

Importing the data
Cleaning the data
Reshaping the data
To clean the data, I dealt with the following four aspects of data wrangling:

Missing Values
Correct Data Types
Consistent Data
Accurate Data


```python
def hello_world():
    print("hello world!")
    
print(hello_world())
```

    hello world!
    None
    


```python

```


```python

```


```python

```
,,,,