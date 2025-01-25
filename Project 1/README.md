
---

# **Customer Segmentation Analysis**

## **Overview**
This analysis explores customer segmentation using clustering techniques to group customers based on their behaviors, preferences, and demographics. By dividing the customer base into distinct groups, I aim to identify key characteristics, spending patterns, and actionable strategies to improve customer engagement and maximize business revenue.

---

## **Data Source:**
[LINK](https://www.kaggle.com/code/analystoleksandra/marketing-analytics-customer-segmentation)
 
 

## **Steps Taken**

### **1. Data Preparation**
- The dataset included key variables such as:
  - **Marital Status** (0: Divorced, 1: Married, 2: Single, 3: Together, 4: Widowed)
  - **Education Levels** (0: 2n Cycle, 1: Basic, 2: Graduates, 3: Masters, 4: PhD)
  - **Income**
  - **Recency** (Days since the last purchase)
  - **Total Spending**
  - **Total Purchases**
  - Spending on various product categories (e.g., wine, meat, gold, sweets, etc.)
- Standardization was applied to numerical columns to ensure fair clustering.

### **2. Clustering Technique**
- **K-Means clustering** was used to divide customers into **three clusters**:
  - **Cluster 0**: High-performing customers
  - **Cluster 1**: Moderate-performing customers
  - **Cluster 2**: Low-performing customers
- Clusters were analyzed to understand spending patterns, marital status, education levels, and income distribution.
![Image](https://github.com/user-attachments/assets/cd9a89d6-5264-4f92-9d89-91dcaf6f2854)

![Image](https://github.com/user-attachments/assets/69e389ac-28aa-4341-8ee4-8501a9d72296)

### **3. Visualization and Interpretation**
- Bar charts and stacked bar plots were used to visualize the distribution of spending, marital status, and education levels across clusters.
- Spending patterns across product categories were analyzed to identify cluster-specific behaviors and preferences.

---

## **Cluster Characteristics**

### **Cluster 0: High Performers**
- **Key Traits:**
  - Highest income, highest spending across all product categories, and frequent purchases.
  - Low recency, indicating recent engagement and strong brand loyalty.
  - Dominated by **married graduates**, with a significant representation of **PhD holders**.
- **Behavior:**
  - Spend the most on premium categories like wine, meat, and gold.
  - Broad purchasing preferences, consistently spending across all categories.
- **Actionable Recommendations:**
  - Retain these high-value customers through exclusive loyalty programs and personalized promotions.
  - Offer premium bundles and high-value packages to maximize their engagement and spending.

### **Cluster 1: Moderate Performers**
- **Key Traits:**
  - Moderate income, moderate spending, and mid-tier purchase activity.
  - Mostly **married graduates** with minimal representation of PhD holders.
- **Behavior:**
  - Spend less on premium categories like wine and gold but contribute moderately across other categories.
- **Actionable Recommendations:**
  - Upsell and cross-sell mid-tier products to increase their spending.
  - Focus on value-based promotions and bundles to appeal to their moderate income levels.
  - Engage this cluster with targeted campaigns highlighting affordability and quality.

### **Cluster 2: Low Performers**
- **Key Traits:**
  - High income but low spending, less frequent purchases, and higher recency (customers are disengaged).
  - Dominated by **PhD holders**, with no representation of customers with basic education.
- **Behavior:**
  - Spend the least across all product categories, with minimal engagement in fruits, fish, and sweets.
  - May prioritize other brands or have preferences misaligned with the current offerings.
- **Actionable Recommendations:**
  - Re-engage this group through targeted marketing strategies:
    - Personalized recommendations for premium or niche products.
    - Exclusive first-time purchase discounts or offers.
    - Address convenience issues, such as delivery options or ease of purchase.

![Image](https://github.com/user-attachments/assets/368b71e0-c16f-4ab1-9145-9e7e5d273a19)
---

## **Key Insights**

### **1. Income vs. Spending**
- Higher income does not guarantee higher spending.  
  - Cluster 2, despite having higher income than Cluster 1, underperforms in spending, total purchases, and recency.
  - This suggests that customer engagement and product alignment are critical to converting high-income customers into high spenders.

  ![Image](https://github.com/user-attachments/assets/2da4ac3d-8a3f-4aba-b4e4-b68fbdb63852)

### **2. Product Spending by Cluster**
- **Wine**:
  - Cluster 0 dominates spending (600), indicating a preference for premium products.
- **Meat**:
  - Cluster 0 leads (350), showing engagement with high-quality food items.
- **Fruits, Fish, and Sweets**:
  - Cluster 0 spends the most, followed by Cluster 1, with Cluster 2 contributing minimally.
- **Gold**:
  - Cluster 0 again dominates (80), highlighting their interest in luxury products.

  ![Image](https://github.com/user-attachments/assets/7a63c587-a9f3-4e28-9d7b-a4f19401cca7)

### **3. Marital Status**
- Married customers dominate all clusters, especially Cluster 0.
- Divorced customers consistently have the lowest representation.

### **4. Educational Level**
- Graduates dominate in Clusters 0 and 1, while Cluster 2 is dominated by PhD holders.
- Basic and 2n Cycle education levels are absent in Cluster 0 and Cluster 2, indicating a correlation between higher education and spending.

![Image](https://github.com/user-attachments/assets/4a2d73c0-c905-4541-a6e2-e8dae9980b9c)

---

## **Conclusion**
This analysis reveals that income alone is not enough to predict customer value. Other behavioral metrics such as recency, total purchases, and spending patterns play a more significant role in customer segmentation.  

- **Cluster 0** represents high-value, loyal customers who require retention strategies to maintain their engagement and maximize lifetime value.  
- **Cluster 1** consists of moderate-value customers who can be nurtured to increase their spending and purchasing frequency.  
- **Cluster 2** includes disengaged, high-income customers who may need personalized marketing and product alignment to boost their contribution.  

By leveraging these insights, businesses can develop targeted marketing strategies tailored to each cluster, ensuring resource optimization and improved customer satisfaction.

---

