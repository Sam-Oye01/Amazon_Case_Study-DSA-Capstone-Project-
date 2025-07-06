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
- **Data Manipulation:**
    - Data sets were added to the data model in the power pivot for easy manipulation and were updated periodically as new columns were being created.
    - Category column was splitted into (Product Category and Produt sub-category) using the "Text to columns" command in the Data tab. The delimiter used was the pipe sign (|)
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

        - Measure 1: =[Count of Product_name]
        - Measure 3: =sum([Review_count])
        - Measure 4: =average([Discount_percentage])

        






