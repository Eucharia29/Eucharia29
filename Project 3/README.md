# **Exploratory Data Analysis of Retail Sales Data**  
## **Project Overview**  
This project undertakes a comprehensive exploratory data analysis (EDA) of retail sales data, with a particular focus on time series analysis. The primary objective is to uncover meaningful patterns, trends, and actionable insights that can empower the retail business to make data-driven decisions.  
The analysis encompasses several key stages:  
- Data loading and cleaning  
- Descriptive statistics  
- Time series analysis (including trend analysis, decomposition, and forecasting)  
- Customer and product analysis  
- Effective visualization  
This project leverages time series techniques to understand sales patterns over time, identify seasonality, and forecast future sales.  
## **Dataset**  
**Dataset Name:** `Customer_shopping_data.csv`  
**Rows & Columns:** 99,457 rows × 10 columns   
**Key Features:**  
- `invoice_date` – Date of transaction  
- `customer_id` – Unique identifier for customers  
- `category` – Product category  
- `price` – Price per item  
- `quantity` – Quantity of items purchased  
- `payment_method` – Payment mode used
  
**Source:** [Link](https://www.kaggle.com/datasets/mehmettahiraslan/customer-shopping-dataset)  
---
## **1. Data Loading and Cleaning**  
### **1.1 Loading the Data**  
The dataset was loaded into a Pandas DataFrame using:  
```python
import pandas as pd  
df = pd.read_csv(r"C:\Users\BR- PROCUREMENT\Downloads\customer_shopping_data.csv\customer_shopping_data.csv")  
```
### **1.2 Data Inspection**  
Initial inspection using:  
```python
df.info()  # Check structure and data types  
df.dtypes  # Confirm data types  
```
### **1.3 Data Cleaning**  
**Missing Values:** Checked using `df.isnull().sum()`, none found.  
**Duplicate Rows:** Checked using `df.duplicated().sum()`, none found.  
**Date Conversion:** Converted `invoice_date` column which was an object to datetime format:  
```python
df["invoice_date"] = pd.to_datetime(df["invoice_date"], dayfirst=True, errors="coerce")
``` 
`errors="coerce"` argument was used to handle any invalid date entries by converting them to `NaT`.

---
## **2. Descriptive Statistics**  
### **2.1 Numerical Features**  
Statistical summary of numerical variables:  
```python
df.describe()
```
### **2.2 Categorical Features**  
```python
df.describe(include="object")
```
Provides insights into category distributions, such as the most common product categories and payment methods.  

---
## **3. Time Series Analysis**  
### **3.1 Sales Trend Analysis**  
**Feature Engineering:** Extracted `year_month` for monthly aggregation:  
```python
df["year_month"] = df["invoice_date"].dt.to_period("M")
```
**Monthly Sales Calculation:**  
```python
sales_trend = df.groupby(df['year_month'])['price'].sum().to_timestamp()
```
**Sales Trend Visualization:**  a line plot was generated to visualize the sales trend over time using:
```python
import matplotlib.pyplot as plt  
plt.figure(figsize=(12,6))  
plt.plot(monthly_sales["year_month"], monthly_sales["price"], marker="o", linestyle="-")  
plt.xlabel("Year-Month")  
plt.ylabel("Total Sales")  
plt.title("Monthly Sales Trend")  
plt.grid(True)  
plt.show()
```
<img src="https://github.com/user-attachments/assets/891af31b-5bdd-43eb-8fcc-8f76521f7a06" width="500">

The sales trend analysis revealed a concerning sharp decline in sales towards the end of the observed period (late 2022 and early 2023). This decline is a critical issue that requires immediate attention from the retail business.

**Recommendation:**  
- Analyze external factors that may have contributed to the decline, such as economic downturns, competitor activities, or seasonal variations.  
- Examine internal factors such as changes in marketing strategy, product availability, pricing, or customer service.  
- Verify the accuracy of sales data for the affected period to rule out any errors or anomalies.  
---
### **3.2 Time Series Decomposition**  
To better understand the components of the sales trend, the time series data was decomposed into trend, seasonal, and residual components.  
```python
from statsmodels.tsa.seasonal import seasonal_decompose  
decomposition = seasonal_decompose(sales_trend, model='additive', period=12)
  
plt.figure(figure=(10,80))
decomposition.plot()
plt.show()
```
![Image](https://github.com/user-attachments/assets/d16d9656-abd2-4069-9e7e-a80273555a5a)

The decomposition suggests that the sharp decline in sales is primarily due to irregular factors rather than seasonality or long-term trends.  

**Recommendation:**  

Focus on identifying specific events or disruptions that may have caused the sudden drop in sales. 

---
### **3.3 Sales Forecasting**  
**Autocorrelation and Partial Autocorrelation Analysis:**  
Autocorrelation (ACF) and Partial Autocorrelation (PACF) plots were generated to identify potential parameters for forecasting.  
```python
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
fig, axes = plt.subplots(1,2, figsize=(14,4))

plot_acf(sales_trend, lags=12, ax=axes[0])
axes[0].set_title("ACF (Autocorrelatio)")

plot_pacf(sales_trend, lags=12, ax=axes[1])
axes[1].set_title("PACF (Partial Autocorrelatio)")
plt.tight_layout()
plt.show()
```
![Image](https://github.com/user-attachments/assets/0207d2b7-a3a9-4069-8215-1ef00287ea2a)


### **ACF (Autocorrelation Function) Plot**
- Measures the correlation between a time series and its past values (lags).
- If significant spikes are present, it suggests strong autocorrelation.
- In this plot, the values seem to be close to zero, indicating weak autocorrelation.

### **PACF (Partial Autocorrelation Function) Plot**
- Measures the correlation between a time series and its past values while controlling for intermediate lags.
- Helps in identifying the appropriate lag order for models like ARIMA.
- This plot also shows weak correlations, suggesting little direct influence from past values.

And from this visuals, ARIMA model is not the best approch for forecasting this data.

**Model Fitting:**  
A Simple Exponential Smoothing model was applied for forecasting.  
```python
from statsmodels.tsa.holtwinters import SimpleExpSmoothing  
exp_model = SimpleExpSmoothing(sales_trend).fit(smoothing_level=0.2, optimized=False)
exp_forecast = exp_model.forecast(6) #forcasting for 6 months
```
**Forecast Visualization:**  
```python
plt.figure(figsize=(8,4))
plt.plot(sales_trend, label='Actual Sales', marker='x')
plt.plot(holt_forecast, label='Exponential Smoothing Forecast', linestyle='dashed', marker='o',color='orange')
plt.title('Sales Forecast Using Exponential Smoothing')
plt.xlabel('Year-Month')
plt.ylabel('Total Sales')
plt.xticks(rotation=45)
plt.legend()
plt.grid()
plt.show()
```
![Image](https://github.com/user-attachments/assets/8a728d79-1ded-43bc-8604-261c9a5aca79)

1. **Actual Sales (Blue Line with X markers)**
- Represents the historical sales data over time.
- Sales remain relatively stable for most of the period but drop sharply at a certain point.
2. **Exponential Smoothing Forecast (Orange Dots)**
- The model predicts future sales using Exponential Smoothing, which assigns more weight to recent observations.
- The forecast shows a steep downward trend, indicating a projected decline in sales.

 **Recommendations**
- Investigate the cause of the sales decline
- If the decline is seasonal, introduse discounts, promotions or target marketing during low periods
- Implement loyalty programs or personalized promotions to maintain engagement
- Analyze top customers segments and their purchase behaviours to tailor offerings.

---
## **4. Customer and Product Analysis**  
### **4.1 Customer Age Distribution**  
A histogram with Kernel Density Estimate (KDE) was used to visualize customer age distribution.  The histogram of customer ages suggests a relatively uniform distribution, indicating a broad customer base across different age groups.
```python
import seaborn as sns  
plt.figure(figsize=(10,5))  
sns.histplot(df["age"], bins=20, kde=True)  
plt.xlabel("Age")  
plt.ylabel("Frequency")  
plt.title("Customer Age Distribution")  
plt.show()
```
![Image](https://github.com/user-attachments/assets/4ed2659d-0cda-44e3-b0b8-7a8e28988269)
**Recommendation:** 

The retail business can leverage this information to tailor marketing campaigns and product offerings to specific age segments within their customer base.
### **4.2 Top Customers by Spending**  
```python
top_customers = df.groupby("customer_id")["price"].sum().sort_values(ascending=False).head(10)
```
The analysis revealed that the top 10 customers had identical total spending, all top 10 customers exhibit identical total spending (5250.0). This pattern is highly unusual and raises concerns about data integrity. It is unlikely to represent real customer behavior.
 
**Recommendation:**  
- Investigate data entry or aggregation errors.  
- Check if business rules, such as fixed-value gift cards, explain the pattern.  
- Conduct a system audit for potential software bugs.  
---
### **4.3 Top Selling Product Categories**  
```python
top_categories = df.groupby("category")["quantity"].sum().sort_values(ascending=False).head(10)

import seaborn as sns
plt.figure(figsize=(8,4))
sns.countplot(data=df, x='category',hue='category',order=df['category'].value_counts().index, palette='viridis',legend=False)
plt.title('Product Category Distribution')
plt.xticks(rotation=45)
plt.show()
```
![Image](https://github.com/user-attachments/assets/4d53033c-d7a8-454c-a8f4-eb0bf937fc23)
The "Clothing" category emerged as the best-selling category, followed by "Cosmetics" and "Food & Beverage."

**Recommendation:**  
- Optimize inventory to meet demand.  
- Expand product lines within high-performing categories.  
- Develop targeted marketing campaigns.  
- Implement cross-selling strategies.  
---
## **5. Payment Method Distribution**  
A pie chart was created to analyze payment method distribution.  
```python
df["payment_method"].value_counts().plot.pie(autopct="%1.1f%%", figsize=(8,8))  
plt.title("Distribution of Payment Methods")  
plt.ylabel("")  
plt.show()
```
![Image](https://github.com/user-attachments/assets/ae00b521-9e78-4500-9fe8-babd9f88cfff)
Cash was the most commonly used payment method, followed by credit and debit cards.  

**Recommendation:**  
- Ensure efficient cash handling processes.  
- Encourage electronic payments through incentives.  
- Analyze customer preferences for different payment methods.  
---
##  **Recommendations**  
1. Investigate the identical spending amounts for top customers.  
2. Analyze internal and external factors contributing to the recent sales decline.  
3. Capitalize on the strong performance of the "Clothing" category.  
4. Optimize cash handling processes and promote electronic payments.  
5. Conduct deeper analysis to understand relationships between customer demographics, product categories, and payment methods.  
---
## **Conclusion**  
This analysis provided valuable insights into retail sales data, highlighting key trends, customer behaviors, and product performance. Further investigation is recommended to resolve data anomalies and optimize business strategies.  

---
## **Code and Libraries Used**  
- Pandas  
- NumPy  
- Matplotlib  
- Seaborn  
- Statsmodels  


