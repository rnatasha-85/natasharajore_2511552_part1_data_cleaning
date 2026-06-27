# natasharajore_2511552_part1_data_cleaning

## Part 1 - Data Cleaning

### 1. Problem Summary

The objective of this project was to clean and validate a retail sales dataset containing missing values, duplicate records, invalid discounts, date issues, calculation mismatches, and order status inconsistencies. After applying the required business rules, an analysis-ready dataset, summary reports, and PivotTables were created for business review.

### 2. Dataset Description

Dataset Location : https://drive.google.com/drive/folders/1cw74bVyMhB-earvIhkARsd8ENDFXIu_E?usp=sharing \
Part 1 folder \
Data set file: raw_orders.xlsx

The dataset contains order-level retail sales data exported from multiple internal systems.
it includes the following details:

- Order ID
- Order Date
- Ship Date
- Customer ID
- Customer Name
- Customer Segment
- Region
- State
- City
- Category
- Sub-category
- Product Name
- Ship Mode
- Quantity
- Unit Price
- Discount
- Sales
- Cost
- Profit
- Payment Status
- Order Status


### 3. Tools Used
Microsoft Excel
- Excel Formulas
- Pivot Tables
- Sorting and Filtering
- Pivot Charts

### 4. Cleaning Steps Performed

The following data cleaning activities were completed:

- Checked and removed exact duplicate rows.
- Identified duplicate Order IDs with conflicting information.
- Handled missing values.
- Standardized discount values.
- Applied business rules.
- Validated sales and profit calculations.
- Created derived fields:
  -- shipping_delay_days
  -- cleaned_discount
  -- calculated_sales
  -- calculated_profit
  -- profit_margin
  -- order_month
  -- order_year
  -- data_quality_flag
- Created additional columns to raise flags, calculate and count missing values, identify data mismatches and identify the fields where missing values were replaced.
- Generated data quality summaries.
- Created pivot reports for business analysis.

### 5. Business Rules Applied

The following business rules were applied:

- Missing Region values were replaced with "Unknown".
- Missing Ship Mode values were replaced with "Unknown".
- Missing Discount values were replaced with 0 only when all other sales fields were valid.
- Negative Discount values were flagged as invalid.
- Discount values above 1 (decimal format) were flagged as invalid.
- Cancelled orders were excluded from completed sales summaries.
- Failed payment orders were excluded from completed sales summaries.
- Refunded orders were summarized separately.
- Ship Date earlier than Order Date was flagged as an invalid shipping record.

### 6. Summary of Data Quality Issues Found

The following issues were identified:

- Missing values
- Exact duplicate rows
- Duplicate Order IDs with conflicting information
- Negative discount values
- Discount values above 1(decimal value)
- Invalid shipping dates
- Sales and profit calculation mismatches

A detailed summary is available in data_quality_report.xlsx.

### 7. Summary of Final Pivot Reports

The following pivot reports were created:

- Sales and Profit by Region
- Sales and Profit by Category and Sub-category
- Order Count by Ship Mode
- Profit Margin by Customer Segment
- Refunded, Cancelled, and Failed Orders by Region
- Monthly Sales Trend
- Separate Refunded Orders Summary

The pivots can be viewed in pivot_summary.xlsx file

### 8. Key Business Insights

Examples of insights obtained from the cleaned dataset include:

- Top 2 Regions generating the highest sales and profit
  -- South and West
  
- Best-performing product categories and sub-categories
  -- Technology is the top performing product category and within it Copiers is the top sub-category followed by accessories
  
- Customer segments with the highest profit margins.
  -- Customer Segment - Small Business had the highest profit margin followed by Home Office
  
- Monthly sales trends.
  -- Monthly sales were relatively stable across most months, with peak sales occurring in June and October 2024 and February–September 2025. A sharp decline was observed during the last quarter of 2025, particularly in November and December.
  
- Distribution of refunded, cancelled, and failed orders across regions.
  -- The South region recorded the highest overall order volume (225), while the East and West regions followed closely with 224 orders each. In every region, paid orders represented the majority of transactions, whereas failed, pending, and refunded orders accounted for a relatively small proportion of the total orders.

- Overall data quality issues identified in the dataset.
  -- Missing values were identified in the Region, Ship Mode, and Discount columns and were handled according to the business rules.
  -- Exact duplicate records and duplicate Order ID values with conflicting information were identified during data validation.
  -- A few records contained invalid discount values, such as negative discounts and discounts greater than 100%, which were flagged for review.
  -- Overall, the dataset was cleaned, validated, and made analysis-ready while retaining flagged records for further business review where required.

### 9. Assumptions and Limitations
Assumptions
- Discount values stored as percentages were converted to decimal format.
- Since the maximum discount limit was not specified, discount values greater than 1 (decimal foramt) were treated as invalid.
- Missing discount values were replaced with 0 only when all other sales fields were valid.
- Returned orders were retained because no business rule specified how they should be handled.

Limitations
- Invalid records were flagged but not corrected or removed because no business rules were provided for handling them.
- Manual data cleaning steps may introduce human error.
- Several helper columns were required to implement the business rules, making the workbook more complex.
- The manual cleaning approach is suitable for small datasets but is not efficient for very large datasets.

### 10. Screenshots Included

The project includes screenshots of:
- Raw dataset before cleaning
- Cleaned dataset with calculated columns
- First Major Pivot Summary - Sales and Profit by Region
- Another Major Pivot Summary - Profit Margin by Customer 
