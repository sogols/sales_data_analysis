# Sales Data Analysis Project

This project presents an end-to-end workflow for analyzing sales data using SQL and Python, including database design, preprocessing, exploratory data analysis, and advanced analytical insights.

---

## 🗂 Project Structure

| Notebook Filename | Description |
|-------------------|-------------|
| `Sales-DB&Preprocessing.ipynb` | Creating and populating the SQLite database with realistic sales data |
| `Sales-BasicAnalysis.ipynb`    | SQL-based exploratory analysis using aggregation, grouping, filtering, etc. |
| `Sales-AdvancedAnalysis.ipynb` | Advanced analysis and visualizations using pandas and matplotlib |

---

## 1️⃣ Database Schema

In `Sales-DB&Preprocessing.ipynb`, we created a relational SQLite database from scratch.

### Tables

- `customers`  
  - `customer_id` (Primary Key)  
  - `name`
  - `age`
  - `location`

- `products`  
  - `product_id` (Primary Key)  
  - `product_name`  
  - `category`  
  - `price`

- `orders`  
  - `order_id` (Primary Key)  
  - `customer_id` (Foreign Key)  
  - `order_date`

- `order_details`  
  - `order_id` (Foreign Key)  
  - `product_id` (Foreign Key)  
  - `quantity`

### Example Entry (customers)

| customer_id | name         | age | location   |
|-------------|--------------|-----|------------|
| 1           | John Smith   |  28 | New York   |
| 2           | Emma Johnson |  34 |Los Angeles |


---

## 2️⃣ SQL-Based Analysis

Notebook: `Sales-BasicAnalysis.ipynb`

We performed the following types of queries using raw SQL on the created database:

### 🔹 Sample Queries



## What are the most sold products?

```sql
SELECT p.name AS product_name,
       SUM(od.quantity) AS total_sold
FROM products p
JOIN order_details od ON p.product_id = od.product_id
GROUP BY p.name
ORDER BY total_sold DESC;
```

<img src="images/most_sold_products.png" alt="most_sold_products" width="200"/>
---
## What are the top customers by total spending?

```sql
SELECT c.name AS customer_name,
       SUM(od.quantity * od.unit_price) AS total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
JOIN order_details od ON o.order_id = od.order_id
GROUP BY c.name
ORDER BY total_spent DESC;
```

<img src="images/total_spent.png" alt="total_spent" width="250"/>

---

## 3️⃣ Advanced Analysis & Visualizations

Notebook: `Sales-AdvancedAnalysis.ipynb`

We used **pandas** for further data wrangling and **matplotlib**/**seaborn** for visualizations.

### 📌 Sample Analysis

- **Monthly sales trend**
- **Top selling product categories**
- **Correlation between quantity and revenue**
- **Most active customers**
- **Seasonal fluctuations in order volume**
- **Clustering Customers Based on Purchase Behavior**
- **Basket Recommendation and Association Rule Interpretations using Apriori Algorithm**

### 📈 Example Plot: Sales over time (monthly)
---

```python

full_data['order_date'] = pd.to_datetime(full_data['order_date'])
sales_over_time = full_data.groupby(full_data['order_date'].dt.to_period('M'))['total_price'].sum()
sales_over_time.index = sales_over_time.index.to_timestamp()

plt.figure(figsize=(12, 5))
sales_over_time.plot(marker='o', linestyle='-')
plt.title('Sales Trend Over Time')
plt.xlabel('Date')
plt.ylabel('Total Sales')
plt.grid(True)
plt.tight_layout()
plt.show()
```

<img src="images/sales_over_time.png" alt="sales_over_time" width="500"/>
---

### City Sales

```python
city_sales = full_data.groupby('city')['total_price'].sum()

plt.figure(figsize=(8, 8))
plt.pie(city_sales, labels=city_sales.index, autopct='%1.1f%%', startangle=90)
plt.title('Sales Distribution by City')
plt.show()
```

<img src="images/sales_by_city.png" alt="sales_by_city" width="380"/>

---
### Clustering Customers using PCA:


<img src="images/cluster.png" alt="cluster" width="400"/>

Cluster 0: High-Spending Loyalists

Cluster 1: Occasional Shoppers

Cluster 2: Active and Diverse Buyers

Cluster 3: Low Engagement Customers

---
### Basket Recommendation using Apriori Algorithm

#### Key Discovered patterns:
<img src="images/apriori.png" alt="apriori" width="620"/>
---
## 📊 Tableau Dashboard

To complement the SQL and Python analytics, an interactive **Tableau dashboard** was created to better visualize sales KPIs and analysis.

---

### 🔍 What the dashboard shows:

| KPI / Chart                        | Description                             |
|------------------------------------|-----------------------------------------|
| Total Revenue (KPI card)           | Overall revenue generated               |
| Total Orders (KPI card)            | Number of unique orders                 |
| Total Customers (KPI card)         | Number of unique customers              |
| Total Products (KPI card)          | Number of unique Products               |
| Top Customer (KPI card)            | Customer with max total spent           |
| Top Product (KPI card)             | Most sold Product + amount              |
| Sales Over Time (line chart)       | Monthly trend of total sales            |
| Orders Over Time (line chart)      | Monthly trend of orders/quantity sold   |
| Sales by Category (bubbles chart)  | Which product categories sell the most  |
| Top Products (bar chart)           | Best-selling individual products        |
| City Revenue (Treemap)             | Each city total revenue                 |
| Customer Revenue (Bar Chart)       | Each customer total spending            |


---

### 📌 Screenshot
#### **Dashboard**

![Sales Dashboard](images/Dashboard.png)

#### **Best Customers**

![best customers](images/best_customers.png)
---

### 📎 How to open the Tableau workbook

To explore or edit the dashboard interactively:

1. Install **Tableau Public Desktop**
2. Open the file located at:  
   `tableau/Sales Project Workbook.twbx`
3. Connect to your own data source or refresh for updates.

---

## 🧩 Tools & Libraries

- SQLite3
- Python 3.x
- Pandas
- Matplotlib
- Seaborn
- Jupyter Notebook
- Scikit-learn
- ipython-sql
- mlxtend
- Tableau Public

---

## 📫 Contact

For questions or collaborations:

**Sogol Sondossi**  
📧 sogol.sondossi96@gmail.com  
📍 Currently open to data-related roles and internships

---

