# 🛍️ E-Commerce Sales & Operations Analytics Dashboard

An interactive corporate business intelligence dashboard built in Power BI to analyze e-commerce store performance. The report translates raw transactional retail logs into high-impact executive insights covering product demand, category distribution, cash-flow analytics, and localized geographic customer demand across major commercial hubs.

## 📸 Dashboard Preview

![Dashboard Preview](E-commerce.png)

---

## 📊 Report Pages & Architecture

### Page 1 — Store's Sales (Core Executive Interface)
The primary analytics canvas providing a synchronized breakdown of top-line store performance.

| Visual Name | Visual Type | Fields / Logic Used |
| :--- | :--- | :--- |
| **Date Slicer** | Slider | `Date` (Temporal Range) |
| **Metric Toggle** | Slicer Matrix | Interactive Buttons: `By Total Units Sold` vs. `By Number of Orders` |
| **Most Bought Items** | Clustered Bar Chart | `Product` vs. Selected Metric Toggle |
| **Most Popular Category** | Pie Chart | `Category` (% Share of Total Volume) |
| **Geographic Sales** | Line Chart | `City` vs. `Sold by Unit` |
| **Units Sold** | Card Visual | Total Sum of `Quantity` |
| **Order Count** | Card Visual | Distinct Count of `Order_ID` |
| **Total Revenue** | Card Visual | Calculated DAX Measure (Formatted in ₹) |
| **Average Order Value** | Card Visual | Calculated DAX Measure (Formatted in ₹) |

### Page 2 — Map (Spatial Distribution Interface)
A geographic view plotting sales distribution across regional commercial hubs.

| Visual Name | Visual Type | Fields Used |
| :--- | :--- | :--- |
| **Cities Map** | Map Visual | Geographic `City` Coordinates |

---

## 🗂️ Data Schema & Source Table
* **Source Table Name:** `ecommerce_sales`

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| **Order_ID** | Text / Key | Unique transaction identifier |
| **Product** | Text | Consumer product name |
| **Category** | Text | High-level product grouping (Electronics, Fashion, etc.) |
| **Quantity** | Integer | Total units purchased per row |
| **Price** | Decimal | Individual unit cost (Local INR Currency) |
| **City** | Text | Customer destination city across India |
| **Date** | Date | Explicit timestamp of checkout |

---

## 🔑 Core Calculated Business Metrics (DAX)

Instead of relying on raw metrics, the dashboard implements custom DAX logic to measure actual financial and transactional health:

* **Total Revenue:** Iterates line-by-line evaluating sales quantity against individual product price points.
  ```DAX
  Total Revenue = SUMX('ecommerce_sales', 'ecommerce_sales'[Quantity] * 'ecommerce_sales'[Price])
