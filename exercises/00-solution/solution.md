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

## Exercise 02: Prepare Data with Power Query

### Analysis Questions

Now that your data is clean and properly formatted, try to answer these questions using PivotTables:

**1. How much revenue did we generate in 2011, 2012, 2013, and 2014?**

Create a PivotTable:
- Drag **Order Date** to Rows
- Drag **Line Total** to Values

**Answer:**
- 2011: 8,778,552.00
- 2012: 27,133,701.38
- 2013: 32,890,351.72
- 2014: 11,685,099.08

**2. In which month (combining all years) did we generate the most revenue and how much?**

Create a PivotTable:
- Drag **Order Date** to Rows
- Drag **Line Total** to Values
- Sort the Line Total column descending

**Answer:**
- **March** generated the most revenue: 10'676'221.57

> 💡 **Notice how easy this is now?** Because you properly formatted the dates in Power Query, Excel can now group them by year, month, quarter automatically. This is why data preparation matters!

**Key learning:** Students learned to:
- Investigate errors (scrolling to find them, analyzing error messages)
- Navigate backwards through Power Query steps to fix issues at their source
- Modify earlier steps and see how subsequent steps automatically update
- Use locale settings to handle international date formats
- Understand that Power Query's step-based approach is non-linear and powerful

### Key Concept: Refreshable Queries

The power of Power Query is that all transformations are saved as steps. When the source CSV file is updated, you can refresh the query (**Data → Refresh All**) and all cleaning steps are automatically reapplied.

---

## Exercise 03: [Future Exercise]

*Solutions will be added here as exercises are completed*
