# Sales Data Analysis Project

This project presents an end-to-end workflow for analyzing sales data using SQL and Python, including database design, preprocessing, exploratory data analysis, and advanced analytical insights.

---

## 🗂 Project Structure

| Notebook Filename | Description |
|-------------------|-------------|
| `sales-db&preprocessing.ipynb` | Creating and populating the SQLite database with realistic sales data |
| `sales-basicanalysis (sql).ipynb` | SQL-based exploratory analysis using aggregation, grouping, filtering, etc. |
| `sales-advanced analysis (python).ipynb` | Advanced analysis and visualizations using pandas and matplotlib |

---

## 1️⃣ Database Schema

In `sales-db&preprocessing.ipynb`, we created a relational SQLite database from scratch.

### Tables

- `customers`  
  - `customer_id` (Primary Key)  
  - `name`  
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

| customer_id | name       | location  |
|-------------|------------|-----------|
| 1           | Alice Doe  | Berlin    |
| 2           | John Smith | Amsterdam |

---

## 2️⃣ SQL-Based Analysis

Notebook: `sales-basicanalysis (sql).ipynb`

We performed the following types of queries using raw SQL on the created database:

### 🔹 Sample Queries

- **Total sales per product:**
```sql
SELECT p.product_name, SUM(od.quantity * p.price) AS total_sales
FROM order_details od
JOIN products p ON od.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_sales DESC;
```

- **Top customers by total purchase:**
```sql
SELECT c.name, SUM(od.quantity * p.price) AS total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
JOIN order_details od ON o.order_id = od.order_id
JOIN products p ON od.product_id = p.product_id
GROUP BY c.name
ORDER BY total_spent DESC;
```

### 📊 Sample Result

| Product Name | Total Sales (€) |
|--------------|-----------------|
| Monitor      | 2,300           |
| Mouse        | 1,800           |
| Laptop       | 1,200           |

---

## 3️⃣ Advanced Analysis & Visualizations

Notebook: `sales-advanced analysis (python).ipynb`

We used **pandas** for further data wrangling and **matplotlib**/**seaborn** for visualizations.

### 📌 Sample Analysis

- **Monthly sales trend**
- **Top selling product categories**
- **Correlation between quantity and revenue**
- **Most active customers**
- **Seasonal fluctuations in order volume**

### 📈 Example Plot: Monthly Sales

```python
df['order_date'] = pd.to_datetime(df['order_date'])
monthly_sales = df.groupby(df['order_date'].dt.to_period('M'))['revenue'].sum()
monthly_sales.plot(kind='bar', figsize=(10,5), title='Monthly Revenue')
```

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
pandas
matplotlib
seaborn
scikit-learn
mlxtend
ipython-sql

---

## 🔍 Goals Achieved

- Practiced SQL and database schema design
- Wrote complex joins, filters, and aggregations
- Transitioned SQL data into pandas for deeper analysis
- Visualized key business metrics

---

## 📫 Contact

For questions or collaborations:

**Sogol Sondossi**  
📧 sogol.sondossi96@gmail.com  
📍 Currently open to data-related roles and internships

---
