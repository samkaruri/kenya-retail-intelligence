# Capstone : Kenya Retail Intelligence

## Milestone 1: Problem Framing and Data Acquisition

### Problem Statement

A growing Kenyan retail chain operating across multiple counties needs data-driven intelligence to optimize branch operations, customer retention, promotional efficiency, and inventory planning.

### Business Questions and Success Measures

#### Q1. Customer Behavior

**Question:** 

Who buys what, where, and when across different payment channels (M-Pesa vs. Cash/Card)?

**Specific questions:**
1. What share of transactions and net sales does each payment method account for, by store, county and product category?
2. On which days of the week does each payment method peak?

**Success measures:**

**Payment mix:**
Share of transactions and net sales by payment method, split by store, county, product category and day of week.

**Significance:**

Chi-square test of independence between payment method and category, and between payment method and county, at the 5% level, with Cramér's V to show how large any difference is.
 
**Output:**

For each payment channel, the top 3 categories and peak days, and a clear statement of whether payment mix differs significantly by county and category.

#### Q2. Revenue & Margin Drivers

**Question:** 

Which stores, counties, and product categories generate the highest revenue and gross profit margins?

**Specific questions:**

1. How do the 10 stores, the counties and the product categories rank by net sales and by gross margin %?
2. Which segments have a margin well above or below the overall margin?

**Success measures:**

**Metrics:**
Net sales and gross margin % (gross profit ÷ net sales) for each store, county and category.

**Reconciliation:**

After cleaning, segment totals must equal total net sales and total gross profit, with a difference of 0 KES.

**Output:**

A full ranking by revenue and by margin, with any segment flagged whose margin is more than 2 percentage points from the overall margin.

#### Q3. Customer Retention

**Question:** 

Which customer segments are drifting away (churn risk), and which high-value customers belong in premium loyalty tiers?

**Specific questions:**

1. How many days usually pass between a customer's purchases, and what share of customers have been inactive longer than that?
2. Does churn differ by loyalty tier, county or preferred payment method?
3. Which customers have high RFM scores but sit in a low loyalty tier?

**Success measures:**

**Churn cutoff and rate:**

A customer is churned if inactive for longer than the cutoff, set from the observed gap between purchases (starting point: 90 days). Report the overall churn rate.

**Segment differences:**

Churn rate for each loyalty tier, county and payment method, with a chi-square test at the 5% level.

**Loyalty tiers:**

score customers on recency, frequency and spend (RFM). High-value means the top 20% by RFM score. Report how many high-value customers are not in the top tier, and their share of total net sales.

#### Q4. External Drivers

**Question:**

How do inflation, county population and public holidays affect purchasing behavior?

**Specific questions:**

1. Do daily sales and basket size rise or fall around public holidays compared with ordinary days?
2. Does monthly net sales (and average basket value) move with the 12-month inflation rate?
3. Do sales per store scale with the population of the county the store is in?

**Success measures:**

**Holidays:**

Compare average daily net sales on holidays, the 3 days before and ordinary days, using a Mann-Whitney U test at the 5% level. Report the percentage difference, not only the p-value.

**Inflation:** 

Spearman correlation between monthly net sales and the 12-month inflation rate, with the number of months used. With few months, treat the result as indicative rather than conclusive.

**Population:** 

Net sales per 1,000 residents for each county with a store, and the Spearman correlation between county population and total net sales.

### Q5. Demand Forecasting

**Question:** 

What item-level and store-level demand can be expected next month?

**Specific questions:**

1. How well can next month's units sold be predicted for each store and for each product?
2. Does a forecasting model beat a simple baseline, and by how much?

**Success measures:**

**Setup:**

Aggregate sales to monthly units per store and per product. Hold out the most recent 2 months as a test set and forecast them using only earlier data.

**Error metric:** 

WAPE (sum of absolute errors ÷ sum of actual units), reported at store level and product level.

**Baselines:** 

(a) naive: next month equals last month, and (b) 3-month moving average. Add same-month-last-year if at least 24 months of data exist.

**Success:**

The chosen model has a lower WAPE than the best baseline on the test months, and store-level WAPE is below 15%. Report product-level WAPE too, even if it is higher.

## Success Metrics

**Financial:**

Gross Revenue (KES), Net Revenue (KES), Gross Margin %, Average Basket Value (KES)

**Customer:**

Monthly Active Customers, Customer Lifetime Value (CLV, defined as total gross profit per customer over the data period), RFM segment distribution, Churn Rate

**Operational:**

Demand Forecast Accuracy (store-level WAPE below 15% and lower than the best baseline), Promotional Lift % (average daily net sales on promotion days versus non-promotion days)


#### Data Inventory & Provenance Log

**Sales period:** 1 Jan 2025 to 31 Oct 2026 (22 months).

The dataset combines synthetic internal transaction data with public Kenyan context data. The inflation and holiday files cover a wider range than the sales data and are filtered to the sales period when joined.

All raw files are in `data/raw/`.

| Table | Description | Rows x Cols | Key Fields | Acquisition Method | License / Terms |
|-------|-------------|-------------|------------|--------------------|-----------------|
| sales_transactions.csv | Transaction line items | 113,377 x 15 | transaction_id, transaction_date, customer_id, store_id, product_id, quantity, unit_cost_kes, unit_price_kes, gross_sales_kes, promo_id, discount_amount_kes, net_sales_kes, cogs_kes, gross_profit_kes, payment_method | Synthetic, generated | Synthetic data, free to use for this project |
| customers.csv | Customer master directory | 1,200 x 8 | customer_id, customer_name, gender, age, county, signup_date, preferred_payment_method, loyalty_tier | Synthetic, generated | Synthetic data, free to use for this project |
| stores.csv | Retail branch network | 10 x 7 | store_id, store_name, county, sub_county, store_format, sqft, opening_date | Synthetic, generated | Synthetic data, free to use for this project |
| products.csv | FMCG product catalog | 15 x 6 | product_id, product_name, category, sub_category, unit_cost_kes, unit_price_kes | Synthetic, generated | Synthetic data, free to use for this project |
| promotions.csv | Marketing and seasonal promos | 9 x 3 | promo_id, promo_name, discount_pct | Synthetic, generated | Synthetic data, free to use for this project |
| 2019-population_census-report-per-county.csv | County demographics (2019 census) | 47 x 11 | County, Total_Population19, Male populatio 2019, Female population 2019, Households, Av_HH_Size, LandArea, Population Density, Population in 2009, Pop_change, Intersex population 2019 | County-level figures from the KNBS *2019 Kenya Population and Housing Census, Volume 1: Population by County and Sub-County* (PDF): https://www.knbs.or.ke/wp-content/uploads/2023/09/2019-Kenya-population-and-Housing-Census-Volume-1-Population-By-County-And-Sub-County.pdf, accessed 25 October 2026. Converted from PDF to Excel/CSV using iLovePDF. | © KNBS. Extracts may be published if the source is duly acknowledged (per [www.knbs.or.ke](https://www.knbs.or.ke)). Used here with attribution to KNBS. |
| cbk_inflation rates.csv | Monthly inflation rates (Jan 2023 to Sep 2026) | 45 x 4 | Year, Month, Annual Average Inflation, 12-Month Inflation | Downloaded from the Central Bank of Kenya (CBK) inflation rates page: https://www.centralbank.go.ke/inflation-rates/, accessed 25 October 2026. One CSV was downloaded per year and combined into a single file. | © Central Bank of Kenya. No specific data licence stated on the page; published CBK statistics used for non-commercial educational purposes with attribution to CBK. |
| kenya_public_holidays.csv | Kenya public holidays (Jan 2020 to Oct 2026) | 98 x 3 | Date, Day, Holiday_Name | Downloaded as a PDF from the Citizen Guide Kenya holidays page: https://www.citizenguide.ke/society-and-culture/holidays, accessed 25 October 2026. Converted from PDF to CSV using iLovePDF. | No specific data licence found on the page; public holiday dates are public information, used for non-commercial educational purposes with attribution to Citizen Guide Kenya. |

**Attribution:** County population data: Kenya National Bureau of Statistics (KNBS), 2019 Kenya Population and Housing Census.

**Attribution:** Inflation data: Central Bank of Kenya (CBK), https://www.centralbank.go.ke/inflation-rates/

**Attribution:** Public holiday data: Citizen Guide Kenya, https://www.citizenguide.ke/society-and-culture/holidays


### Updates on Reviewers' feedback.

**Duplicate transaction IDs.**

35,379 transaction_id values appear on more than one row (89,824 rows in total). 
These are line items in multi-product baskets: each row has the same date, customer, store and payment method but a different product_id. Separately, 209 rows are exact copies of another row across every column (same transaction_id, product_id, quantity and price). 
These are treated as duplicate records and will be removed during data cleaning in Milestone 2.

### How the synthetic tables were generated

The five synthetic tables (sales_transactions , customers, stores, products, promotions) were generated with Google NotebookLM in October 2026 by prompting it
to produce CSV files matching the project schema. NotebookLM has no seed or temperature setting, so generation is not deterministic.

**Limitations:**

The original prompt and chat history were not saved, and the tables cannot be regenerated identically. The CSV files committed in data/raw/ are the reference copy, and all analysis uses those files. Any tables created in later milestones will come from a committed script with a fixed random seed.

**Checks after generation:** 

Row and column counts match this inventory, and the duplicate check on sales_transactions is documented in notebook 01 (see below).

### Specific Business questions.

I updated the to be specific for insightful analysisis.
