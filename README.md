

## End-to-End Retail Data Analysis using MySQL

---
 
# A relational database project simulating a **retail store's** back-end operations — schema design, data population, and a progressive set of 25+ SQL queries (Levels 1–6) covering everything from basic filtering to joins, subqueries, and set operations.

---

## 📌 Project Overview

| | |
|---|---|
| **Project Name** | Data Fetching – Retail Store |
| **Objective** | Design a normalized retail database and answer real business questions using progressively advanced SQL |
| **Database** | `retail_store` |
| **Tables** | 6 (customers, products, orders, order_items, payments, product_reviews) |
| **Tools Used** | MySQL |
| **File Type** | `.sql` scripts |

---

## 🎯 Business Problem

A retail store needs to track customers, product inventory, orders, payments, and reviews in one relational system — and answer operational and analytical questions from that data: who are the customers, what's selling, how much revenue is coming in, and which products or customers need attention.

---

## 🗂️ Database Schema

| Table | Description | Key Columns |
|---|---|---|
| `customers` | Registered customers | `customer_id` (PK), name, email, phone, created_at |
| `products` | Product catalog | `product_id` (PK), name, category, price, stock_quantity |
| `orders` | Customer orders | `order_id` (PK), customer_id (FK), order_date, status, total_amount |
| `order_items` | Line items within an order | `order_item_id` (PK), order_id (FK), product_id (FK), quantity, item_price |
| `payments` | Payments made against orders | `payment_id` (PK), order_id (FK), amount_paid, method |
| `product_reviews` | Customer product reviews | `review_id` (PK), product_id (FK), customer_id (FK), rating, review_text |

**Relationships:** `customers` → `orders` → `order_items` → `products`, with `payments` and `product_reviews` linking back to `orders`/`products`/`customers` respectively (1-to-many throughout).

---

## 🛠️ Query Workflow (Level 1 → Level 6)

### Level 1 — Basics
Simple `SELECT`, `WHERE`, `DISTINCT`, `LIKE`, and `ORDER BY` queries — e.g., retrieving customer contact lists, filtering products by price range, finding customers whose names start with a given letter.

### Level 2 — Filtering & Formatting
Handling nulls, column aliasing, computed columns (`quantity × price`), string concatenation (`CONCAT`), and date extraction from timestamps for reporting.

### Level 3 — Aggregations
`COUNT`, `SUM`, `AVG`, and `GROUP BY` to calculate total orders, total revenue, average order value, orders per customer, products sold per category, and payments received per method.

### Level 4 — Multi-Table Queries (Joins)
`INNER JOIN`, `LEFT JOIN`, and `RIGHT JOIN` across customers, orders, order_items, products, and payments — including a 3-table join combining orders, customers, and payments in a single result set.

### Level 5 — Subqueries
Correlated and non-correlated subqueries to find above-average priced products, customers with no orders, products never ordered, and each customer's highest-value order — solved with both classic subqueries and window functions (`OVER (PARTITION BY ...)`).

### Level 6 — Set Operations
`UNION` and membership subqueries to find customers who either ordered or reviewed a product, and customers who did both.

---

## 💡 Sample Queries

```sql
-- Total revenue collected from all orders
SELECT SUM(total_amount) AS total_revenue FROM orders;

-- Customers who have never placed an order
SELECT name FROM customers
WHERE customer_id NOT IN (SELECT customer_id FROM orders);

-- Highest-value order per customer
SELECT c.name, MAX(o.total_amount) AS highest_order_value
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.name;

-- Customers who both placed an order AND reviewed a product
SELECT DISTINCT customer_id FROM orders
WHERE customer_id IN (SELECT customer_id FROM product_reviews);
```

---

## 🧰 Skills Demonstrated

- Relational schema design with primary/foreign key constraints
- Data filtering, sorting, and string/date formatting
- Aggregate functions and `GROUP BY` / `HAVING` reporting logic
- `INNER`, `LEFT`, and `RIGHT` joins across multiple tables
- Correlated subqueries, non-correlated subqueries, and window functions
- Set operations (`UNION`) for combined customer segmentation

---

## 📁 Repository Contents

```
├── Schema_database_tables.sql        # Database & table creation (DDL)
├── DataInsertionQueries.sql          # Sample data population (DML)
├── Queries_Level_1_to_6.sql          # All 25+ business queries, organized by level
└── README.md                         # Project documentation (this file)
```

---

## 🚀 How to Use

1. Run `Schema_database_tables.sql` in MySQL to create the `retail_store` database and its 6 tables.
2. Run `DataInsertionQueries.sql` to populate the tables with sample data.
3. Open `Queries_Level_1_to_6.sql` and run any query to explore the dataset — each is labeled with its business question and difficulty level.

---





