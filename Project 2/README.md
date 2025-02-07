
# **New York City Airbnb Analysis**

## **Project Overview**
This project analyzes **Airbnb listings in New York City**, using the [KAGGLE](https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data) dataset. The dataset includes information on listings, hosts, pricing, reviews, availability, and location data.

I performed **data cleaning** using **Python (pandas)** and created visualizations in **Power BI** to uncover key insights about Airbnb trends in NYC.

---

## **Dataset Information**
### **Source:**
[LINK](https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data)

### **Size:**
- **Rows:** 48,895
- **Columns:** 16

### **Columns & Descriptions:**
| Column | Description |
|---------|------------|
| `id` | Unique listing ID |
| `name` | Name of the listing |
| `host_id` | Unique host ID |
| `host_name` | Name of the host |
| `neighbourhood_group` | NYC borough (e.g., Manhattan, Brooklyn) |
| `neighbourhood` | Specific neighborhood within the borough |
| `latitude` | Geographic coordinate |
| `longitude` | Geographic coordinate |
| `room_type` | Type of room (e.g., Entire home/apt, Private room) |
| `price` | Price per night (USD) |
| `minimum_nights` | Minimum nights required to book |
| `number_of_reviews` | Total reviews received |
| `last_review` | Date of the most recent review |
| `reviews_per_month` | Average monthly reviews |
| `calculated_host_listings_count` | Total listings owned by the host |
| `availability_365` | Number of available days per year |

---

## **Data Cleaning Process**
Before analyzing the data, I **cleaned and processed** the dataset in Python:

### **1. Handling Missing Values**
I identified missing values in the dataset:

| Column | Missing Values | 
|--------|---------------|
| `last_review` | 10,052 |
| `reviews_per_month` | 10,052 |
| `host_name` | 21 |
| `name` | 16 |

**Solutions:**
- `last_review`: I left this has it is, because when I tried replacing with ‘no review’, I could not change the data type to **DateTime**.
- `reviews_per_month`: Filled missing values with `0`.
- `host_name` & `name`: Filled missing values with `"Unknown"`.

### **2. Fixing Data Types**
Some columns had incorrect data types. Which I corrected them as follows:

| Column | Initial Type | Corrected Type |
|--------|-------------|---------------|
| ‘latitude’| Object | float |
| ‘last_review| Object | DateTime |

**Code Used to Fix Data Types:**
```python
import pandas as pd

# Convert last_review to datetime
df['last_review'] = pd.to_datetime(df['last_review'], dayfirst=True, errors='coerce')

# Convert latitude to float
df[‘latitude’] = pd.numeric(df[‘latitude’], errors =‘coerce’)

```

### **3. Removing Unwanted Characters**
Some columns contained non-ASCII characters, which I removed:

![Image](https://github.com/user-attachments/assets/fa72eb9c-9e72-4ad1-b273-1eee84af2793)


### **4. Final Cleaning Steps**
- Removed unnecessary spaces.
- Reset the index after removing missing values.
```python
df.reset_index(drop=True, inplace=True)
```

---

## **Power BI Visualizations & Insights**
After cleaning, I used **Power BI** to create dashboards. Below are the key insights from the analysis:

### **1. Number of Listings by Neighborhood**
**Insight:**
- Williamsburg and Bedford-Stuyvesant (both in Brooklyn) have the highest number of listings.
- Harlem and Upper West Side (Manhattan) also have significant listings.

**Conclusion:**
Brooklyn and Manhattan dominate the Airbnb market in NYC.

---

### **2. Distribution of Room Types**
**Insight:**
- **Entire home/apartments** are the most common (~50% of listings).
- **Private rooms** are also popular (~45%).
- **Shared rooms** make up a small fraction.

**Conclusion:**
Most Airbnb users in NYC prefer renting entire homes rather than shared or private rooms.

---

### **3. Top 10 Hosts with the Most Listings**
**Insight:**
- Some hosts manage hundreds of listings, suggesting **large property management businesses** operate on Airbnb.
- The top host has **over 300 listings**.

**Conclusion:**
Many NYC Airbnb listings are controlled by commercial operators rather than individual hosts.

---

### **4. Average Price by Neighborhood**
**Insight:**
- The most expensive neighborhoods are **Fort Wadsworth, Woodrow, Sea Gate, and Riverside**.
- These neighborhoods have average prices of **$800 per night**.

**Conclusion:**
Luxury Airbnb listings are concentrated in certain high-end neighborhoods.

---

### **5. Price Distribution of Listings**
**Insight:**
- The majority of Airbnb listings are priced **below $200 per night**.
- Only a few **luxury listings** exceed **$1,000 per night**.

**Conclusion:**
Most NYC Airbnb listings cater to budget-conscious travelers.

---

### **6. Geographical Distribution of Listings**
**Insight:**
- **Manhattan and Brooklyn** have the densest Airbnb activity, especially near tourist hotspots.
- Listings decrease towards **Queens, Staten Island, and The Bronx**.

**Conclusion:**
Airbnb activity in NYC is heavily concentrated in central areas.

---

### **7. Reviews Per Month Over Time**
**Insight:**
- Airbnb reviews increased steadily over the years.
- A sharp decline is visible in **2020**, likely due to **COVID-19** travel restrictions.

**Conclusion:**
The NYC Airbnb market experienced a **downturn during the pandemic** but is likely recovering.

---

## **Dashboard**

![Image](https://github.com/user-attachments/assets/30aa589d-b30f-42b4-a102-e93a276be379)

---

## **Technologies Used**
- **Python (pandas)** → Data Cleaning & Processing
- **Power BI** → Data Visualization

---

## **How to Reproduce This Analysis**
To reproduce this analysis:
1. **Download the dataset**: `AB_NYC_2019.csv`
2. **Run the Python cleaned script** (`AirBnB_clean`).
3. **Import the cleaned dataset into Power BI and recreate the visualizations.**

---



---

## **Conclusion**
This project provides an in-depth analysis of Airbnb listings in New York City. The key takeaways include:
1. **Brooklyn and Manhattan dominate the market.**
2. **Entire home/apartment rentals are the most common.**
3. **Some hosts manage hundreds of properties, indicating commercial involvement.**
4. **Luxury listings are concentrated in high-end neighborhoods.**
5. **The Airbnb market suffered a downturn in 2020 due to COVID-19.**

---




