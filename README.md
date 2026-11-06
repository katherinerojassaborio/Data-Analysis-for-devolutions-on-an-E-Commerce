# Makaled Consulting Group: Shopify Returns Analysis 

## Context
- **Business:** Shopify, a B2C retail e-commerce business with customers in several countries and a medium-high transaction volume.
- **Problem:** a return rate of ~14% sustained for 3 years, which increases global shipping and logistics costs. No purchasing patterns have been identified that explain the cause.
- **Data:** Kaggle CSV with 60,000 rows and 17 columns (one row per `order_id`). Period from 2023 to June 18, 2025. Manual, one-time load on a copy of the original. There is no connection to the store and no automatic updates.

## Tech stack
- **Python:** Pandas (cleaning and transformation), NumPy (numerical calculations), Seaborn and Matplotlib (EDA charts).
- **Power BI:** dashboard with three views (operational, strategic, and tactical) and global filters.
- **DAX:** measures for the dashboard KPIs.

## Objectives
1. Reduce the global return rate by at least 7% in the next semester.
2. Profile the customers who generate at least 40% of returns and design retention strategies.
3. Reduce the cost of shipments affected by returns by at least 10%.

## Defined KPIs
- **Return rate** by category (and SKU), monthly and semester.
- **Customer return frequency ratio:** distinguishes product problems (returns spread across many customers) from behavior problems (returns concentrated in a few).
- **Buyer severity index:** combines frequency, returned value, and impact on profit, using weights w1, w2, and w3.

## Data processing
- Dates converted to datetime; `is_returned` changed to boolean.
- New fields: `order_month`, `order_day`, and `return_days`.
- Nulls in `return_reason` and `refund_status` replaced with "NA". `traffic_source` was removed.
- The returns table was joined with the main table on `order_id` using a left join.
- `revenue` and `profit` recalculated with real costs: COGS, marketing, payment gateway fees, platform, and staff.
- Outliers (orders of 4 or 5 units, products priced $600 to $800, discount close to 5%) were kept because they are considered valid.

## Key findings
- **Financials:** revenue of $59.65M, net profit of $24.75M, and returns equal to 14.72% of revenue, with losses of approximately $1.7M per semester.
- **Stability:** the monthly rate stays around 14.8% and is not concentrated in a single category, country, or payment method (variations under 15%).
- **Internal causes:** ~33% of returns are due to defective products or wrong sizes. Adding "not as described" and "unexpected quality" brings it to ~62%.
- **Customers:** ~59% are dissatisfied (about 4,950) and ~14% are "toxic" (437 customers), with patterns that erode profits.
- **Return time:** average of 16 days (range 2 to 30), uniform across categories. This rules out mass wardrobing and opens a 14-day window for preventive contact.
- **Logistics:** shipping costs for returned orders are close to $60,000, spread almost evenly across categories (~$8,600 each).
- **Discounts:** raising discounts from 1% to 40% does not reduce returns, but reduces profit per order by 41% (~$90,000).

## Dashboard
The dashboard has three views, with global filters by Country, Product Category, and Update Date:

### Operational view
root causes of returns, recurring customer behavior, and logistics impact.

![Operational view](https://github.com/katherinerojassaborio/Assets/blob/main/shopify_operative.png?raw=true)

### Strategic view
financial health, impact of returns, and effect of discounts on profitability.

![Strategic view](https://github.com/katherinerojassaborio/Assets/blob/main/shopify_strategic.png?raw=true)

### Tactical view
concentration of returns by geography, payment method, category, and time window.

![Tactical view](https://github.com/katherinerojassaborio/Assets/blob/main/shopify_tactical.png?raw=true)

## Recommendations
1. **Quality and catalog:** audit suppliers with the most defects; publish size guides in cm; align photos and descriptions with the manufacturer's specifications.
2. **Discounts:** eliminate or rethink aggressive discounts (30% to 40%).
3. **After-sales:** proactive follow-up with manuals and support before day 16.
4. **Logistics:** require packaging and delivery SLAs from couriers (~1,300 cases of damage and delays).
5. **Return policy:** customers pay the return shipping cost for returns due to "change of mind" (~1,000 cases).
6. **Customer management:** CRM alert for customers with more than 2 returns, and for dissatisfied or toxic customers, offer store credit instead of a cash or card refund.
