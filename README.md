# Amazon_Case_Study-DSA-Capstone-Project

## Project Topic: Amazon Product Review Analysis

### Project Overview 
This project aims to analyse product and customer review data of sellers on Amazon to generate insights that can guide product improvement, marketing strategies, and customer engagement. At the end of this analysis, we should be able to perfectly give perspectives to the trends and patterns accompanying products sales and reviews by customers on Amazon, thus, helping us to make meaningful prescriptions on product improvement strategies.

### Data Source
The primary source of data used here is Amazon case study.xlsx and this data was pooled directly from the Amazon platform and shared by the data analysis facilitator to all students for the project assessment.

[Download here](https://github.com/user-attachments/files/21090025/Amazon.case.study.xlsx)

### Dataset Description 
The dataset contains information scraped from Amazon product pages, including: 
- **Product details:** name, category, price, discount, and ratings.
- **Customer engagement:** user reviews, titles, and content.
- Each row represents a unique product, with aggregated reviewer data stored as comma-separated values

**Total Records:** 1,465
  
**Total Fields:** 16 columns 

### Data Cleaning and Preparation
- **Data Loading and Inspection:**
    - Data sets was converted to a table for easy manipulation.
- **Data Cleaning and formatting:**
    - Filter drop down button was applied to all header column to look for blanks and inconsistent data.
        - All missing numerical data was replaced with the median value of the entire data in the column.
        - All inconsistent numerical data was replaced with the median value of the entire data in the column.
    - Duplicate rows were removed.
    - Column headers were formatted in the proper case.
    - Rating Count column header was changed to Review count.
    - The data types of the columns with quantitative data was formatted appropriately.
- **Data Manipulation:**
    - Data sets were added to the data model in the power pivot for easy manipulation and were updated periodically as new columns were being created.
    - Category column was splitted into (Product Category and Produt sub-category) using the "Text to columns" command in the Data tab. The delimiter used was the pipe sign (|).
    - Two calculated columns were created. They are :
  
``` MS EXCEL ```

         - Potential Revenue: =[@[Actual_price]]*[@[Review_count]]
         - Combined score (Ratings and Reviews count): =([@Rating] * [@[Review_count]])
         
      
    - Conditional columns were created using "IF" function for the following columns:
 
``` MS EXCEL ```
      
        - % Discount distribution: =IF([@[Discount_percentage]] < 50%, "Low discount", "High discount")
        - Price range bucket: =IF([@[Discounted_price]] < 200, "< ₹200", IF(AND([@[Discounted_price]] > 200, [@[Discounted_price]] < 500), "₹200-₹500", "> ₹500"))
        - Product Main Category: =IF([@[Product Category]] = "Computers&Accessories", "Computers & Accessories", IF([@[Product Category]] = "Cars&Motorbike", "Cars & Motorbike", IF([@[Product Category]] = "Health&PersonalCare", "Health & Personal Care", IF([@[Product Category]] = "Home&Kitchen", "Home & Kitchen", IF([@[Product Category]] = "HomeImprovement", "Home Improvement", IF([@[Product Category]] = "MusicalInstruments", "Musical Instruments", IF([@[Product Category]] = "OfficeProducts", "Office Products", IF([@[Product Category]] = "Toy&Games", "Toy & Games", "Electronics"))))))))
        - Rating boundaries: =IF([@Rating] < 1, "0 - 1.0", IF(AND([@Rating] < 2,[@Rating] > 1), "1.0 - 2.0", IF(AND([@Rating] < 3,[@Rating] > 2), "2.0 - 3.0", IF(AND([@Rating] < 4, [@Rating]> 3), "3.0 - 4.0", "4.0 - 5.0"))))
        - % Discount boundaries: =IF([@[Discount_percentage]] < 20%, "< 20%", IF(AND([@[Discount_percentage]] < 40%, [@[Discount_percentage]] > 20%), "20% - 40%", IF(AND([@[Discount_percentage]] < 60%, [@[Discount_percentage]] > 40%), "40% - 60%", IF(AND([@[Discount_percentage]] < 80%, [@[Discount_percentage]] > 60%), "60% - 80%", "80% - 100%"))))
        - Review count distribution: =IF([@[Review_count]] < 1000, "Low reviews", "High reviews")


- Three measures were created on the power pivot

``` MS EXCEL ```

        - Measure 1 as Total products: =[Count of Product_name]
        - Measure 3 as Total review count: =sum([Review_count])
        - Measure 4 as Avg % Discount: =average([Discount_percentage])

        
### Exploratory Data Analysis (EDA)
EDA involved the exploring of the data to answer some questions about the data such as;

1. What is the average discount percentage by product category? 
2. How many products are listed under each category? 
3. What is the total number of reviews per category?  
4. Which products have the highest average ratings? 
5. What is the average actual price vs the discounted price by category? 
6. Which products have the highest number of reviews? 
7. How many products have a discount of 50% or more? 
8. What is the distribution of product ratings (e.g., how many products are rated 3.0, 
4.0, etc.)? 
9. What is the total potential revenue (actual_price × rating_count) by category? 
10. What is the number of unique products per price range bucket (e.g., <₹200, 
₹200–₹500, >₹500)? 
11. How does the rating relate to the level of discount? 
12. How many products have fewer than 1,000 reviews? 
13. Which categories have products with the highest discounts? 
14. Identify the top 5 products in terms of rating and number of reviews combined.


**Task-by-Task Power Pivot Execution:**

Insert Pivot Table using Data Model.

Task 1: Average Discount % by Product Category
- Rows: Product Main Category.
- Values: Discount_percentage (set to Average).
- Format values as Percentage.

Task 2: Product Count by Category
- Rows: Product Main Category.
- Values: Product_name (set to Distinct Count).

Task 3: Total Reviews by Category
- Rows: Product Main Category.
- Values: Review_count (set to Sum).

Task 4: Products with Highest Ratings
- Rows: Product_name.
- Values: Rating (set to Average).
- Sort Descending by Rating.
- Filter to show Top 10.

Task 5: Average Actual Price vs Discounted Price by Category
- Rows: Product Main Category.
- Values: Actual_price (set to Average).
- Values: Discounted_price (set to Average).

Task 6: Products with Most Reviews
- Rows: Product_name.
- Values: Review_count (set to Sum).
- Sort Descending by Review Count.

Task 7: Products with High (50% or More) Discount
- Rows: High Discount.
- Values: Product_name (set to Count).

Task 8: Distribution of Product Ratings
- Rows: Rating.
- Values: Product_name (set to Count).

Task 9: Total Potential Revenue by Category
- Rows: Product Main Category.
- Values: Potential Revenue (set to Sum).

Task 10: Unique Products per Price range bucket
- Rows: Price Range Bucket.
- Values: Product_name (set to Distinct Count).

Task 11: Rating by % Discount
- Rows: Discount_percentage (group into bands)
- Values: Rating (set to Average).

Task 12: Count of Products with High (< 1,000) Reviews
- Rows: Low Reviews.
- Values: Product_name (set to Count).

Task 13: Product Categories with Highest % Discounts
- Rows: Product Main Category.
- Values: Discount_percentage (set to Average).
- Sort Descending.

Task 14: Top 5 Products by Rating and Review count combined
- Rows: Product_name.
- Values: Combined Score (set to Sum).
- Sort Descending.
- Filter Top 5.


### Visualization and Reporting

**Dashboard creation**

Dashboard Structure (Layout)

| Section | Visuals Included | Notes |
| :-----: | :-------------: | :----: |
| Header Area (Top Row) | Dashboard Title: Amazon Product Review Dashboard, Date of Last Refresh, Name/Project Label | Text box is used with bold and large fonts for the title |
| Key Metrics Section (KPIs) |  Total Reviews, Total Number of Products, Avg. Discount %, Total Potential revenue | Shapes with bold numbers were used |
| Interactive Slicers (Filters) | Price Range Bucket | Real-time filtering across visuals were used |
| Visual 1 & 2: Product Categories Overview	| Bar Chart: Number of Products by Category,  Pie Chart: % Discount by Product Category  |  |
| Visual 3 & 4 : Price Range Analysis	| Donut Chart: Product Count by Price Range Bucket, Bar Chart: Avg. Price vs Discounted Price by Category | Helps illustrate price segmentation | | Visual 5: Discount & Rating Relationship | Column Chart: discount_percentage vs rating |  |
| Visual 6: Review Insights	| Bar Chart: Total Reviews by Main Category	Display side by side for comparison |  |
| Visual 7: Top Products Snapshot	| Column Chart showing Top 5 Products by Combined Score	For highlighting high-performing products |  |
| Visual 8: Revenue Insights | Bar Chart: Total Potential Revenue by Main Category |  |


 


                          







