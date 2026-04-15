# Solutions Guide

This file contains answers to the exploration and analysis questions across all exercises in this Business Intelligence course.

---

## Exercise 01: Data Exploration with Excel

### For Products:

- **How many products do we have in total?**  
  **Answer:** 295  
  **How to get this:** In the products worksheet, select the table and use the total row to count all non-empty cells in column A (ProductID) minus the header row. Alternatively, look at the row numbers in the table - the last row number minus 1 gives you the count.

- **How many different product categories or models do we have?**  
  **Answer:** 119  
  **How to get this:** Create a PivotTable with Model in the Rows area and look at the row numbers in the table - minus the beginning rows at the top. You can also use Remove Duplicates on a copy of the Model column and count the remaining rows.

- **What is the list price range of our products?**  
  **Answer:** $2.29 - $3,578.27  
  **How to get this:** Use `MIN` and `MAX` on the ListPrice column with Total Row enabled to find the minimum and maximum prices. Alternativley, select the filter option on the ListPrice column and check the minimum and maximum values. Lastly, you could sort the table ASC or DESC to get the min and max values.

### For Orders:

- **How many unique orders were placed?**  
  **Answer:** 3,806  
  **How to get this:** Create a PivotTable with SalesOrderID in the Rows area and look at the row numbers in the table - minus the beginning rows at the top. You can also use Remove Duplicates on a copy of the SalesOrderID column and count the remaining rows.

- **Which products appear most frequently in orders?**  
  **Answer:**
  - Product 712: 1,192 times
  - Product 715: 1,183 times
  - Product 711: 965 times
  
  **How to get this:** Create a PivotTable with ProductID in the Rows area and ProductID in the Values area (set to Count). Sort the count column in descending order to see which products appear most frequently.

- **What is the total value of all orders?**  
  **Answer:** $80,487,704.18  
  **How to get this:** Use the formula `SUM` on the LineTotal column with Total Row enabled to find the sum, or create a PivotTable with LineTotal in the Values area set to Sum.

---

## Exercise 02: [Future Exercise]

*Solutions will be added here as exercises are completed*

---

## Exercise 03: [Future Exercise]

*Solutions will be added here as exercises are completed*
