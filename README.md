## 📦 Brazilian E-Commerce: Sales & Delivery Analytics Project

### 📁 Project Overview
This project dives deep into transactional data from a leading Brazilian e-commerce marketplace. With over 100,000 orders, it analyzes key aspects of customer orders, product categories, delivery logistics, payment methods, and seller performance.

The objective was not just to manipulate data, but to extract actionable business insights that reflect the real-world challenges and operations of online retail at scale.

### 🧠 Motivation & Story

As a guy who is understanding data analyst, I wanted to challenge myself with a real-world, messy, multi-table dataset—something that would push me to integrate SQL-style joins, perform data cleaning, build a robust ETL pipeline in Python, and ultimately drive impactful storytelling via Tableau dashboards.

#### This project helped me simulate the kind of end-to-end problem-solving expected in modern analytics roles:

1. Data ingestion & cleaning
2. Exploratory & advanced analysis
3. Data enrichment across multiple datasets
4. KPI extraction
5. Interactive visualization

### 📊 Business Goals
* Identify high-performing product categories and delivery challenges
* Uncover revenue trends over time and geography
* Evaluate seller distribution & concentration
* Compare payment method performance and customer preferences
* Provide insights for strategic decision-making in logistics, marketing, and sales

### 🗃️ Datasets Used
* olist_orders_dataset.csv
* olist_order_items_dataset.csv
* olist_products_dataset.csv
* olist_order_payments_dataset.csv
* olist_sellers_dataset.csv


### 🧪 Steps Performed

#### 1. Data Acquisition & Exploration
* Loaded multiple CSV files
* Explored schema and checked for nulls and duplicates
* Conducted info() and head() evaluations

#### 2. Data Cleaning & Preprocessing
* Merged datasets (order_items + products → orders)
* Added delivery days calculation
* Standardized column names
* Filtered out incomplete or missing records
* Translated category names for better readability

#### 3. Enrichment & KPI Calculation
* Calculated total revenue per order
* Added payment type insights: % of orders, revenue, installments
* Extracted revenue over time by month and payment method
* Generated seller KPIs:
* Top 10 Sellers by Revenue
* Seller Count by State
* Revenue by State
* Revenue Distribution Histogram

#### 4. Exported Processed Datasets
* Clean datasets were exported as .csv and fed into Tableau for visualization.


### 📈 Tableau Dashboards

#### 📌 Dashboard 1: Sales Overview

<img width="1204" alt="Screenshot 2025-04-18 at 4 14 00 PM" src="https://github.com/user-attachments/assets/ebe35d14-39aa-4364-a29f-ec14bc91323c" />

Link : https://public.tableau.com/views/SalesOverviewDashboardBrazilianE-Commerce/SellerandPaymentDashboard?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link

* Total Revenue, Total Orders, Avg Delivery Time KPIs
* Avg Delivery Time by Product Category
* Revenue by Category
* Order Status Distribution
* Revenue Trend Over Time

#### 📌 Dashboard 2: Payment & Seller Insights

<img width="1171" alt="Screenshot 2025-04-18 at 4 14 56 PM" src="https://github.com/user-attachments/assets/bda17bfa-ed50-4c99-98a1-c666d61e9d59" />

link : https://public.tableau.com/views/SellerPaymentDashboardBrazilianE-Commerce/SellerandPaymentDashboard?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link

* KPIs: Top Seller Revenue, Most Used Payment Type, Avg Installments
* Revenue by Payment Type Over Time
* Top Sellers by Revenue
* Seller Count by State
* State-wise Revenue Performance

### 💡 Key Insights & Takeaways
1. Credit Cards dominate both in order count and revenue share (~76%).
2. Delivery time varies significantly across product categories—office furniture has the longest delays.
3. Revenue spikes in May & August, possibly due to seasonal demand or promotional campaigns.
4. A small set of sellers contribute disproportionately to revenue—heavy concentration at the top.
5. SP and RJ are powerhouse states—leading in both seller density and revenue.

   
### 📚 Tools & Technologies
* Python (Pandas, NumPy, Matplotlib)
* SQL-style joins & logic via Pandas
* Tableau Public (interactive dashboards)
* Jupyter Notebook (for reproducibility and presentation)

📦 e-commerce-analysis/
├── Project1.ipynb               # Python exploration and data prep
├── Cleaned CSVs/
│   ├── sales_data.csv
│   ├── seller_revenue_by_state.csv
│   ├── revenue_by_payment_type.csv
│   └── ...
├── Dashboards/
│   ├── Dashboard1_SalesOverview.twb
│   └── Dashboard2_Payment_Sellers.twb
└── README.md                    # You are here!


### 🚀 What’s Next?

This project can be extended with:

* NLP analysis on Portuguese product reviews
* Customer segmentation using clustering
* Delivery delay prediction using regression modeling
