# Retail Data Strategy & Customer Intelligence POS
## Project Scope

This project analyzes retail transaction data in `retail_visualized.ipynb` to build:
- a clean analytical dataset,
- customer behavior segmentation (RFM-style),
- management dashboards for volume and revenue decisions.

---

## Technical Pipeline (Notebook-driven)

The pipeline below follows the exact flow implemented in `retail_visualized.ipynb`.

### 1) Environment and database connection
- Install and import: `ipython-sql`, `plotly`, `psycopg2`, `pandas`, `sqlalchemy`, `matplotlib`.
- Connect to PostgreSQL and create SQLAlchemy engine.

### 2) Data exploration and cleaning
- **Query 1 - Pre-cleaning variables**
  - Baseline profile:
    - `total_rows = 541,909`
    - `invoices = 25,900`
    - `customers = 4,372`
    - `products = 4,070`
    - `countries = 38`
- **Query 2 - Data cleaning**
  - Filter invalid/irrelevant rows and standardize transactional fields.
- **Query 3 - Description deep clean**
  - Detect inconsistent descriptions per `stock_code`.
- **Query 4 - Description standardization**
  - Consolidate each `stock_code` to one unified product description.

### 3) Metrics engineering

#### 3.1 General metrics
- Build SQL views for business monitoring:
  - `total_revenue`
  - `top5_months`
  - `top5_products`
  - `country_customers`

#### 3.2 Customer metrics (RFM logic)
- **Query 5 - Create `customer_metrics`**
  - Features by `customer_id`:
    - `frequency = COUNT(DISTINCT invoice_no)`
    - `monetary = SUM(quantity * unit_price)`
    - `lifespan = MAX(invoice_date) - MIN(invoice_date)` (days)
- **Query 6 - Recency/lifespan segmentation**
  - `< 60 days`: `1,962`
  - `61-180 days`: `740`
  - `> 180 days`: `1,632`
- **Query 7 - Monetary by percentile**
  - Split customers into `Copper`, `Silver`, `Gold`.
- **Query 8 - Frequency by percentile**
  - Split customers into frequency buckets.
- **Query 9 - Behavior mapping**
  - Final segment mapping from frequency x monetary matrix.

### 4) Visualization layer
- **4.1 General metrics visualizing**
  - Revenue scorecard, Top 5 peak months, Top 5 best-selling products, country distribution.
- **4.2 Segment quantity and percentage**
  - Segment distribution table + percentage share.
- **4.3 Top 4 segment quantity visualization**
  - Bar chart + donut chart for dominant segment groups.
- **4.4 Segment revenue visualization**
  - Revenue share by segment (`total_revenue`, `pct_revenue`).

---

## Key Insights

1. **Segment design reality check**
   - Initial 9-segment hypothesis operationally results in **8 active segments**.
   - `Brand Fans` is missing under the current data-driven frequency/monetary logic.

2. **Customer base concentration**
   - Most customers are concentrated in:
     - `One-time Customers`
     - `Middle Customers`
     - `Low Engagement Customers`
   - This indicates a broad but low/medium-engagement customer base.

3. **High-value target groups**
   - Strategic target segments identified in the notebook:
     - `VIP`
     - `Loyal Customers`
     - `Big Spenders`
     - `Key Customers`

4. **Revenue contribution is not proportional to customer count**
   - `VIP` is the **largest revenue contributor**.
   - `Middle Customers` is the **second-largest revenue contributor**.
   - Some high-spend labels (e.g., `Big Spenders`, `Loyal Customers`) contribute less than `One-time Customers` when frequency and segment size are lower.

5. **Managerial implication**
   - Segment sizing alone is insufficient; decisions should combine:
     - **segment size** (quantity share),
     - **segment value** (revenue share),
     - **behavioral profile** (frequency x monetary).

---

## Data Schema Used in Pipeline

Core columns processed:
- `invoice_no`
- `stock_code`
- `description`
- `quantity`
- `invoice_date`
- `unit_price`
- `customer_id`
- `country`

---

## Status

- Technical flow in notebook is implemented end-to-end (cleaning -> metrics -> segmentation -> visualization).
- Next extension options: region x segment strategy, monthly/half-year segment tracking, and forecasting actions.

