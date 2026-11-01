# Capstone : Kenya Retail Intelligence

## Milestone 1: Problem Framing and Data Acquisition

### Problem Statement

A growing Kenyan retail chain operating across multiple counties needs data-driven intelligence to optimize branch operations, customer retention, promotional efficiency, and inventory planning.

### Business Questions

1. **Customer Behavior:** Who buys what, where, and when across different payment channels (M-Pesa vs. Cash/Card)?
2. **Revenue & Margin Drivers:** Which stores, counties, and product categories generate the highest revenue and gross profit margins?
3. **Customer Retention:** Which customer segments are drifting away (churn risk), and which high-value customers belong in premium loyalty tiers?
4. **External Drivers:** How do macro-economic factors (inflation, county population, public holidays) affect purchasing behavior?
5. **Demand Forecasting:** What item-level and store-level demand can be expected next month, to guide inventory replenishment?

### Success Metrics

| Type | Metrics |
|------|---------|
| Financial KPIs | Gross Revenue (KES), Net Revenue (KES), Gross Margin %, Average Basket Value (KES) |
| Customer KPIs | Monthly Active Customers, Customer Lifetime Value (CLV), RFM segment distribution, Churn Rate |
| Operational KPIs | Demand Forecast Accuracy (MAPE < 15%), Promotional Lift % |

### Data Inventory & Provenance Log

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