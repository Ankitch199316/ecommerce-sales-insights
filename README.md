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

## 📁 Dataset Source

This project uses real-world data from **Olist**, one of Brazil’s largest online marketplaces.

- 📦 **Source**: [Brazilian E-Commerce Public Dataset by Olist on Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- 📅 Data spans from **2016 to 2018**
- Includes customer orders, payments, product categories, sellers, reviews, and geolocation

All data used was publicly available under a permissive license and cleaned for the purposes of this project.

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

## 📈 Business Insights & Recommended Actions

| 🔍 Insight | 💡 Business Action |
|-----------|--------------------|
| **76% of customers used credit cards for payment** | Focus marketing promotions and loyalty programs around credit card users. Consider partnerships with credit card companies to offer cashback or EMI plans. |
| **Credit card users used an average of 3.6 installments** | Enable or highlight installment options more clearly during checkout to increase average order value. Bundle high-value items with flexible EMI plans. |
| **SP (São Paulo) and RJ (Rio) generate the most revenue and have the most sellers** | Prioritize logistics, seller acquisition, and fulfillment capabilities in these high-performing regions. Launch region-specific seller training or incentives. |
| **Office furniture and related categories had the longest delivery times (~20 days)** | Reevaluate the shipping and fulfillment process for bulky or slow-moving categories. Consider local warehousing or alternate 3PL partners. |
| **Revenue spikes observed in May & August, then dips** | Investigate historical campaigns or shopping events during those peak months. Strategically plan promotions or influencer pushes to replicate success. |
| **Seller revenue is highly concentrated among a few top sellers** | Introduce performance-driven programs or early-access tools to help mid-tier sellers scale up. Encourage more balanced seller contribution to reduce risk. |
| **Low adoption of debit cards, vouchers, and boleto** | Create awareness campaigns or discounts specific to underused payment methods. This diversifies transaction risk and enhances inclusivity. |
| **Very low cancellation rate (~0%)** | Excellent operational performance — highlight this in marketing as a trust-builder (“99%+ delivery rate”). Keep investing in fulfillment ops. |


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
📁 e-commerce-analysis/
├── 📒 Project1.ipynb                     # Python exploration and analysis
├── 📁 Clean_CSVs.zip                     # Zipped cleaned datasets
├── 📊 Dashboard1_SalesOverview.twbx     # Tableau dashboard 1
├── 📊 Dashboard2_PaymentSellerInsights.twbx # Tableau dashboard 2
├── 📝 README.md                         # Project overview + insights

```

---

---

## ⚙️ Dependencies

To ensure full reproducibility of this analysis, the following versions were used:

- Python 3.8+
- pandas 1.3.0
- numpy 1.21.0
- matplotlib 3.4.0
- seaborn 0.11.1
- Jupyter Notebook
- Tableau Public (2021.4+)

📦 You can install the core Python libraries using:

```bash
pip install pandas==1.3.0 numpy==1.21.0 matplotlib==3.4.0 seaborn==0.11.1

---

## 🚀 What’s Next?

This project can be extended with:
- NLP analysis on Portuguese product reviews
- Customer segmentation using clustering
- Delivery delay prediction using regression modeling
