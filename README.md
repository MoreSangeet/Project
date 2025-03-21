# Diwali Sales Data Analysis

Welcome to the **Diwali Sales Data Analysis** project! This Python project focuses on analyzing sales data from Diwali, extracting valuable insights regarding customer demographics, purchasing patterns, and regional sales performance.

---

## 📚 **Libraries Used**

We’ve used the following Python libraries for data manipulation, visualization, and analysis:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt  # For data visualization
import seaborn as sns           # For advanced data visualization
%matplotlib inline
```

## 📥 **Data Import and Preparation**
We start by importing the Diwali sales data from a CSV file and then perform various preprocessing tasks:

```python
# Import CSV file
df = pd.read_csv(r"C:\Users\sangit\Downloads\Python_Diwali_Sales_Analysis\Diwali Sales Data.csv", encoding='unicode_escape')
```

##  **View dataset dimensions and first few records**
```python
df.shape  # Output: (11251, 15)
df.head()  # Preview the first 5 rows of the dataset
```
The dataset contains 15 columns and 11,251 rows with details like user ID, product information, gender, age group, marital status, and purchase details.

## 🧹 **Data Cleaning and Transformation**
We clean the data by:

* Dropping irrelevant or empty columns
* Handling missing values
* Converting data types for consistency
```python
# Drop irrelevant/blank columns
df.drop(['Status', 'unnamed1'], axis=1, inplace=True)

# Check for missing values
df.isnull().sum()

# Drop rows with null values
df.dropna(inplace=True)

# Convert 'Amount' to integer type
df['Amount'] = df['Amount'].astype('int')
```
## 🔎 **Data Exploration**
**1. General Statistics**  

We use the describe() method to understand key statistics like mean, standard deviation, and range for numerical columns:

```python
df.describe()
```
* The average age of customers is approximately 35 years.
* The average purchase amount is ₹9453.

**2. Data Visualizations**  

Gender Distribution  

We plot a countplot to visualize the gender distribution of customers:

```python
sns.countplot(x='Gender', data=df)
```
**Insights:**

* Most customers are female.  

* Females also have a higher purchasing power compared to males.  

**Age Group vs Purchase Amount**  

We explore the relationship between age group and total purchase amounts using a barplot:

```python
Copy
sns.barplot(x='Age Group', y='Amount', data=df.groupby(['Age Group'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False))
```
**Insights:**

* The 26-35 years age group is the most active in making purchases, particularly females.  

**Top States by Sales**  

We visualize the total sales by state to understand regional performance:

```python
Copy
sns.barplot(x='State', y='Amount', data=df.groupby(['State'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10))
```
**Insights:**

* Uttar Pradesh, Maharashtra, and Karnataka have the highest sales.  

**Marital Status and Purchases**  

We compare purchase amounts based on marital status and gender:

```python
Copy
sns.barplot(data=df.groupby(['Marital_Status', 'Gender'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False), x='Marital_Status', y='Amount', hue='Gender')
```
**Insights:**

* Married women tend to spend more, especially on specific product categories.  

**Occupation vs Sales**  

We analyze which occupations contribute most to sales:

```python
Copy
sns.barplot(data=df.groupby(['Occupation'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False), x='Occupation', y='Amount')
```
**Insights:**

* Occupations in IT, Healthcare, and Aviation lead in purchases.  

**Product Category Breakdown**  

We visualize the top-selling product categories:

```python
Copy
sns.barplot(data=df.groupby(['Product_Category'], as_index=False)['Amount'].sum().sort_values(by='Amount', ascending=False).head(10), x='Product_Category', y='Amount')
```
**Insights:**

* Food, Clothing, and Electronics are the most popular categories.  

## 🎯 **Key Insights & Conclusion**
**Project Learnings**  

* Data Cleaning and Manipulation: We used various techniques to clean and prepare the data for analysis, ensuring consistency across all columns.
* Exploratory Data Analysis (EDA): Leveraged libraries like pandas, matplotlib, and seaborn to gain deeper insights into the dataset through visualization and statistical analysis.
* Improved Customer Understanding: By analyzing different customer demographics (state, occupation, gender, and age), we identified segments of potential customers that could be targeted for more personalized marketing.
* Sales Insights: We identified the most popular products and categories, which can help in better inventory planning and sales forecasting.

## **Conclusion**
From the analysis, we concluded that:

* Married women in the age group 26-35 years from states like Uttar Pradesh, Maharashtra, and Karnataka working in sectors like IT, Healthcare, and Aviation are more likely to purchase products, particularly from Food, Clothing, and Electronics categories.

This analysis can help businesses optimize inventory, target the right customer segments, and improve marketing strategies to boost sales.
