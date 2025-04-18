# 📦 Brazilian E-Commerce: Sales & Delivery Analytics Project

### 📁 Project Overview

This project dives deep into transactional data from a leading Brazilian e-commerce marketplace. With over **100,000 orders**, it analyzes key aspects of customer orders, product categories, delivery logistics, payment methods, and seller performance.

The objective was not just to manipulate data, but to extract actionable business insights that reflect the real-world challenges and operations of online retail at scale.

---

## 🧠 Motivation & Story

As a new budding data analyst, I wanted to challenge myself with a real-world, messy, multi-table dataset—something that would push me to integrate SQL-style joins, perform data cleaning, build a robust ETL pipeline in Python, and ultimately drive impactful storytelling via Tableau dashboards.

This project helped me simulate the kind of end-to-end problem-solving expected in modern analytics roles:
- Data ingestion & cleaning
- Exploratory & advanced analysis
- Data enrichment across multiple datasets
- KPI extraction
- Interactive visualization

---

## 📊 Business Goals

- Identify **high-performing product categories** and delivery challenges
- Uncover **revenue trends** over time and geography
- Evaluate **seller distribution & concentration**
- Compare **payment method performance** and customer preferences
- Provide insights for strategic decision-making in logistics, marketing, and sales

---

## 🗃️ Datasets Used

- `olist_orders_dataset.csv`
- `olist_order_items_dataset.csv`
- `olist_products_dataset.csv`
- `olist_order_payments_dataset.csv`
- `olist_sellers_dataset.csv`

---

## 🧪 Steps Performed

### 1. **Data Acquisition & Exploration**
- Loaded multiple CSV files
- Explored schema and checked for nulls and duplicates
- Conducted `info()` and `head()` evaluations

### 2. **Data Cleaning & Preprocessing**
- Merged datasets (`order_items + products → orders`)
- Added delivery days calculation
- Standardized column names
- Filtered out incomplete or missing records
- Translated category names for better readability

### 3. **Enrichment & KPI Calculation**
- Calculated total revenue per order
- Added payment type insights: `% of orders`, `revenue`, `installments`
- Extracted revenue over time by month and payment method
- Generated seller KPIs:
  - Top 10 Sellers by Revenue
  - Seller Count by State
  - Revenue by State
  - Revenue Distribution Histogram

### 4. **Exported Processed Datasets**
- Clean datasets were exported as `.csv` and fed into Tableau for visualization.

---

## 📈 Tableau Dashboards

### 📌 **Dashboard 1: Sales Overview**
- Total Revenue, Total Orders, Avg Delivery Time KPIs
- Avg Delivery Time by Product Category
- Revenue by Category
- Order Status Distribution
- Revenue Trend Over Time

<img width="1201" alt="Screenshot 2025-04-18 at 11 57 49 AM" src="https://github.com/user-attachments/assets/e209dc43-a0b1-4e99-b682-a442ce729b55" />

link : https://public.tableau.com/views/SalesOverviewDashboardBrazilianE-Commerce/SellerandPaymentDashboard?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link

### 📌 **Dashboard 2: Payment & Seller Insights**
- KPIs: Top Seller Revenue, Most Used Payment Type, Avg Installments
- Revenue by Payment Type Over Time
- Top Sellers by Revenue
- Seller Count by State
- State-wise Revenue Performance

<img width="1171" alt="Screenshot 2025-04-18 at 4 14 56 PM" src="https://github.com/user-attachments/assets/dcff4ea2-4f91-466a-98f9-8c76e50e26b0" />

link : https://public.tableau.com/views/SellerPaymentDashboardBrazilianE-Commerce/SellerandPaymentDashboard?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link

---

## 💡 Key Insights & Takeaways

1. **Credit Cards dominate** both in order count and revenue share (~76%).
2. Delivery time varies significantly across product categories—**office furniture** has the longest delays.
3. **Revenue spikes in May & August**, possibly due to seasonal demand or promotional campaigns.
4. A small set of sellers contribute disproportionately to revenue—**heavy concentration at the top**.
5. **SP and RJ are powerhouse states**—leading in both seller density and revenue.

---

## 📚 Tools & Technologies

- **Python (Pandas, NumPy, Matplotlib)**
- **SQL-style joins & logic via Pandas**
- **Tableau Public** (interactive dashboards)
- **Jupyter Notebook** (for reproducibility and presentation)

---

## 🧩 Key Code Snippets

### 📥 1. Importing Data and Setting Up SQLite

```python
import pandas as pd
import sqlite3

conn = sqlite3.connect('ecommerce.db')
cursor = conn.cursor()

orders = pd.read_csv('olist_orders_dataset.csv')
order_items = pd.read_csv('olist_order_items_dataset.csv')
products = pd.read_csv('olist_products_dataset.csv')
```

---

### 🔗 2. Merging Order Items with Product Data

```python
items_with_products = pd.merge(order_items, products, on='product_id')
sales_data = pd.merge(items_with_products, orders, on='order_id')
```

---

### 🧮 3. Feature Engineering: Order Value and Delivery Time

```python
sales_data['total_order_value'] = sales_data['price'] + sales_data['freight_value']
sales_data['delivery_time_days'] = (sales_data['order_delivered_customer_date'] -
                                    sales_data['order_purchase_timestamp']).dt.days
```

---

### 💳 4. Aggregating Payment Details

```python
payments_agg = payments.groupby('order_id').agg({
    'payment_type': lambda x: x.mode()[0],
    'payment_installments': 'mean',
    'payment_value': 'sum'
}).reset_index()

sales_data = sales_data.merge(payments_agg, on='order_id', how='left')
```

---

### 📈 5. Monthly Revenue by Payment Type

```python
sales_data['order_month'] = sales_data['order_purchase_timestamp'].dt.to_period('M')

monthly_revenue_by_payment = (
    sales_data.groupby(['order_month', 'primary_payment_type'])['total_order_value']
    .sum().reset_index()
)
```

---

## 📁 Folder Structure

```plaintext
📦 e-commerce-analysis/
├── Project1.ipynb               # Python exploration and data prep
├── Cleaned CSVs/
│   ├── sales_data.csv
│   ├── seller_revenue_by_state.csv
│   ├── revenue_by_payment_type.csv
├── Dashboards/
│   ├── Dashboard1_SalesOverview.twbx
│   ├── Dashboard2_Payment_Sellers.twbx
└── README.md                    # You are here!
```

---

## 🚀 What’s Next?

This project can be extended with:
- NLP analysis on Portuguese product reviews
- Customer segmentation using clustering
- Delivery delay prediction using regression modeling
