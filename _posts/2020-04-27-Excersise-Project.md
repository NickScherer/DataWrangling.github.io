# Data Wrangling with Python - Exercises Project

## Introduction

The purpose of this project was to clean a messy dataset for a marketing department at an ecommerce company. The marketing company analyzes the data in detail to provide business decisions. My task was to clean the data for them so that they would have a reliable dataset to analyze. The final deliverable to the marketing group was a clean dataset in tabular format that they could easily work with.

I worked with various data formats, including JSON and XML. To perform the data cleaning tasks I utilized Python, along with useful data cleaning libraries such as Pandas. All of my work was neatly documented and organized using Jupyter Notebooks. You can find a link to the full data cleaning notebook here *[this is where you provide a link to your github page]*.

## Data Overview

In this project I worked with a JSON dataset and an XML dataset. The JSON dataset contained customer information with various fields. These fields included the following:
- customer_id
- date
- purchase
- category
- amount
- related_items
- frequently_bought_together
- city
- state
- zip_code
- lat_lon

The JSON dataset with the customer information is the messy dataset that needs to be cleaned. 

An XML file with location data was provided by a different part of the data cleaning team. This file contains the following fields:
- City
- Zipcode
- Latitude_Longitude

The other members of the data cleaning team have assured me that this dataset is accurate. They also said that the "city", "state", and "lat_lon" fields are accurate in the JSON file, but the "zip_code" field is not. The "lat_lon" data in the JSON file will be cross-referenced with the location data in the XML file to correct innacurate zipcode data.


## Data Cleaning Plan
To clean the data, I used a three step data cleaning plan that consisted of the following:
1. Importing the data
2. Cleaning the data
3. Reshaping the data

To clean the data, I dealt with the following four aspects of data wrangling:
1. Missing Values
2. Correct Data Types
3. Consistent Data
4. Accurate Data

## Importing the Data

The first step was to import the data. The customer information data was in JSON format. I utilized the JSON library to take a look at the data.


```python
import json

with open("customer_data_example.json") as f_in:
    data = json.load(f_in)

print(json.dumps(data, indent=2))
```

    [
      {
        "customer_id": 100191,
        "date": "1-Jan-14",
        "purchase": "soap",
        "category": "household",
        "amount": "24.64",
        "related_items": "towels",
        "frequently_bought_together": "towels",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60605,
        "lat_lon": "41.86,-87.619"
      },
      {
        "customer_id": 100199,
        "date": "2-Jan-14",
        "purchase": "shorts",
        "category": "clothing",
        "amount": "35",
        "related_items": "belts",
        "frequently_bought_together": "sandals",
        "city": "Dallas",
        "state": "TX",
        "zip_code": 75089,
        "lat_lon": "32.924,-96.547"
      },
      {
        "customer_id": 100170,
        "date": "3-Jan-14",
        "purchase": "lawn_mower",
        "category": "outdoor",
        "amount": "89.72",
        "related_items": "shovels",
        "frequently_bought_together": "lawn bags",
        "city": "Philadelphia",
        "state": "PA",
        "zip_code": 19019,
        "lat_lon": "40.002,-75.118"
      },
      {
        "customer_id": 100124,
        "date": "4-Jan-14",
        "purchase": "laptop",
        "category": "electronics",
        "amount": "51.32",
        "related_items": "headphones",
        "frequently_bought_together": "headphones",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60603,
        "lat_lon": "41.88,-87.63"
      },
      {
        "customer_id": 100173,
        "date": "5-Jan-14",
        "purchase": "car wash",
        "category": "outdoor",
        "amount": "81.75",
        "related_items": "sponge",
        "frequently_bought_together": "sponge",
        "city": "Philadelphia",
        "state": "PA",
        "zip_code": 19102,
        "lat_lon": "39.953,-75.166"
      },
      {
        "customer_id": 100116,
        "date": "6-Jan-14",
        "purchase": "lawn mower",
        "category": "outdoor",
        "amount": "29.16",
        "related_items": "rakes",
        "frequently_bought_together": "fertilizer",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 92027,
        "lat_lon": "33.143,-117.03"
      },
      {
        "customer_id": 100105,
        "date": "7-Jan-14",
        "purchase": "grill",
        "category": "outdoor",
        "amount": "50.71",
        "related_items": "grill cleaner",
        "frequently_bought_together": "bbq sauce",
        "city": "Dallas",
        "state": "TX",
        "zip_code": 75126,
        "lat_lon": "32.745,-96.46"
      },
      {
        "customer_id": 100148,
        "date": "8-Jan-14",
        "purchase": "household cleaner",
        "category": "household",
        "amount": "35.03",
        "related_items": "spray bottles",
        "frequently_bought_together": "spray bottles",
        "city": "San Antonio",
        "state": "TX",
        "zip_code": 78109,
        "lat_lon": "29.502,-98.306"
      },
      {
        "customer_id": 100118,
        "date": "9-Jan-14",
        "purchase": "slow cooker",
        "category": "appliances",
        "amount": "30.55",
        "related_items": "tupperware",
        "frequently_bought_together": "pot holders",
        "city": "Philadelphia",
        "state": "PA",
        "zip_code": 19102,
        "lat_lon": "39.953,-75.166"
      },
      {
        "customer_id": 100106,
        "date": "10-Jan-14",
        "purchase": "camera",
        "category": "electronics",
        "amount": "92.01",
        "related_items": "lens cleaner",
        "frequently_bought_together": "camera lens",
        "city": "Dallas",
        "state": "TX",
        "zip_code": 75126,
        "lat_lon": "32.917,-96.973"
      },
      {
        "customer_id": 100109,
        "date": "11-Jan-14",
        "purchase": "snow shovel",
        "category": "outdoor",
        "amount": "31.79",
        "related_items": "boots",
        "frequently_bought_together": "gloves",
        "city": "New York City",
        "state": "NY",
        "zip_code": 10004,
        "lat_lon": "40.699,-74.041"
      },
      {
        "customer_id": 100153,
        "date": "12-Jan-14",
        "purchase": "shoes",
        "category": "clothing",
        "amount": "96.87",
        "related_items": "dress shoes",
        "frequently_bought_together": "dress shoes",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60605,
        "lat_lon": "41.86,-87.619"
      },
      {
        "customer_id": 100116,
        "date": "13-Jan-14",
        "purchase": "grill",
        "category": "outdoor",
        "amount": "41.91",
        "related_items": "propane tank",
        "frequently_bought_together": "bbq sauce",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 92027,
        "lat_lon": "33.143,-117.03"
      },
      {
        "customer_id": 100151,
        "date": "14-Jan-14",
        "purchase": "blender",
        "category": "appliances",
        "amount": "61.99",
        "related_items": "pitcher",
        "frequently_bought_together": "fruit",
        "city": "San Antonio",
        "state": "TX",
        "zip_code": 78214,
        "lat_lon": "29.363,-98.49"
      },
      {
        "customer_id": 100191,
        "date": "15-Jan-14",
        "purchase": "shirts",
        "category": "clothing",
        "amount": "36.11",
        "related_items": "t-shirt",
        "frequently_bought_together": "t shirt",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60605,
        "lat_lon": "41.86,-87.619"
      },
      {
        "customer_id": 100185,
        "date": "16-Jan-14",
        "purchase": "toaster",
        "category": "appliances",
        "amount": "75",
        "related_items": "cream cheese",
        "frequently_bought_together": "bagels",
        "city": "San Antonio",
        "state": "TX",
        "zip_code": 78214,
        "lat_lon": "29.363,-98.49"
      },
      {
        "customer_id": 100153,
        "date": "17-Jan-14",
        "purchase": "laptop",
        "category": "electronics",
        "amount": "87.08",
        "related_items": "charger",
        "frequently_bought_together": "headphones",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60605,
        "lat_lon": "41.86,-87.619"
      },
      {
        "customer_id": 100151,
        "date": "18-Jan-14",
        "purchase": "detergent",
        "category": "household",
        "amount": "41.34",
        "related_items": "fabric softener",
        "frequently_bought_together": "fabric softener",
        "city": "San Antonio",
        "state": "TX",
        "zip_code": 78214,
        "lat_lon": "29.363,-98.49"
      },
      {
        "customer_id": 100196,
        "date": "19-Jan-14",
        "purchase": "shoes",
        "category": "clothing",
        "amount": "27.37",
        "related_items": "dress shoes",
        "frequently_bought_together": "shoe laces",
        "city": "New York City",
        "state": "NY",
        "zip_code": 10004,
        "lat_lon": "40.699,-74.041"
      },
      {
        "customer_id": 100124,
        "date": "20-Jan-14",
        "purchase": "tv",
        "category": "electronics",
        "amount": "38.61",
        "related_items": "surround sound",
        "frequently_bought_together": "surround sound",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60603,
        "lat_lon": "41.88,-87.63"
      },
      {
        "customer_id": 100188,
        "date": "21-Jan-14",
        "purchase": "paper products",
        "category": "household",
        "amount": "53.8",
        "related_items": "toilet paper",
        "frequently_bought_together": "paper towels",
        "city": "New York City",
        "state": "NY",
        "zip_code": 10002,
        "lat_lon": "40.717,-73.987"
      },
      {
        "customer_id": 100192,
        "date": "22-Jan-14",
        "purchase": "toaster",
        "category": "appliances",
        "amount": "85",
        "related_items": "bread",
        "frequently_bought_together": "butter",
        "city": "San Jose",
        "state": "CA",
        "zip_code": 94560,
        "lat_lon": "37.536,-122.034"
      },
      {
        "customer_id": 100140,
        "date": "23-Jan-14",
        "purchase": "tools",
        "category": "house",
        "amount": "85.92",
        "related_items": "screws",
        "frequently_bought_together": "batteries",
        "city": "SD",
        "state": "CA",
        "zip_code": 92037,
        "lat_lon": "32.839,-117.262"
      },
      {
        "customer_id": 100159,
        "date": "24-Jan-14",
        "purchase": "shoes",
        "category": "clothing",
        "amount": "91.98",
        "related_items": "dress shoes",
        "frequently_bought_together": "sneakers",
        "city": "San Jose",
        "state": "CA",
        "zip_code": 95115,
        "lat_lon": "37.189,-121.705"
      },
      {
        "customer_id": 100182,
        "date": "25-Jan-14",
        "purchase": "slow cooker",
        "category": "appliances",
        "amount": "64.86",
        "related_items": "tongs",
        "frequently_bought_together": "cookbook",
        "city": "San Antonio",
        "state": "TX",
        "zip_code": 78006,
        "lat_lon": "29.852,-98.729"
      },
      {
        "customer_id": 100158,
        "date": "26-Jan-14",
        "purchase": "lawn mower",
        "category": "outdoor",
        "amount": "86.05",
        "related_items": "gardening gloves",
        "frequently_bought_together": "rakes",
        "city": "Hou",
        "state": "TX",
        "zip_code": 77005,
        "lat_lon": "29.718,-95.428"
      },
      {
        "customer_id": 100185,
        "date": "27-Jan-14",
        "purchase": "pants",
        "category": "clothing",
        "amount": "78.81",
        "related_items": "wallet",
        "frequently_bought_together": "wallet",
        "city": "San Antonio",
        "state": "TX",
        "zip_code": 78214,
        "lat_lon": "29.363,-98.49"
      },
      {
        "customer_id": 100103,
        "date": "28-Jan-14",
        "purchase": "audio",
        "category": "electronics",
        "amount": "78.61",
        "related_items": "headphones",
        "frequently_bought_together": "headphones",
        "city": "Houston",
        "state": "TX",
        "zip_code": 77012,
        "lat_lon": "29.72,-95.279"
      },
      {
        "customer_id": 100150,
        "date": "29-Jan-14",
        "purchase": "shorts",
        "category": "clothing",
        "amount": "36.21",
        "related_items": "t-shirts",
        "frequently_bought_together": "sunglasses",
        "city": "Philadelphia",
        "state": "PA",
        "zip_code": 19019,
        "lat_lon": "40.002,-75.118"
      },
      {
        "customer_id": 100183,
        "date": "30-Jan-14",
        "purchase": "shirts",
        "category": "clothing",
        "amount": "66.56",
        "related_items": "shortsleeve",
        "frequently_bought_together": "collared shirt",
        "city": "Phoenix",
        "state": "AZ",
        "zip_code": 85004,
        "lat_lon": "33.451,-112.071"
      },
      {
        "customer_id": 100111,
        "date": "31-Jan-14",
        "purchase": "snow shovel",
        "category": "outdoor",
        "amount": "77.28",
        "related_items": "mittens",
        "frequently_bought_together": "gloves",
        "city": "Phoenix",
        "state": "AZ",
        "zip_code": 85019,
        "lat_lon": "33.512,-112.142"
      },
      {
        "customer_id": 100160,
        "date": "1-Feb-14",
        "purchase": "tv",
        "category": "electronics",
        "amount": "89.36",
        "related_items": "speakers",
        "frequently_bought_together": "surround sound",
        "city": "San Jose",
        "state": "CA",
        "zip_code": 94560,
        "lat_lon": "37.536,-122.034"
      },
      {
        "customer_id": 100133,
        "date": "2-Feb-14",
        "purchase": "shirts",
        "category": "clothing",
        "amount": "23.69",
        "related_items": "collared shirt",
        "frequently_bought_together": "dress shirt",
        "city": "Los Angeles",
        "state": "CA",
        "zip_code": 90020,
        "lat_lon": "34.066,-118.309"
      },
      {
        "customer_id": 100158,
        "date": "3-Feb-14",
        "purchase": "snow shovel",
        "category": "outdoor",
        "amount": "85.69",
        "related_items": "mittens",
        "frequently_bought_together": "sand",
        "city": "Houston",
        "state": "TX",
        "zip_code": 77005,
        "lat_lon": "29.718,-95.428"
      },
      {
        "customer_id": 100193,
        "date": "4-Feb-14",
        "purchase": "microwave",
        "category": "appliances",
        "amount": "97.59",
        "related_items": "popcorn",
        "frequently_bought_together": "egg cooker",
        "city": "San Jose",
        "state": "CA",
        "zip_code": 95115,
        "lat_lon": "37.189,-121.705"
      },
      {
        "customer_id": 100167,
        "date": "5-Feb-14",
        "purchase": "food processor",
        "category": "appliances",
        "amount": "32.89",
        "related_items": "vegetable peeler",
        "frequently_bought_together": "vegetable peeler",
        "city": "New York City",
        "state": "NY",
        "zip_code": 10004,
        "lat_lon": "40.699,-74.041"
      },
      {
        "customer_id": 100102,
        "date": "6-Feb-14",
        "purchase": "soap",
        "category": "house",
        "amount": "70.66",
        "related_items": "shampoo",
        "frequently_bought_together": "loofah",
        "city": "Houston",
        "state": "TX",
        "zip_code": 77009,
        "lat_lon": "29.793,-95.367"
      },
      {
        "customer_id": 100167,
        "date": "7-Feb-14",
        "purchase": "soap",
        "category": "house",
        "amount": "76.69",
        "related_items": "body wash",
        "frequently_bought_together": "loofah",
        "city": "New York City",
        "state": "NY",
        "zip_code": 10004,
        "lat_lon": "40.699,-74.041"
      },
      {
        "customer_id": 100185,
        "date": "8-Feb-14",
        "purchase": "camera",
        "category": "electronics",
        "amount": "54.64",
        "related_items": "editing software",
        "frequently_bought_together": "camera case",
        "city": "San Antonio",
        "state": "TX",
        "zip_code": 78214,
        "lat_lon": "29.363,-98.49"
      },
      {
        "customer_id": 100140,
        "date": "9-Feb-14",
        "purchase": "food processor",
        "category": "appliances",
        "amount": "85.23",
        "related_items": "vegetable peeler",
        "frequently_bought_together": "vegetables",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 92037,
        "lat_lon": "32.839,-117.262"
      },
      {
        "customer_id": 100162,
        "date": "10-Feb-14",
        "purchase": "food processor",
        "category": "appliances",
        "amount": "70.18",
        "related_items": "vegetables",
        "frequently_bought_together": "tupperware",
        "city": "San Jose",
        "state": "CA",
        "zip_code": 94560,
        "lat_lon": "37.536,-122.034"
      },
      {
        "customer_id": 100123,
        "date": "11-Feb-14",
        "purchase": "slow cooker",
        "category": "appliances",
        "amount": "34.57",
        "related_items": "cookbook",
        "frequently_bought_together": "serving spoon",
        "city": "Los Angeles",
        "state": "CA",
        "zip_code": 90020,
        "lat_lon": "34.066,-118.309"
      },
      {
        "customer_id": 100186,
        "date": "12-Feb-14",
        "purchase": "slow cooker",
        "category": "appliances",
        "amount": "63.54",
        "related_items": "tongs",
        "frequently_bought_together": "tupperware",
        "city": "Houston",
        "state": "TX",
        "zip_code": 77009,
        "lat_lon": "29.793,-95.367"
      },
      {
        "customer_id": 100198,
        "date": "13-Feb-14",
        "purchase": "pants",
        "category": "clothing",
        "amount": "76.43",
        "related_items": "khakis ",
        "frequently_bought_together": "wallet",
        "city": "San Antonio",
        "state": "TX",
        "zip_code": 78206,
        "lat_lon": "29.438,-98.462"
      },
      {
        "customer_id": 100188,
        "date": "14-Feb-14",
        "purchase": "snow shovel",
        "category": "outdoor",
        "amount": "95.85",
        "related_items": "mittens",
        "frequently_bought_together": "sand",
        "city": "New York City",
        "state": "NY",
        "zip_code": 10002,
        "lat_lon": "40.717,-73.987"
      },
      {
        "customer_id": 100136,
        "date": "15-Feb-14",
        "purchase": "pants",
        "category": "clothing",
        "amount": "79.43",
        "related_items": "khakis ",
        "frequently_bought_together": "wallet",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60602,
        "lat_lon": "41.883,-87.629"
      },
      {
        "customer_id": 100162,
        "date": "16-Feb-14",
        "purchase": "shirts",
        "category": "clothing",
        "amount": "76.08",
        "related_items": "t-shirt",
        "frequently_bought_together": "dress shirt",
        "city": "San Jose",
        "state": "CA",
        "zip_code": 94560,
        "lat_lon": "37.536,-122.034"
      },
      {
        "customer_id": 100191,
        "date": "17-Feb-14",
        "purchase": "shirts",
        "category": "clothing",
        "amount": "57.33",
        "related_items": "shortsleeve",
        "frequently_bought_together": "button down shirt",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60605,
        "lat_lon": "41.86,-87.619"
      },
      {
        "customer_id": 100120,
        "date": "18-Feb-14",
        "purchase": "jackets",
        "category": "clothing",
        "amount": "86.29",
        "related_items": "scarfs",
        "frequently_bought_together": "winter gloves",
        "city": "Dallas",
        "state": "TX",
        "zip_code": 75001,
        "lat_lon": "32.961,-96.838"
      },
      {
        "customer_id": 100106,
        "date": "19-Feb-14",
        "purchase": "cell phone",
        "category": "electronics",
        "amount": "91.87",
        "related_items": "screen cleaner",
        "frequently_bought_together": "cell phone case",
        "city": "Dallas",
        "state": "TX",
        "zip_code": 75063,
        "lat_lon": "32.917,-96.973"
      },
      {
        "customer_id": 100192,
        "date": "20-Feb-14",
        "purchase": "pants",
        "category": "clothing",
        "amount": "78.11",
        "related_items": "wallet",
        "frequently_bought_together": "wallet",
        "city": "San Jose",
        "state": "CA",
        "zip_code": 94560,
        "lat_lon": "37.536,-122.034"
      },
      {
        "customer_id": 100107,
        "date": "21-Feb-14",
        "purchase": "paper products",
        "category": "household",
        "amount": "90.84",
        "related_items": "paper plates",
        "frequently_bought_together": "paper towels",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 92102,
        "lat_lon": "32.715,-117.125"
      },
      {
        "customer_id": 100142,
        "date": "22-Feb-14",
        "purchase": "flower pot",
        "category": "outdoor",
        "amount": "59.02",
        "related_items": "plant food",
        "frequently_bought_together": "flower seeds",
        "city": "Phoenix",
        "state": "AZ",
        "zip_code": 85001,
        "lat_lon": "33.704,-112.352"
      },
      {
        "customer_id": 100131,
        "date": "23-Feb-14",
        "purchase": "grill",
        "category": "outdoor",
        "amount": "49.41",
        "related_items": "grill cleaner",
        "frequently_bought_together": "steak seasoning",
        "city": "San Antonio",
        "state": "TX",
        "zip_code": 78206,
        "lat_lon": "29.438,-98.462"
      },
      {
        "customer_id": 100115,
        "date": "24-Feb-14",
        "purchase": "pants",
        "category": "clothing",
        "amount": "99.06",
        "related_items": "slacks",
        "frequently_bought_together": "khakis ",
        "city": "New York City",
        "state": "NY",
        "zip_code": 10013,
        "lat_lon": "40.721,-74.005"
      },
      {
        "customer_id": 100194,
        "date": "25-Feb-14",
        "purchase": "shirts",
        "category": "clothing",
        "amount": "77.83",
        "related_items": "button down shirt",
        "frequently_bought_together": "dress shirt",
        "city": "Philadelphia",
        "state": "PA",
        "zip_code": 19115,
        "lat_lon": "40.093,-75.041"
      },
      {
        "customer_id": 100133,
        "date": "26-Feb-14",
        "purchase": "car wash",
        "category": "outdoor",
        "amount": "49.57",
        "related_items": "wax",
        "frequently_bought_together": "tire cleaner",
        "city": "Los Angeles",
        "state": "CA",
        "zip_code": 90020,
        "lat_lon": "34.066,-118.309"
      },
      {
        "customer_id": 100108,
        "date": "27-Feb-14",
        "purchase": "pants",
        "category": "clothing",
        "amount": "90.84",
        "related_items": "slacks",
        "frequently_bought_together": "wallet",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 91911,
        "lat_lon": "32.609,-117.061"
      },
      {
        "customer_id": 100120,
        "date": "28-Feb-14",
        "purchase": "tv",
        "category": "electronics",
        "amount": "41.18",
        "related_items": "dvd player",
        "frequently_bought_together": "video game console",
        "city": "Dallas",
        "state": "TX",
        "zip_code": 75001,
        "lat_lon": "32.961,-96.838"
      },
      {
        "customer_id": 100191,
        "date": "1-Mar-14",
        "purchase": "jackets",
        "category": "clothing",
        "amount": "65.72",
        "related_items": "scarfs",
        "frequently_bought_together": "winter gloves",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60605,
        "lat_lon": "41.86,-87.619"
      },
      {
        "customer_id": 100189,
        "date": "2-Mar-14",
        "purchase": "slow cooker",
        "category": "appliances",
        "amount": "90.89",
        "related_items": "serving spoon",
        "frequently_bought_together": "tongs",
        "city": "Dallas",
        "state": "TX",
        "zip_code": 75001,
        "lat_lon": "32.961,-96.838"
      },
      {
        "customer_id": 100192,
        "date": "3-Mar-14",
        "purchase": "laptop",
        "category": "electronics",
        "amount": "46.34",
        "related_items": "charger",
        "frequently_bought_together": "wireless mouse",
        "city": "San Jose",
        "state": "CA",
        "zip_code": 94560,
        "lat_lon": "37.536,-122.034"
      },
      {
        "customer_id": 100132,
        "date": "4-Mar-14",
        "purchase": null,
        "category": "electronics",
        "amount": "97.54",
        "related_items": "subwoofer",
        "frequently_bought_together": "headphones",
        "city": "New York City",
        "state": "NY",
        "zip_code": 10013,
        "lat_lon": "40.721,-74.005"
      },
      {
        "customer_id": 100143,
        "date": "5-Mar-14",
        "purchase": null,
        "category": "clothing",
        "amount": "52.99",
        "related_items": "t-shirt",
        "frequently_bought_together": "shortsleeve",
        "city": "Phoenix",
        "state": "AZ",
        "zip_code": 85015,
        "lat_lon": "33.507,-112.103"
      },
      {
        "customer_id": 100101,
        "date": "6-Mar-14",
        "purchase": null,
        "category": "appliances",
        "amount": "51.46",
        "related_items": "mixing spoon",
        "frequently_bought_together": "vegetable peeler",
        "city": "Los Angeles",
        "state": "CA",
        "zip_code": 75001,
        "lat_lon": "34.09,-118.295"
      },
      {
        "customer_id": 100129,
        "date": "7-Mar-14",
        "purchase": null,
        "category": "clothing",
        "amount": "64.7",
        "related_items": "belts",
        "frequently_bought_together": "wallets",
        "city": "Dallas",
        "state": "TX",
        "zip_code": 75126,
        "lat_lon": "32.745,-96.46"
      },
      {
        "customer_id": 100100,
        "date": "8-Mar-14",
        "purchase": null,
        "category": "appliances",
        "amount": "98.25",
        "related_items": "bowls",
        "frequently_bought_together": "forks",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60610,
        "lat_lon": "41.899,-87.637"
      },
      {
        "customer_id": 100154,
        "date": "9-Mar-14",
        "purchase": "cell phone",
        "category": "electronics",
        "amount": "21.32",
        "related_items": "charger",
        "frequently_bought_together": "cell phone case",
        "city": "San Antonio",
        "state": "TX",
        "zip_code": 78206,
        "lat_lon": "29.438,-98.462"
      },
      {
        "customer_id": 100168,
        "date": "10-Mar-14",
        "purchase": "jackets",
        "category": "clothing",
        "amount": "58.43",
        "related_items": "winter gloves",
        "frequently_bought_together": "winter gloves",
        "city": "San Antonio",
        "state": "TX",
        "zip_code": 78109,
        "lat_lon": "29.502,-98.306"
      },
      {
        "customer_id": 100138,
        "date": "11-Mar-14",
        "purchase": "soap",
        "category": "household",
        "amount": "28.74",
        "related_items": "shampoo",
        "frequently_bought_together": "shampoo",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 91911,
        "lat_lon": "32.609,-117.061"
      },
      {
        "customer_id": 100165,
        "date": "12-Mar-14",
        "purchase": "tools",
        "category": "household",
        "amount": "61.12",
        "related_items": "drills ",
        "frequently_bought_together": "drill bits",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 91911,
        "lat_lon": "32.609,-117.061"
      },
      {
        "customer_id": 100111,
        "date": "13-Mar-14",
        "purchase": "slow cooker",
        "category": "appliances",
        "amount": "82.12",
        "related_items": "tupperware",
        "frequently_bought_together": "serving spoon",
        "city": "Phoenix",
        "state": "AZ",
        "zip_code": 85019,
        "lat_lon": "33.512,-112.142"
      },
      {
        "customer_id": 100124,
        "date": "14-Mar-14",
        "purchase": "soap",
        "category": "household",
        "amount": "58.73",
        "related_items": "body wash",
        "frequently_bought_together": "bar soap",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60603,
        "lat_lon": "41.88,-87.63"
      },
      {
        "customer_id": 100119,
        "date": "15-Mar-14",
        "purchase": "flower pot",
        "category": "outdoor",
        "amount": "26.66",
        "related_items": "plant food",
        "frequently_bought_together": "tomato stakes",
        "city": "San Antonio",
        "state": "TX",
        "zip_code": 78073,
        "lat_lon": "29.227,-98.609"
      },
      {
        "customer_id": 100116,
        "date": "16-Mar-14",
        "purchase": "car wash",
        "category": "outdoor",
        "amount": "72.4",
        "related_items": "sponge",
        "frequently_bought_together": "sponge",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 92027,
        "lat_lon": "33.143,-117.03"
      },
      {
        "customer_id": 100132,
        "date": "17-Mar-14",
        "purchase": "cell phone",
        "category": "electronics",
        "amount": "45.11",
        "related_items": "cell phone case",
        "frequently_bought_together": "cell phone case",
        "city": "New York City",
        "state": "NY",
        "zip_code": 10013,
        "lat_lon": "40.721,-74.005"
      },
      {
        "customer_id": 100106,
        "date": "18-Mar-14",
        "purchase": "microwave",
        "category": "appliances",
        "amount": "26.48",
        "related_items": "popcorn",
        "frequently_bought_together": "forks",
        "city": "Dallas",
        "state": "TX",
        "zip_code": 75063,
        "lat_lon": "32.917,-96.973"
      },
      {
        "customer_id": 100103,
        "date": "19-Mar-14",
        "purchase": "jackets",
        "category": "clothing",
        "amount": "46.02",
        "related_items": "scarfs",
        "frequently_bought_together": "scarfs",
        "city": "Houston",
        "state": "TX",
        "zip_code": 77012,
        "lat_lon": "29.72,-95.279"
      },
      {
        "customer_id": 100192,
        "date": "20-Mar-14",
        "purchase": "laptop",
        "category": "elect^ronics",
        "amount": "33.93",
        "related_items": "wireless mouse",
        "frequently_bought_together": "headphones",
        "city": "San Jose",
        "state": "CA",
        "zip_code": 94560,
        "lat_lon": "37.536,-122.034"
      },
      {
        "customer_id": 100180,
        "date": "21-Mar-14",
        "purchase": "jackets",
        "category": "clothing",
        "amount": "48.03",
        "related_items": "mittens",
        "frequently_bought_together": "winter gloves",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 92027,
        "lat_lon": "33.143,-117.03"
      },
      {
        "customer_id": 100165,
        "date": "22-Mar-14",
        "purchase": "detergent",
        "category": "household",
        "amount": "81.56",
        "related_items": "dryer sheets",
        "frequently_bought_together": "fabric softener",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 91911,
        "lat_lon": "32.609,-117.061"
      },
      {
        "customer_id": 100116,
        "date": "23-Mar-14",
        "purchase": "car wash",
        "category": "outdoor",
        "amount": "23.34",
        "related_items": "towels",
        "frequently_bought_together": "wax",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 92027,
        "lat_lon": "33.143,-117.03"
      },
      {
        "customer_id": 100149,
        "date": "24-Mar-14",
        "purchase": "cell phone",
        "category": "electronics",
        "amount": "70.36",
        "related_items": "charger",
        "frequently_bought_together": "cell phone case",
        "city": "Houston",
        "state": "TX",
        "zip_code": 77009,
        "lat_lon": "29.793,-95.367"
      },
      {
        "customer_id": 100118,
        "date": "25-Mar-14",
        "purchase": "shirts",
        "category": "clothing",
        "amount": "82.35",
        "related_items": "shortsleeve",
        "frequently_bought_together": "shortsleeve",
        "city": "Philadelphia",
        "state": "PA",
        "zip_code": 19102,
        "lat_lon": "39.953,-75.166"
      },
      {
        "customer_id": 100128,
        "date": "26-Mar-14",
        "purchase": "detergent",
        "category": "household",
        "amount": "94.16",
        "related_items": "dryer sheets",
        "frequently_bought_together": "bleach",
        "city": "Phoenix",
        "state": "AZ",
        "zip_code": 60603,
        "lat_lon": "33.507,-112.103"
      },
      {
        "customer_id": 100142,
        "date": "27-Mar-14",
        "purchase": "detergent",
        "category": "household",
        "amount": "91.23",
        "related_items": "bleach",
        "frequently_bought_together": "fabric softener",
        "city": "Phoenix",
        "state": "AZ",
        "zip_code": 85001,
        "lat_lon": "33.704,-112.352"
      },
      {
        "customer_id": 100195,
        "date": "28-Mar-14",
        "purchase": "car wash",
        "category": "outdoor",
        "amount": "81.17",
        "related_items": "buckets",
        "frequently_bought_together": "towels",
        "city": "Philadelphia",
        "state": "PA",
        "zip_code": 19102,
        "lat_lon": "39.953,-75.166"
      },
      {
        "customer_id": 100123,
        "date": "29-Mar-14",
        "purchase": "shirts",
        "category": "clothing",
        "amount": "89.68",
        "related_items": "collared shirt",
        "frequently_bought_together": "shortsleeve",
        "city": "Los Angeles",
        "state": "CA",
        "zip_code": 90020,
        "lat_lon": "34.066,-118.309"
      },
      {
        "customer_id": 100145,
        "date": "30-Mar-14",
        "purchase": "blender",
        "category": "appliances",
        "amount": "74.52",
        "related_items": "pitcher",
        "frequently_bought_together": "straws",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60603,
        "lat_lon": "41.88,-87.63"
      },
      {
        "customer_id": 100199,
        "date": "31-Mar-14",
        "purchase": null,
        "category": "clothing",
        "amount": "26.81",
        "related_items": "sunglasses",
        "frequently_bought_together": "sunglasses",
        "city": "Dallas",
        "state": "TX",
        "zip_code": 75089,
        "lat_lon": "32.924,-96.547"
      },
      {
        "customer_id": 100167,
        "date": "1-Apr-14",
        "purchase": null,
        "category": "appliances",
        "amount": "58.97",
        "related_items": "cookbook",
        "frequently_bought_together": "tupperware",
        "city": "New York City",
        "state": "NY",
        "zip_code": 10004,
        "lat_lon": "40.699,-74.041"
      },
      {
        "customer_id": 100187,
        "date": "2-Apr-14",
        "purchase": null,
        "category": "outdoor",
        "amount": "90.37",
        "related_items": "rakes",
        "frequently_bought_together": "gardening gloves",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 91911,
        "lat_lon": "41.905,-87.625"
      },
      {
        "customer_id": 100156,
        "date": "3-Apr-14",
        "purchase": null,
        "category": "electronics",
        "amount": "37.32",
        "related_items": "charger",
        "frequently_bought_together": "headphones",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 91911,
        "lat_lon": "32.609,-117.061"
      },
      {
        "customer_id": 100166,
        "date": "4-Apr-14",
        "purchase": null,
        "category": "electronics",
        "amount": "44.31",
        "related_items": "surround sound",
        "frequently_bought_together": "dvd player",
        "city": "Philadelphia",
        "state": "PA",
        "zip_code": 19115,
        "lat_lon": "40.093,-75.041"
      },
      {
        "customer_id": 100124,
        "date": "5-Apr-14",
        "purchase": null,
        "category": "appliances",
        "amount": "53.94",
        "related_items": "cookbook",
        "frequently_bought_together": "tongs",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60603,
        "lat_lon": "41.88,-87.63"
      },
      {
        "customer_id": 100162,
        "date": "6-Apr-14",
        "purchase": "paper products",
        "category": "household",
        "amount": "69.28",
        "related_items": "paper towels",
        "frequently_bought_together": "toilet paper",
        "city": "San Jose",
        "state": "CA",
        "zip_code": 94560,
        "lat_lon": "37.536,-122.034"
      },
      {
        "customer_id": 100187,
        "date": "7-Apr-14",
        "purchase": "audio",
        "category": "electronics",
        "amount": "65.79",
        "related_items": "earbuds",
        "frequently_bought_together": "headphones",
        "city": "Chicago",
        "state": "IL",
        "zip_code": 60611,
        "lat_lon": "41.905,-87.625"
      },
      {
        "customer_id": 100186,
        "date": "8-Apr-14",
        "purchase": "laptop",
        "category": "electronics",
        "amount": "97.6",
        "related_items": "charger",
        "frequently_bought_together": "charger",
        "city": "Houston",
        "state": "TX",
        "zip_code": 77009,
        "lat_lon": "29.793,-95.367"
      },
      {
        "customer_id": 100190,
        "date": "9-April-2014",
        "purchase": "tv",
        "category": "electronics",
        "amount": "61.33",
        "related_items": "speakers",
        "frequently_bought_together": "dvd player",
        "city": "Dallas",
        "state": "TX",
        "zip_code": 75089,
        "lat_lon": "32.924,-96.547"
      },
      {
        "customer_id": 100152,
        "date": "10-April-2014",
        "purchase": "tools",
        "category": "household",
        "amount": "90.48",
        "related_items": "hammers",
        "frequently_bought_together": "drills ",
        "city": "Dallas",
        "state": "TX",
        "zip_code": 75126,
        "lat_lon": "32.745,-96.46"
      },
      {
        "customer_id": 100103,
        "date": "11-April-2014",
        "purchase": "slow cooker",
        "category": "appliances",
        "amount": "86.52",
        "related_items": "pot holders",
        "frequently_bought_together": "cookbook",
        "city": "Houston",
        "state": "TX",
        "zip_code": 77012,
        "lat_lon": "29.72,-95.279"
      },
      {
        "customer_id": 100194,
        "date": "12-April-2014",
        "purchase": "camera",
        "category": "electronics",
        "amount": "67.2",
        "related_items": "editing software",
        "frequently_bought_together": "lens cleaner",
        "city": "Philadelphia",
        "state": "PA",
        "zip_code": 19115,
        "lat_lon": "40.093,-75.041"
      },
      {
        "customer_id": 100130,
        "date": "13-April-2014",
        "purchase": "blender",
        "category": "appliances",
        "amount": "25.83",
        "related_items": "pitcher",
        "frequently_bought_together": "fruit",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 92107,
        "lat_lon": "32.741,-117.244"
      },
      {
        "customer_id": 100152,
        "date": "14-April-2014",
        "purchase": "car wash",
        "category": "outdoor",
        "amount": "50.12",
        "related_items": "tire cleaner",
        "frequently_bought_together": "wax",
        "city": "Dallas",
        "state": "TX",
        "zip_code": 75126,
        "lat_lon": "32.745,-96.46"
      },
      {
        "customer_id": 100140,
        "date": "15-April-2014",
        "purchase": "shirts",
        "category": "clothing",
        "amount": "53.09",
        "related_items": "t-shirt",
        "frequently_bought_together": "button down shirt",
        "city": "San Diego",
        "state": "CA",
        "zip_code": 92037,
        "lat_lon": "32.839,-117.262"
      }
    ]
    

After getting a feel for the data and the different fields, I utilized the Pandas library to import the data into a Pandas dataframe. This is a table-like format in Pandas that makes the data easier to work with for cleaning and reshaping purposes.


```python
import pandas as pd
df = pd.read_json("customer_data_example.json")

df
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
      <td>None</td>
      <td>towels</td>
      <td>IL</td>
      <td>60605</td>
    </tr>
    <tr>
      <th>1</th>
      <td>35.00</td>
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
    <tr>
      <th>5</th>
      <td>29.16</td>
      <td>outdoor</td>
      <td>San Diego</td>
      <td>100116</td>
      <td>2014-01-06</td>
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
      <td>2014-01-07</td>
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
      <td>2014-01-08</td>
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
      <td>2014-01-09</td>
      <td>pot holders</td>
      <td>39.953,-75.166</td>
      <td>None</td>
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
      <td>2014-01-10</td>
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
      <td>2014-01-11</td>
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
      <td>2014-01-12</td>
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
      <td>2014-01-13</td>
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
      <td>2014-01-14</td>
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
      <td>2014-01-15</td>
      <td>t shirt</td>
      <td>41.86,-87.619</td>
      <td>shirts</td>
      <td>t-shirt</td>
      <td>IL</td>
      <td>60605</td>
    </tr>
    <tr>
      <th>15</th>
      <td>75.00</td>
      <td>appliances</td>
      <td>San Antonio</td>
      <td>100185</td>
      <td>2014-01-16</td>
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
      <td>2014-01-17</td>
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
      <td>2014-01-18</td>
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
      <td>2014-01-19</td>
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
      <td>2014-01-20</td>
      <td>surround sound</td>
      <td>41.88,-87.63</td>
      <td>tv</td>
      <td>surround sound</td>
      <td>IL</td>
      <td>60603</td>
    </tr>
    <tr>
      <th>20</th>
      <td>53.80</td>
      <td>household</td>
      <td>New York City</td>
      <td>100188</td>
      <td>2014-01-21</td>
      <td>paper towels</td>
      <td>40.717,-73.987</td>
      <td>n/a</td>
      <td>toilet paper</td>
      <td>NY</td>
      <td>10002</td>
    </tr>
    <tr>
      <th>21</th>
      <td>85.00</td>
      <td>appliances</td>
      <td>San Jose</td>
      <td>100192</td>
      <td>2014-01-22</td>
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
      <td>2014-01-23</td>
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
      <td>2014-01-24</td>
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
      <td>2014-01-25</td>
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
      <td>2014-01-26</td>
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
      <td>2014-01-27</td>
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
      <td>2014-01-28</td>
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
      <td>2014-01-29</td>
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
      <td>2014-01-30</td>
      <td>collared shirt</td>
      <td>33.451,-112.071</td>
      <td>shirts</td>
      <td>shortsleeve</td>
      <td>AZ</td>
      <td>85004</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>75</th>
      <td>45.11</td>
      <td>electronics</td>
      <td>New York City</td>
      <td>100132</td>
      <td>2014-03-17</td>
      <td>cell phone case</td>
      <td>40.721,-74.005</td>
      <td>cell phone</td>
      <td>cell phone case</td>
      <td>NY</td>
      <td>10013</td>
    </tr>
    <tr>
      <th>76</th>
      <td>26.48</td>
      <td>appliances</td>
      <td>Dallas</td>
      <td>100106</td>
      <td>2014-03-18</td>
      <td>forks</td>
      <td>32.917,-96.973</td>
      <td>microwave</td>
      <td>popcorn</td>
      <td>TX</td>
      <td>75063</td>
    </tr>
    <tr>
      <th>77</th>
      <td>46.02</td>
      <td>clothing</td>
      <td>Houston</td>
      <td>100103</td>
      <td>2014-03-19</td>
      <td>scarfs</td>
      <td>29.72,-95.279</td>
      <td>jackets</td>
      <td>scarfs</td>
      <td>TX</td>
      <td>77012</td>
    </tr>
    <tr>
      <th>78</th>
      <td>33.93</td>
      <td>elect^ronics</td>
      <td>San Jose</td>
      <td>100192</td>
      <td>2014-03-20</td>
      <td>headphones</td>
      <td>37.536,-122.034</td>
      <td>laptop</td>
      <td>wireless mouse</td>
      <td>CA</td>
      <td>94560</td>
    </tr>
    <tr>
      <th>79</th>
      <td>48.03</td>
      <td>clothing</td>
      <td>San Diego</td>
      <td>100180</td>
      <td>2014-03-21</td>
      <td>winter gloves</td>
      <td>33.143,-117.03</td>
      <td>jackets</td>
      <td>mittens</td>
      <td>CA</td>
      <td>92027</td>
    </tr>
    <tr>
      <th>80</th>
      <td>81.56</td>
      <td>household</td>
      <td>San Diego</td>
      <td>100165</td>
      <td>2014-03-22</td>
      <td>fabric softener</td>
      <td>32.609,-117.061</td>
      <td>detergent</td>
      <td>dryer sheets</td>
      <td>CA</td>
      <td>91911</td>
    </tr>
    <tr>
      <th>81</th>
      <td>23.34</td>
      <td>outdoor</td>
      <td>San Diego</td>
      <td>100116</td>
      <td>2014-03-23</td>
      <td>wax</td>
      <td>33.143,-117.03</td>
      <td>car wash</td>
      <td>towels</td>
      <td>CA</td>
      <td>92027</td>
    </tr>
    <tr>
      <th>82</th>
      <td>70.36</td>
      <td>electronics</td>
      <td>Houston</td>
      <td>100149</td>
      <td>2014-03-24</td>
      <td>cell phone case</td>
      <td>29.793,-95.367</td>
      <td>cell phone</td>
      <td>charger</td>
      <td>TX</td>
      <td>77009</td>
    </tr>
    <tr>
      <th>83</th>
      <td>82.35</td>
      <td>clothing</td>
      <td>Philadelphia</td>
      <td>100118</td>
      <td>2014-03-25</td>
      <td>shortsleeve</td>
      <td>39.953,-75.166</td>
      <td>shirts</td>
      <td>shortsleeve</td>
      <td>PA</td>
      <td>19102</td>
    </tr>
    <tr>
      <th>84</th>
      <td>94.16</td>
      <td>household</td>
      <td>Phoenix</td>
      <td>100128</td>
      <td>2014-03-26</td>
      <td>bleach</td>
      <td>33.507,-112.103</td>
      <td>detergent</td>
      <td>dryer sheets</td>
      <td>AZ</td>
      <td>60603</td>
    </tr>
    <tr>
      <th>85</th>
      <td>91.23</td>
      <td>household</td>
      <td>Phoenix</td>
      <td>100142</td>
      <td>2014-03-27</td>
      <td>fabric softener</td>
      <td>33.704,-112.352</td>
      <td>detergent</td>
      <td>bleach</td>
      <td>AZ</td>
      <td>85001</td>
    </tr>
    <tr>
      <th>86</th>
      <td>81.17</td>
      <td>outdoor</td>
      <td>Philadelphia</td>
      <td>100195</td>
      <td>2014-03-28</td>
      <td>towels</td>
      <td>39.953,-75.166</td>
      <td>car wash</td>
      <td>buckets</td>
      <td>PA</td>
      <td>19102</td>
    </tr>
    <tr>
      <th>87</th>
      <td>89.68</td>
      <td>clothing</td>
      <td>Los Angeles</td>
      <td>100123</td>
      <td>2014-03-29</td>
      <td>shortsleeve</td>
      <td>34.066,-118.309</td>
      <td>shirts</td>
      <td>collared shirt</td>
      <td>CA</td>
      <td>90020</td>
    </tr>
    <tr>
      <th>88</th>
      <td>74.52</td>
      <td>appliances</td>
      <td>Chicago</td>
      <td>100145</td>
      <td>2014-03-30</td>
      <td>straws</td>
      <td>41.88,-87.63</td>
      <td>blender</td>
      <td>pitcher</td>
      <td>IL</td>
      <td>60603</td>
    </tr>
    <tr>
      <th>89</th>
      <td>26.81</td>
      <td>clothing</td>
      <td>Dallas</td>
      <td>100199</td>
      <td>2014-03-31</td>
      <td>sunglasses</td>
      <td>32.924,-96.547</td>
      <td>None</td>
      <td>sunglasses</td>
      <td>TX</td>
      <td>75089</td>
    </tr>
    <tr>
      <th>90</th>
      <td>58.97</td>
      <td>appliances</td>
      <td>New York City</td>
      <td>100167</td>
      <td>2014-04-01</td>
      <td>tupperware</td>
      <td>40.699,-74.041</td>
      <td>None</td>
      <td>cookbook</td>
      <td>NY</td>
      <td>10004</td>
    </tr>
    <tr>
      <th>91</th>
      <td>90.37</td>
      <td>outdoor</td>
      <td>Chicago</td>
      <td>100187</td>
      <td>2014-04-02</td>
      <td>gardening gloves</td>
      <td>41.905,-87.625</td>
      <td>None</td>
      <td>rakes</td>
      <td>IL</td>
      <td>91911</td>
    </tr>
    <tr>
      <th>92</th>
      <td>37.32</td>
      <td>electronics</td>
      <td>San Diego</td>
      <td>100156</td>
      <td>2014-04-03</td>
      <td>headphones</td>
      <td>32.609,-117.061</td>
      <td>None</td>
      <td>charger</td>
      <td>CA</td>
      <td>91911</td>
    </tr>
    <tr>
      <th>93</th>
      <td>44.31</td>
      <td>electronics</td>
      <td>Philadelphia</td>
      <td>100166</td>
      <td>2014-04-04</td>
      <td>dvd player</td>
      <td>40.093,-75.041</td>
      <td>None</td>
      <td>surround sound</td>
      <td>PA</td>
      <td>19115</td>
    </tr>
    <tr>
      <th>94</th>
      <td>53.94</td>
      <td>appliances</td>
      <td>Chicago</td>
      <td>100124</td>
      <td>2014-04-05</td>
      <td>tongs</td>
      <td>41.88,-87.63</td>
      <td>None</td>
      <td>cookbook</td>
      <td>IL</td>
      <td>60603</td>
    </tr>
    <tr>
      <th>95</th>
      <td>69.28</td>
      <td>household</td>
      <td>San Jose</td>
      <td>100162</td>
      <td>2014-04-06</td>
      <td>toilet paper</td>
      <td>37.536,-122.034</td>
      <td>paper products</td>
      <td>paper towels</td>
      <td>CA</td>
      <td>94560</td>
    </tr>
    <tr>
      <th>96</th>
      <td>65.79</td>
      <td>electronics</td>
      <td>Chicago</td>
      <td>100187</td>
      <td>2014-04-07</td>
      <td>headphones</td>
      <td>41.905,-87.625</td>
      <td>audio</td>
      <td>earbuds</td>
      <td>IL</td>
      <td>60611</td>
    </tr>
    <tr>
      <th>97</th>
      <td>97.60</td>
      <td>electronics</td>
      <td>Houston</td>
      <td>100186</td>
      <td>2014-04-08</td>
      <td>charger</td>
      <td>29.793,-95.367</td>
      <td>laptop</td>
      <td>charger</td>
      <td>TX</td>
      <td>77009</td>
    </tr>
    <tr>
      <th>98</th>
      <td>61.33</td>
      <td>electronics</td>
      <td>Dallas</td>
      <td>100190</td>
      <td>2014-04-09</td>
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
      <td>2014-04-10</td>
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
      <td>2014-04-11</td>
      <td>cookbook</td>
      <td>29.72,-95.279</td>
      <td>slow cooker</td>
      <td>pot holders</td>
      <td>TX</td>
      <td>77012</td>
    </tr>
    <tr>
      <th>101</th>
      <td>67.20</td>
      <td>electronics</td>
      <td>Philadelphia</td>
      <td>100194</td>
      <td>2014-04-12</td>
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
      <td>2014-04-13</td>
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
      <td>2014-04-14</td>
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
      <td>2014-04-15</td>
      <td>button down shirt</td>
      <td>32.839,-117.262</td>
      <td>shirts</td>
      <td>t-shirt</td>
      <td>CA</td>
      <td>92037</td>
    </tr>
  </tbody>
</table>
<p>105 rows × 11 columns</p>
</div>



I also took a look at the data types for each field.


```python
df.dtypes
```




    amount                               float64
    category                              object
    city                                  object
    customer_id                            int64
    date                          datetime64[ns]
    frequently_bought_together            object
    lat_lon                               object
    purchase                              object
    related_items                         object
    state                                 object
    zip_code                               int64
    dtype: object



After importing the JSON data, I imported the XML data. I did this by first parsing the XML data to collect the tags and elements to store in a dictionary. The dictionary was then converted to a dataframe.


```python
import xml.etree.ElementTree as ET
tree = ET.parse('location_data.xml')
root = tree.getroot()

# root tag
print(root.tag)

# child tag
print(root[0].tag)

# number of children elements
num_children = len(root.getchildren())
print(num_children)

# number of subchildren elements
num_subchildren = len(root[0].getchildren())
print(num_subchildren)
    
    
# pulling out all of the subchildren tags
tags = []
for subchild in root[0]:
    tags.append(subchild.tag)
print(tags)
    

# creating an empty dictionary to store the data
d = {}
for tag in tags:
    d[tag] = []
print(d)


# pulling out all of the data
for i in range(0, num_children):
    for j in range(0, num_subchildren):
        value = root[i][j].text
        d[tags[j]].append(value)
        
#print(d)


# converting to a dataframe
df = pd.DataFrame(data=d)

print(df)
```

    data-set
    record
    50
    3
    ['City', 'Zipcode', 'Latitude_Longitude']
    {'City': [], 'Zipcode': [], 'Latitude_Longitude': []}
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
    

With the JSON and XML data in dataframe format, I could more easily clean and reshape the data.

## 2. Cleaning the Data
After importing the data I worked through the data cleaning plan that I outlined above. This four step process involved the following steps:

1. Missing Values
2. Correct Data Types
3. Consistent Data
4. Accurate Data

Each feature was investigated and cleaned for missing values, correct data types, and consistent data. The only data that needed to be checked for accuracy was the "zip_code" data. You can find the full data cleaning notebook for each feature on my github page *[provide link to your github page here]*.

As an example of my data cleaning process I'll go through detecting and cleaning missing values for the "purchase" column.

After importing the JSON data in to a pandas dataframe, I summed up the amount of missing values.


```python
# summing the missing values
print(sum(df["purchase"].isna()))
```

    14
    

Taking a look I could see that there was 14 missing values detected by Pandas. These are default missing values that Pandas detected right away. I was also curious in looking for other potential missing values, so I used the "unique()" method.


```python
# looking for non-standard missing values
print(df["purchase"].unique())
```

    [None 'shorts' 'lawn_mower' 'laptop' 'car wash' 'lawn mower' 'grill'
     'household cleaner' 'camera' 'snow shovel' 'shoes' 'blender' 'shirts'
     'toaster' 'detergent' 'tv' 'n/a' 'tools' 'slow cooker' 'pants' 'audio'
     'microwave' 'food processor' 'soap' '--' 'jackets' 'cell phone' 'N/A'
     'paper products' 'flower pot']
    

There's three unique values that look like missing values. Pandas did not detect these. They are the following:
- 'n/a'
- '--'
- 'N/A'

To clean these values I put them in to an array called "missing_values", and then looped through the "purchase" column to look for those values, and then change them to a new class called "unavailable".


```python
missing_values = ["n/a", "--", "N/A"]

cnt = 0
for i in df["purchase"]:
    if i in missing_values:
        df.loc[cnt, "purchase"] = "unavailable"
    cnt+=1

print(df["purchase"].unique())
```

    [None 'shorts' 'lawn_mower' 'laptop' 'car wash' 'lawn mower' 'grill'
     'household cleaner' 'camera' 'snow shovel' 'shoes' 'blender' 'shirts'
     'toaster' 'detergent' 'tv' 'unavailable' 'tools' 'slow cooker' 'pants'
     'audio' 'microwave' 'food processor' 'soap' 'jackets' 'cell phone'
     'paper products' 'flower pot']
    

Taking a look, all three of the non-standard missing values were replaced with the new class label, "unavailable". 

Finally, I finished up by replacing the standard missing value types using the "fillna()" method.


```python
df["purchase"].fillna("unavailable", inplace=True)
print(sum(df["purchase"].isna()))
print(df["purchase"].unique())
```

    0
    ['unavailable' 'shorts' 'lawn_mower' 'laptop' 'car wash' 'lawn mower'
     'grill' 'household cleaner' 'camera' 'snow shovel' 'shoes' 'blender'
     'shirts' 'toaster' 'detergent' 'tv' 'tools' 'slow cooker' 'pants' 'audio'
     'microwave' 'food processor' 'soap' 'jackets' 'cell phone'
     'paper products' 'flower pot']
    

Taking a final look at the "purchase" column using the "sum()" and "unique()" methods confirms that all missing values have been detected and changed to "unavailable".

Sometimes missing data can provide additional information, so rather than throwing it out I decided to label all of it and keep it. I would consult with my team and the marketing group before disposing of it. The missing data could convey valuable information about customer experience, so it's better to keep that data for now.

For the full data cleaning notebook, please refer to my github page *[provide link to your github page here]*.

## 3. Reshaping the Data
The final part is reshaping the data. Talk about how you used "pivot_table" to display the data in the correct format. This is the format requested by the hypothetical sales department in this project.

After importing and cleaning the data, the final step was to reshape the data.

During the cleaning portion the cleaned dataset was exported as a clean CSV, so I'm going to import and reshape that clean dataset.

I'll start by importing the clean dataset, "customer_data_cleaned.csv".


```python
df = pd.read_csv("customer_data_cleaned.csv")
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
      <th>Unnamed: 0</th>
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
      <td>0</td>
      <td>24.64</td>
      <td>household</td>
      <td>Chicago</td>
      <td>100191</td>
      <td>2014-01-01</td>
      <td>towels</td>
      <td>41.86,-87.619</td>
      <td>NaN</td>
      <td>towels</td>
      <td>IL</td>
      <td>60605</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>35.00</td>
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
      <td>2</td>
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
      <td>3</td>
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
      <td>4</td>
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



The marketing department is interested in lookin at how much each customer spends in each category.

To make it easier for them to look at this data, I'll subset my full dataframe, and reshape it using the "pivot_table" method. Since they're probably interested in total spending in each category, I'll use the "sum" method from Numpy as my aggregation function.


```python
# pivot table; aggregation function "sum"
import numpy as np
df_subset = df[["customer_id", "category", "amount"]]
#print(df_subset)

df_pivot = df_subset.pivot_table(index="customer_id", columns="category", values="amount", aggfunc=np.sum)
print(df_pivot)
```

    category     appliances  clothing  electronics  household  outdoor
    customer_id                                                       
    100100            98.25       NaN          NaN        NaN      NaN
    100101            51.46       NaN          NaN        NaN      NaN
    100102              NaN       NaN          NaN      70.66      NaN
    100103            86.52     46.02        78.61        NaN      NaN
    100105              NaN       NaN          NaN        NaN    50.71
    100106            26.48       NaN       183.88        NaN      NaN
    100107              NaN       NaN          NaN      90.84      NaN
    100108              NaN     90.84          NaN        NaN      NaN
    100109              NaN       NaN          NaN        NaN    31.79
    100111            82.12       NaN          NaN        NaN    77.28
    100115              NaN     99.06          NaN        NaN      NaN
    100116              NaN       NaN          NaN        NaN   166.81
    100118            30.55     82.35          NaN        NaN      NaN
    100119              NaN       NaN          NaN        NaN    26.66
    100120              NaN     86.29        41.18        NaN      NaN
    100123            34.57     89.68          NaN        NaN      NaN
    100124            53.94       NaN        89.93      58.73      NaN
    100128              NaN       NaN          NaN      94.16      NaN
    100129              NaN     64.70          NaN        NaN      NaN
    100130            25.83       NaN          NaN        NaN      NaN
    100131              NaN       NaN          NaN        NaN    49.41
    100132              NaN       NaN       142.65        NaN      NaN
    100133              NaN     23.69          NaN        NaN    49.57
    100136              NaN     79.43          NaN        NaN      NaN
    100138              NaN       NaN          NaN      28.74      NaN
    100140            85.23     53.09          NaN      85.92      NaN
    100142              NaN       NaN          NaN      91.23    59.02
    100143              NaN     52.99          NaN        NaN      NaN
    100145            74.52       NaN          NaN        NaN      NaN
    100148              NaN       NaN          NaN      35.03      NaN
    ...                 ...       ...          ...        ...      ...
    100153              NaN     96.87        87.08        NaN      NaN
    100154              NaN       NaN        21.32        NaN      NaN
    100156              NaN       NaN        37.32        NaN      NaN
    100158              NaN       NaN          NaN        NaN   171.74
    100159              NaN     91.98          NaN        NaN      NaN
    100160              NaN       NaN        89.36        NaN      NaN
    100162            70.18     76.08          NaN      69.28      NaN
    100165              NaN       NaN          NaN     142.68      NaN
    100166              NaN       NaN        44.31        NaN      NaN
    100167            91.86       NaN          NaN      76.69      NaN
    100168              NaN     58.43          NaN        NaN      NaN
    100170              NaN       NaN          NaN        NaN    89.72
    100173              NaN       NaN          NaN        NaN    81.75
    100180              NaN     48.03          NaN        NaN      NaN
    100182            64.86       NaN          NaN        NaN      NaN
    100183              NaN     66.56          NaN        NaN      NaN
    100185            75.00     78.81        54.64        NaN      NaN
    100186            63.54       NaN        97.60        NaN      NaN
    100187              NaN       NaN        65.79        NaN    90.37
    100188              NaN       NaN          NaN      53.80    95.85
    100189            90.89       NaN          NaN        NaN      NaN
    100190              NaN       NaN        61.33        NaN      NaN
    100191              NaN    159.16          NaN      24.64      NaN
    100192            85.00     78.11        80.27        NaN      NaN
    100193            97.59       NaN          NaN        NaN      NaN
    100194              NaN     77.83        67.20        NaN      NaN
    100195              NaN       NaN          NaN        NaN    81.17
    100196              NaN     27.37          NaN        NaN      NaN
    100198              NaN     76.43          NaN        NaN      NaN
    100199              NaN     61.81          NaN        NaN      NaN
    
    [64 rows x 5 columns]
    

Taking a look, we now have a more neatly shaped dataframe for the marketing department. The total amount that each customer has spent in each category is shown. A lot of customers didn't spend any money in certain categories, which is represented by "NaN".

## Conclusion

In this project I cleaned a messy JSON dataset. I also worked with XML data, and delivered my cleaned dataset in CSV format.

I worked through a data cleaning plan that involved investigating and cleaning the dataset for missing values, incorrect data types, inconsistent data, and data inaccuracies.

Finally, the data was reshaped to more concisely organize the data in the format requested by the marketing department. This reshaped format would make it easier for them to investigate spending trends of each customer based on the various categories.

It's important to investigate and clean data because dirty data can lead to errors during exploratory analysis and machine learning.
04-2020/ Nick Scherer.
