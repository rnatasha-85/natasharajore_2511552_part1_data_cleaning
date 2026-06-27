## 1. List of Issues Found

The following data quality issues were identified during the data cleaning process:

- Missing values in the region column.
- Missing values in the ship_moode column.
- Missing values in the discount column.
- Duplicate records.
- Duplicate order_id values with conflicting information.
- Negative discount values.
- Ship Date earlier than Order Date.
- Sales and profit calculation mismatches.

## 2. Cleaning Actions Performed

The following cleaning actions were performed:

- Removed exact duplicate rows.
- Retained duplicate order_id records with conflicting information and flagged them for review.
- Replaced missing Region values with "Unknown".
- Replaced missing Ship Mode values with "Unknown".
- Replaced missing Discount values with 0 only when all other sales fields were valid.
- Standardized discount values to decimal format where required.
- Flagged records with negative discount values.
- Flagged records with discount values greater than 1 (decimal format).
- Flagged records where the Ship Date was earlier than the Order Date.
- Created required derived fields including shipping_delay_days, cleaned_discount, calculated_sales, calculated_profit, profit_margin, order_month,order_year and data_quality_flag.
- Created additional fields to raise flags, calculate and count missing values, identify data mismatches and identify the fields where missing values were replaced.


## 3. Business Rules Applied

### Business Rule 1:
Rule Area: Missing region
Required Action: Fill as Unknown and flag in quality report

Action Taken:
Replaced all blank Region values with "Unknown".

Reason:
Orders without region information should still be retained for analysis while clearly indicating the region is unknown.

Records affected:25

### Business Rule 2:
Rule Area: Missing ship_mode
Required Action: Fill as Unknown and flag in quality report

Action Taken:
Replaced all blank Ship Mode values with "Unknown".

Reason:
Orders without ship_mode information should still be retained for analysis while clearly indicating the ship_mode is unknown.

Records affected: 21

### Business Rule 3:
Rule Area: Missing discount
Required Action: Treat as 0 only if all other sales fields are valid

Action Taken:
Reviewed all sales fields to check whether they were valid. If they were valid, all blank discount values were replaced with 0.

Reason:
A missing discount is assumed to mean that no discount was applied only when the sales information is complete and valid. If other key sales fields are missing or invalid, the missing discount cannot be safely interpreted as zero and should be left for further review.

Records affected: 18

### Business Rule 4:
Rule Area:Negative discount
Required Action: Flag as invalid

Action Taken:
Negative Discount values were identified and flagged as invalid.

Reason:
Negative discount values are invalid because discounts cannot be less than zero.

Records affected:15


### Business Rule 5:
Rule Area: Discount above allowed range
Required Action:Flag as invalid

Action Taken:
1) First, it was identified that 8 records in the discount column were in percentage format and the rest were in decimal format. So to maintain data consistency, the discount values for the 8 records were converted from percentage format to decimal format.
2) Applied a formula to check whether discount values exceeded the allowed range and flagged them as Invalid.

Reason:
The business rules did not specify the maximum allowable discount. Since the dataset stores discount values in decimal format (e.g., 0.10 = 10%, 0.25 = 25%), a value of 1 represents a 100% discount. As a discount cannot logically exceed 100% of the selling price, all discount values greater than 1 were flagged as invalid.

Records affected: 0


### Business Rule 6:
Rule Area: Cancelled orders
Required Action:Should not contribute to final completed sales summary

Action Taken:
Identified 145 orders with the order status "Cancelled".
Excluded all orders with the order status "Cancelled" from the final completed sales summary. .

Reason:
Cancelled orders do not represent completed transactions and should not contribute to completed sales metrics. Therefore, they are excluded only from the final sales summary and retained in the dataset.

Records affected: 0


### Business Rule 7:
Rule Area: Failed payments
Required Action:Should not contribute to final completed sales summary

Action Taken:
Identified 69 orders with the payment status "Failed". Excluded all orders with the payment status "Failed" from the final completed sales summary. .


Reason:
Orders with failed payments are not successfully completed transactions and should not contribute to completed sales metrics. Therefore, they are excluded only from the final sales summary and retained in the dataset.

Records affected: 0

### Business Rule 8:
Rule Area: Refunded orders
Required Action:Must be separately summarized

Action Taken:
Identified 163 orders with the order status "Refunded". No changes were made to the dataset, as these orders is summarized separately as "Refunded Orders Summary" in the file pivot_summary.xlsx.


Reason:
Refunded orders represent reversed transactions and should be reported separately from completed sales to provide an accurate representation of business performance.

Records affected: 0


### Business Rule 9:
Rule Area: Ship date before order date
Required Action:Flag as invalid shipping record

Action Taken:
Ship date before order date were identified and flagged as invalid shipping record

Reason:
A Ship Date cannot be earlier than the Order Date. Such records indicate a data quality issue and were flagged for review.

Records affected: 93

## 4. Assumptions Made
- Discount values stored in percentage format were converted to decimal format to ensure consistency.
- Since the maximum allowable discount was not specified, discount values greater than 1 (100%) were considered invalid.
- Missing Discount values were replaced with 0 only when all other sales-related fields (Sales, Unit Price, and Quantity) were present, valid, and did not show any significant value differences.
- Returned orders were retained in sales summary because no business rule specified how they should be handled.


## 5. Records Removed
Exact duplicate rows removed = 20


## 6. Records Flagged
Issue	Count
Duplicate order_id values with conflicting information  12
Negative discount values  15
Discount values above 1 (decimal format) 0
Ship Date before Order Date	93

## 7. Limitations of the Cleaning Process
- Business rules were applied only where explicitly provided.
- Returned orders were not excluded because no business rule specified how they should be handled.
- Records with invalid data, such as negative discounts, discounts above 1 (decimal format), and Ship Dates before Order Dates, were flagged but not corrected or removed because no business rules were provided for handling them. These records remain in the dataset and may affect summary reports and analysis.
- Duplicate order IDs with different information need to be checked manually to determine which record is correct.
- The cleaning process required creating several helper columns (such as cleaned_discount, calculated_sales, calculated_profit, profit_margin, and data_quality_flag) to apply the business rules. This made the process time-consuming and increased the complexity of the workbook.
- Some cleaning tasks, such as replacing missing values with "Unknown" or updating discount values, required manual steps. Manual updates can increase the risk of human error.
- This approach is suitable for small datasets but is not practical for very large datasets. 
