# acc102
# Project:
# Sales and Profit Analysis for an E-commerce Business
#
# Objective:
# To help an e-commerce operations manager understand sales performance,
# profitability, discount effects, and regional differences.
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
df = pd.read_csv("data/superstore.csv")
df.head()
df.info()
df.isnull().sum()
df.describe()
df['Order Date'] = pd.to_datetime(df['Order Date'])
df['Month'] = df['Order Date'].dt.to_period('M').astype(str)
df.drop_duplicates(inplace=True)
category_sales = df.groupby('Category')['Sales'].sum().sort_values(ascending=False)
category_sales.plot(kind='bar', color='skyblue')
plt.title('Total Sales by Category')
plt.ylabel('Sales')
plt.show()
category_profit = df.groupby('Category')['Profit'].sum().sort_values(ascending=False)
category_profit.plot(kind='bar', color='lightgreen')
plt.title('Total Profit by Category')
plt.ylabel('Profit')
plt.show()
region_perf = df.groupby('Region')[['Sales', 'Profit']].sum().sort_values(by='Sales', ascending=False)
region_perf.plot(kind='bar', figsize=(8,5))
plt.title('Sales and Profit by Region')
plt.show()
monthly = df.groupby('Month')[['Sales', 'Profit']].sum()
monthly.plot(figsize=(10,5))
plt.title('Monthly Sales and Profit Trend')
plt.show()
sns.scatterplot(data=df, x='Discount', y='Profit', alpha=0.5)
plt.title('Discount vs Profit')
plt.show()
top_products = df.groupby('Product Name')['Sales'].sum().sort_values(ascending=False).head(10)
top_products.plot(kind='barh', color='orange')
plt.title('Top 10 Products by Sales')
plt.show()
