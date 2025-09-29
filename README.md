# Pandas Filtering Practice — Realistic Datasets

This bundle contains two realistic, multi-table datasets you can use to master **Day 3: Pandas Filtering**.

## 1) Retail Sales (2024)
**Files:** `retail_sales/customers.csv`, `stores.csv`, `products.csv`, `calendar.csv`, `transactions.csv`  
**Highlights for filtering:**
- Date filters (weekends, promo days, specific months/quarters)
- Numeric ranges & outliers (`unit_price`, `quantity`, `line_total`)
- Logical masks (e.g., returns where `quantity < 0`, anomalies like negative prices)
- Categorical filters (`category`, `payment_method`, `city`)
- Null handling (`age` with missing values)
- Multi-table joins then filter (e.g., top categories in specific cities)
- Regex/text filters on `product_name`

**Starter tasks:**
1. Select transactions from **Q2 2024** with `discount_pct >= 0.10` and `quantity >= 2`.
2. Find **suspicious rows**: negative `unit_price` or `line_total`, or `unit_price > 200`.
3. Keep only **weekend sales** for **Bakery** products purchased by **card**.
4. Customers with missing `age` — filter and impute with city median (practice filtering before imputation).
5. Join `transactions`→`products`→`stores` and filter to **Tashkent** stores, **Beverages** category.
6. Filter products where `product_name` **contains** `Premium` **and** not discontinued.
7. Use `query()` API to express: `quantity >= 3 and discount_pct in [0.1, 0.15, 0.2]`.
8. Filter top 5 stores by **weekend revenue** in May 2024 (combine filter + groupby).

## 2) Student Records (2024–2025)
**Files:** `student_records/students.csv`, `courses.csv`, `enrollments.csv`, `attendance.csv`, `grades.csv`  
**Highlights for filtering:**
- Time-window filters on `attendance.date` (e.g., midterm weeks)
- Value checks and impossible values in `grades.overall` (e.g., `< 0 or > 100`)
- Categorical filters (`major`, `faculty`, `status`, `letter`)
- Membership filters with `.isin()` (e.g., majors in a shortlist)
- Join filters (students + enrollments + courses for a semester)
- Handling missing `city`

**Starter tasks:**
1. Filter **active** enrollments in **Spring 2025** 300/400-level courses.
2. Find students with **scholarship >= 75** outside **Tashkent**.
3. Identify **grade anomalies** where `overall < 0 or overall > 100` and remove them.
4. Attendance filter: students with **< 70% presence** in any course.
5. Use `between()` to keep `overall` in **[85, 95]** and letter in `['A-', 'A']` — compare results.
6. Filter enrollments **dropped within 2 weeks** from `enrolled_on` (simulate with date filters).

---

## Suggested Folder Structure
```
pandas_filtering_realistic_datasets/
  retail_sales/
    customers.csv
    stores.csv
    products.csv
    calendar.csv
    transactions.csv
  student_records/
    students.csv
    courses.csv
    enrollments.csv
    attendance.csv
    grades.csv
  README.md
```

## Quick-Start (Python)
```python
import pandas as pd

tx = pd.read_csv("retail_sales/transactions.csv", parse_dates=["date"])
products = pd.read_csv("retail_sales/products.csv")
stores = pd.read_csv("retail_sales/stores.csv")
cal = pd.read_csv("retail_sales/calendar.csv", parse_dates=["date"])

# Example: weekend, bakery, paid by card
bakery_weekend = (
    tx.merge(products, on="product_id")
      .merge(stores, on="store_id")
      .merge(cal, on="date")
      .query("category == 'Bakery' and payment_method == 'Card' and is_weekend")
)

# Student example: grade anomalies
grades = pd.read_csv("student_records/grades.csv")
grade_anomalies = grades[(grades["overall"] < 0) | (grades["overall"] > 100)]
```

Happy filtering! 🎯
