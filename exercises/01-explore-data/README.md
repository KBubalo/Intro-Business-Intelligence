# Step 1: Data Exploration with Excel

Welcome to the first exercise! In this step, you'll learn how to import CSV files into Microsoft Excel and explore the data using basic Excel features.

## What You'll Learn

- How to import CSV files using Excel's Get Data feature
- How to view and understand your data structure
- How to sort and filter data
- How to create simple PivotTables
- How to identify data quality issues (like date formatting)

## Prerequisites

- Microsoft Excel 2016 or newer (including Microsoft 365)
- The CSV files from the `data` folder in this repository

---

## Goal of This Exercise

The goal is not to find perfect answers, but to get comfortable:

- Looking at unfamiliar data
- Asking simple questions
- Using Excel as a data exploration tool

There is no single "correct" way to explore the data.

---

## Getting Started

### Import the CSV Files

You will work with TWO CSV files in this exercise:
- **orders.csv** - Contains order transaction data
- **products.csv** - Contains product information

### Step 1: Import orders.csv

1. Open Microsoft Excel
2. Go to the **Data** tab on the ribbon
3. Click **Get Data** → **From File** → **From Text/CSV**
4. Navigate to the `data` folder in the repository
5. Select **orders.csv**
6. Click **Import**
7. A preview window will appear showing your data
   - Excel will automatically detect column headers and data types
   - Review the preview to ensure it looks correct
8. Click **Load** to import the data into a new worksheet

Excel will create a new sheet with your orders data loaded as a table.

### Step 2: Import products.csv

Repeat the same process for the products file:

1. Go to the **Data** tab
2. Click **Get Data** → **From File** → **From Text/CSV**
3. Navigate to the `data` folder
4. Select **products.csv**
5. Click **Import**
6. Review the preview
7. Click **Load**

You should now have two worksheets in your Excel workbook: one for orders and one for products.

---

## Exploring the Data

Now that your data is loaded, let's explore it! Work with each worksheet separately.

### View Column Names and Data Types

1. Look at the **column headers** (first row) - these tell you what each column represents
2. Scroll through a few rows to see sample data
3. Notice the different types of data:
   - Text (names, descriptions)
   - Numbers (quantities, prices, IDs)
   - Dates (order dates)

### Confirm Your Data is Formatted as a Table

When you import data using Get Data, Excel usually creates a table automatically. You'll know it's a table if:
- The headers have filter dropdown arrows
- The rows have alternating colors (banding)
- The **Table Design** tab appears when you click in the data

If your data is NOT already a table:
1. Click anywhere in your data
2. Press **Ctrl + T** (or go to Insert → Table)
3. Make sure "My table has headers" is checked
4. Click **OK**

### Sort Your Data

1. Click the dropdown arrow in any column header
2. Choose **Sort A to Z** (ascending) or **Sort Z to A** (descending)
3. Try sorting products by ProductName, or orders by OrderDate

### Filter Your Data

1. Click the dropdown arrow in a column header
2. Uncheck items you want to hide, or use the search box to find specific values
3. Click **OK**
4. Notice the filter icon appears on filtered columns
5. To clear filters, click the arrow again and select **Clear Filter**

### Create a PivotTable for Quick Analysis

PivotTables are powerful tools for summarizing and exploring data.

**Example: Analyze the orders data**

1. Click anywhere in the orders table
2. Go to **Insert** → **PivotTable**
3. Ensure "Select a table or range" includes your entire data table
4. Choose **New Worksheet**
5. Click **OK**

You'll see the PivotTable Fields pane on the right. Try this:
- Drag a field like "OrderDate" to the **Rows** area
- Drag "LineTotal" to the **Values** area (it will sum the total order amounts)
- You've just created a summary showing the total order amounts by order date!

> **⚠️ Notice something strange about the dates?**  
> When you create a PivotTable with OrderDate in the Rows area, you might notice the dates appear in a format that looks strange or difficult to read. The dates might show as individual daily entries (like 1/1/2012, 1/28/2013, etc.) rather than being grouped nicely by month, quarter, or year.
> 
> **This is normal!** The dates need to be **transformed** before they work properly in analysis. We will learn how to clean and transform date data in a later step of this course. For now, just be aware that date columns often need special preparation before they're ready for analysis.

**Try more PivotTable examples:**

- Count of orders by customer
- Total order amounts by product

---

## Exploration Questions

Try to answer these questions using the tools you've learned:

### For Products:
- How many products do we have in total?
- How many different product categories or models do we have?
- What is the list price range of our products?

### For Orders:
- How many unique orders were placed?
- Which products appear most frequently in orders?
- What is the total value of all orders?

### Tips:
- Use **SUM**, **AVERAGE**, **COUNT** functions in a blank cell below your data
- Use PivotTables to group and summarize
- Apply filters to focus on specific segments

> 💡 **Need help?** Once you've tried these questions, you can check your answers in the [solution file](../00-solution/solution.md).

> 🚀 **Optional Challenge (Advanced)**  
> Try to answer this question using only Excel:
> - Which product category generates the highest total order value?
>
> Don't worry if you can't solve it yet – this will become easy later in the course.

---

## Important Note: Individual File Exploration

For now, you are exploring each CSV file **separately** and **independently**. 

You might notice that:
- The orders file has a ProductID
- The products file also has a ProductID
- You could potentially "connect" these files

**Don't worry about that yet!** In later steps, you will learn how to create relationships between tables and build data models. For now, focus on understanding what data you have in each file.

---

## Reflection (No Right or Wrong Answer)

- What questions about this data would you like to answer, but cannot yet?
- What information do you feel is missing?
- What feels difficult or unclear when exploring the data?

---

## What's Next?

Once you're comfortable exploring the data in Excel, you're ready to move on to the next step where you'll learn how to:
- Clean and transform data (including fixing those date formats!)
- Prepare data for analysis
- Handle missing or incorrect values

Return to the [main README](../../README.md) to continue to Step 2.

---

## Questions or Issues?

If you encounter any problems:
- Make sure you're using Microsoft Excel 2016 or newer
- Check that the CSV files downloaded correctly and are in the `data` folder
- Verify that your Excel has the **Get Data** option (if not, try **From Text** instead)

Happy exploring! 🎓📊
