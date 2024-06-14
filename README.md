# Eagle-Project-Cigarette-Sales-Analysis , Associated with NielsenIQ
Eagle Project : Cigarette Sales AnalysisEagle Project : Cigarette Sales Analysis
Feb 2022 - Apr 2022Feb 2022 - Apr 2022


Detail Data Cleaning Stage
Objective :
The project aims to analyze sales data for different cigarette brands to identify the best-selling products and provide insights for informed business decisions. This involves examining weekly sales figures, pricing strategies, and purchase volumes for various brands.

Background
During the pandemic period, the client required detailed insights into product status in the market. The Data Acquisition (DA) team conducted surveys via phone calls across 22,000 outlets, covering both on-premise and off-premise channels. The surveys included 10 main questions focusing on various aspects such as product availability, claim sales, selling price, purchase price, SOP, FOP, selling format, most selling bundles, and bundle selling price.
Challenges Faced
For the data cleaning rules: We collaborated with the operations team during the data mapping validation stage to establish data-checking rules.
Data Volume and Complexity: Each batch of raw data, received every three days, contained 268 columns, leading to a substantial amount of data to validate.
Survey Specificity: The surveys encompassed 20 products per main question, which significantly increased the validation time.
Resistance from Shop Owners: Auditors faced challenges as shop owners sometimes refused to participate in the phone surveys.
Data Validation and Cleaning Process
Initial Extraction for Specific Checks:
Selling Cigarettes Check: 
sql
SELECT
*
FROM
    survey_data
WHERE
    selling_cig = 'No'
    AND product_availability_checked = 'Yes';
If the "Selling Cig" column was marked as "No" but product availability was checked, a recheck was initiated by calling the shop owners to confirm the records.


Price Validation:
Extracting Data with Prices Greater than Averages:
sql
Copy code
WITH AvgPrices AS (
    SELECT
        AVG(selling_price) AS avg_selling_price,
        AVG(purchasing_price) AS avg_purchasing_price
    FROM
        survey_data
)
SELECT
    *
FROM
    survey_data
WHERE
    selling_price > (SELECT avg_selling_price FROM AvgPrices)
    AND purchasing_price > (SELECT avg_purchasing_price FROM AvgPrices);
Extracting Data with Prices Less than Averages:
sql
Copy code
WITH AvgPrices AS (
    SELECT
        AVG(selling_price) AS avg_selling_price,
        AVG(purchasing_price) AS avg_purchasing_price
    FROM
        survey_data
)
SELECT
    *
FROM
    survey_data
WHERE
    selling_price < (SELECT avg_selling_price FROM AvgPrices)
    AND purchasing_price < (SELECT avg_purchasing_price FROM AvgPrices);

Handling Incomplete and Erroneous Data:  
Any data with missing or incomplete values was flagged, and the DA team supervisor reconducted the survey to reduce the error rate.
Data Transformation: 
Once all validation was completed, the required data types were converted using Power Query in Excel to ensure consistency and accuracy.


Data Analysis and Findings:
  The data provided includes sales and pricing information for multiple cigarette brands. Key metrics analyzed include the number of packs sold per week, the selling price per pack, the purchase price per pack, and the purchase volume per frequency.
  
Selling Format and Bundle Sales:
The details about selling formats, including per stick and various bundle options, indicate popular packaging preferences among consumers. Analysis of the most selling bundles provides insights into consumer purchasing behavior and preferences.

Recommendations:
Based on the analysis, the recommendations are to focus on top-selling products, optimize pricing strategy, enhance bundle offers, and monitor purchase patterns.


Conclusion:
The project provides valuable insights into the sales performance of various cigarette brands, enabling the client to make informed decisions to enhance product offerings, optimize pricing, and improve overall business performance.
Skills: Data Analysis · Microsoft Power Query · microsoft power bi · Reporting & Analysis · SQL
