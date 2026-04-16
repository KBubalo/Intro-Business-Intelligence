# Step 2: Prepare Data with Power Query

Welcome to the second exercise! In this step, you'll learn how to clean and transform data using Power Query in Excel, preparing it for meaningful analysis and reporting.

## What You'll Learn

- What ETL (Extract, Transform, Load) means and why it matters
- How to load data into Power Query (not just Excel)
- How to inspect and understand data quality issues
- How to fix data types, especially dates
- How to handle errors and invalid data
- How to rename columns for clarity
- How to prepare data for time-based analysis

## Prerequisites

- Microsoft Excel 2016 or newer (including Microsoft 365)
- Completed Exercise 01 (or basic familiarity with the orders.csv file)
- The **orders.csv** file from the `data` folder

---

## Goal of This Exercise

The goal is to understand that **raw data is rarely ready for analysis**. You will:

- Learn to think about data **quality** before analyzing it
- Use Power Query as a preparation tool (not just Excel's direct import)
- Fix common data issues that prevent good reporting
- Build a repeatable transformation process

This is not about creating reports yet—it's about making your data **report-ready**.

---

## What is ETL?

**ETL** stands for **Extract, Transform, Load**—getting data from a source, cleaning it, and loading it ready for analysis.

In this exercise, **Power Query** is your transformation engine. Instead of manually fixing data every time, you define the cleaning steps once, and Power Query reapplies them automatically when data refreshes.

---

## Getting Started

### Step 1: Load Data into Power Query

Instead of using **Get Data → Load**, we'll use **Get Data → Transform Data** to open Power Query.

1. Open a **new, blank Excel workbook**
2. Go to the **Data** tab
3. Click **Get Data** → **From File** → **From Text/CSV**
4. Navigate to the `data` folder
5. Select **orders.csv**
6. Click **Import**
7. In the preview window, **do NOT click Load**—instead, click **Transform Data**

**What just happened?**  
You opened the **Power Query Editor**, a separate window where you can see and modify the data before it lands in Excel.

---

## Understanding the Power Query Editor

The Power Query Editor has three main areas:

- **Left pane**: Your queries (you should see "orders")
- **Center**: Data preview
- **Right pane (Applied Steps)**: Every transformation you make is recorded here as a step

> 💡 **Key concept**: Steps are repeatable. When you refresh data, all steps run automatically.

---

## Step 2: Inspect and Fix Data Types

Look at the column headers. Each has an icon showing its data type:
- **ABC** = Text | **123** = Whole number | **1.2** = Decimal | **Calendar** = Date

**Check the OrderDate column**—it's likely Text or "Any" instead of Date. This is why dates don't work in PivotTables!

---

## Step 3: Fix the Date Column

Dates are tricky because different regions format them differently (MM/DD/YYYY vs DD/MM/YYYY). Let's fix the OrderDate column properly.

### First Attempt (You'll likely see an error - this is normal!)

1. Click the **OrderDate** column header
2. Go to **Transform** tab → **Data Type** → **Date** (not Date/Time)
3. Click **Replace current** in the popup

**What happened?** You probably see an error like:
```
DataFormat.Error: We couldn't parse the input provided as a Date value.
Details: 5/31/2011
```

This happens because Power Query doesn't know which date format your data uses. Is 5/31/2011 May 31st or March 5th (if your system expects DD/MM)?

### Fix the Error: Revert to Text First

Before we can apply the correct date format, we need to undo the error:

1. With the **OrderDate** column still selected, go to **Transform** tab
2. Click **Data Type** → **Text**
3. Click **Replace current** if prompted

**What happens?** The column reverts back to text (ABC icon), and the error disappears. The dates show as text again (e.g., "5/31/2011").

### Now Apply the Correct Date Format with Locale

Now let's tell Power Query the correct date format:

1. **Right-click** the **OrderDate** column header
2. Select **Change Type** → **Using Locale...**
3. In the dialog that appears:
   - **Data Type**: Select **Date**
   - **Locale**: Type or select **English (United States)** 
4. Click **OK**

**What happens now?** The dates should parse correctly! The icon changes to a calendar, and dates display consistently (e.g., `5/31/2011`).

> 💡 **Key lesson**: When working with dates, always check the source data format and use "Using Locale..." to avoid parsing errors. If you get an error, revert to Text first, then apply the correct locale.

**Why this matters:** Properly typed dates enable time-based analysis in PivotTables (grouping by month, quarter, year).

---

## Step 4: Investigate and Fix Errors (Don't Just Delete Them!)

You might notice the **DueDate** column has some error rows. Instead of deleting these rows and losing data, let's investigate and fix the problem.

> 💡 **Important principle**: In real projects, removing error rows means losing data. Always investigate first!

### A. Find the Error Rows

1. Look at the **DueDate** column in the data preview
2. **Scroll down** through the data to find rows that show **"Error"** in the DueDate column
3. You'll see several rows with errors (look for cells that display the word "Error" instead of a date)

**What you're looking for:** Rows where DueDate shows "Error" instead of a date value.

### B. Analyze the Error

1. **Click on one of the error cells** in the DueDate column
2. Look at the **formula bar** or the **error details** that appear at the bottom of the Power Query window

You'll see something like:
```
DataFormat.Error: We couldn't parse the input provided as a Date value.
Details:
    7/13/2011
```

**Notice the problem?** It's the same issue as OrderDate! The DueDate column has the same locale/date format problem. It needs to be converted with the correct locale setting.

> 💡 The error message tells us exactly what's wrong. Always read error details—they're helpful!

### C. Fix the Problem: Use Power Query Steps to Go Back and Fix It

Here's where Power Query's step-based approach becomes powerful! Instead of starting over, we can go back to an earlier step and fix the issue.

**Step 1: Go back to the "Changed Type" step**

1. Look at the **Applied Steps** pane on the right
2. Find and **click on** the step called **"Changed Type"** (one of the early steps)
3. The data preview will show how the data looked at that point

**What just happened?** You "time traveled" back to that transformation step!

**Step 2: Change DueDate back to Text**

1. With the **Changed Type** step selected, click the **DueDate** column header
2. Go to **Transform** tab → **Data Type** → **Text**
3. Select **Insert** on the popup window
4. Click **Replace current**

**Important:** You'll see a yellow warning banner at the top saying changes were made to a previous step. This is normal!

**Step 3: Go back to the latest step**

1. In the **Applied Steps** pane, click on the **last step** in the list (likely "Changed Type with Locale")
2. The data preview updates to show the current state

**What you'll notice:** The DueDate column is now Text (ABC icon), but the errors are gone because we fixed the root cause!

**Step 4: Apply the Date Format with Locale to DueDate**

Now let's convert DueDate to a proper date with the correct locale:

1. **Right-click** the **DueDate** column header
2. Select **Change Type** → **Using Locale...**
3. In the dialog:
   - **Data Type**: Select **Date**
   - **Locale**: Select **English (United States)**
4. Click **OK**

**Success!** The DueDate column should now be properly formatted as dates with no errors.

> 💡 **Key lesson about Power Query Steps**: You can go back to any step, modify it, and all subsequent steps automatically update. This makes it easy to fix issues without starting over. This is one of Power Query's most powerful features!

---

## Step 5: Rename Columns for Clarity

Make column names business-friendly:

1. **Right-click** a column header → **Rename**
2. Type a better name → Press **Enter**

**Suggested renames:**

| Original Column Name | New Column Name |
|---------------------|-----------------|
| `SalesOrderID` | `Order ID` |
| `SalesOrderDetailID` | `Order Detail ID` |
| `OrderDate` | `Order Date` |
| `DueDate` | `Due Date` |
| `ShipDate` | `Ship Date` |
| `EmployeeID` | `Employee ID` |
| `CustomerID` | `Customer ID` |
| `SubTotal` | `Sub Total` |
| `TaxAmt` | `Tax Amount` |
| `TotalDue` | `Total Due` |
| `ProductID` | `Product ID` |
| `OrderQty` | `Quantity` |
| `UnitPrice` | `Unit Price` |
| `UnitPriceDiscount` | `Unit Price Discount` |
| `LineTotal` | `Line Total` |

---

## Step 6: Verify Numeric Data Types

Quick check—make sure these are set correctly:
- **Quantity**: Whole Number
- **Unit Price**: Decimal Number
- **Line Total**: Decimal Number

To change: Click column header → **Transform** → **Data Type** → select type

---

## Step 7: Review Your Applied Steps

Look at the **Applied Steps** pane (right side). You should see steps like:
- **Source** - Your original CSV file
- **Promoted Headers** - First row became column headers
- **Changed Type** - Initial data type detection (modified to set DueDate as Text)
- **Changed Type with Locale** - OrderDate converted to Date with US locale
- **Changed Type with Locale1** - DueDate converted to Date with US locale
- **Renamed Columns** - Your column renames

**This is the power of Power Query**: These steps are saved and will automatically reapply when you refresh the data.

**Try it**: Click different steps to see how the data looked at that point. Notice how you can trace every transformation!

> 💡 **What you just learned**: You modified an earlier step (Changed Type), and Power Query automatically updated all the steps that came after it. This is called "step dependency" and it's one of the most powerful features of Power Query. You can always go back and refine your transformations without starting over!

---

## Step 8: Load the Cleaned Data to Excel

1. Click **Close & Load** (Home tab in Power Query)
2. Excel creates a new worksheet with your cleaned data as a Table

> 💡 This table is **connected** to the query. When the source CSV changes, you can refresh (**Data → Refresh All**) and all transformations reapply automatically.

---

## Step 9: Test Your Cleaned Data

**Quick test**: Create a PivotTable

1. Click in your table → **Insert** → **PivotTable**
2. Drag **OrderDate** to **Rows**
3. Drag **Line Total** to **Values**

**Expected result:** Dates should work properly! Excel may offer to group by months/quarters/years.

✅ **Success**: No more date formatting issues in PivotTables.

---

## Analysis Questions

Now that your data is clean and properly formatted, try to answer these questions using PivotTables:

### Question 1: Revenue by Year
**How much revenue did we generate in 2011, 2012, 2013, and 2014?**

**Hint:** Create a PivotTable with Order Date in Rows and Line Total in Values.

### Question 2: Best Month for Revenue
**In which month (combining all years) did we generate the most revenue and how much?**

**Hint:** Create a PivotTable with Order Date in Rows and Line Total in Values. Right-click on the dates → Group → Select Months only (uncheck Years). Sort by Line Total descending.

> 💡 **Notice how easy this is?** Because you properly formatted the dates in Power Query, Excel can now automatically group them by year, month, and quarter. This is why data preparation matters!

> 💡 **Need help?** Check the [solution file](../solution.md#exercise-02-prepare-data-with-power-query) for answers and step-by-step guidance.

---

## Reflection Questions

- What would happen if you loaded the CSV directly without Power Query transformations?
- Why is it valuable to have repeatable transformation steps?
- How did fixing data types (especially dates) improve the data's usability?
- Why is it better to investigate and fix errors rather than just removing error rows?
- If you received a new orders.csv file every month, how would Power Query help you?

>  **Optional Challenge (Advanced)**  
> Add calculated columns in Power Query to extract:
> - Year from OrderDate (Add Column → Date → Year)
> - Month Name from OrderDate (Add Column → Date → Month → Name of Month)
>
> These columns will make time-based analysis even easier later!

---

## Common Issues and Solutions

### "I don't see the Transform Data button"
- Make sure you're using Excel 2016 or newer
- Try clicking **Get Data** → **Launch Power Query Editor**

### "My dates still don't work in PivotTables"
- Double-check that the date columns are set to **Date** type with proper locale (not Text or DateTime)
- Make sure you used **Change Type → Using Locale...** with **English (United States)**
- Ensure you clicked **Close & Load** after changing the type

### "I see errors after changing data types"
- Don't immediately delete error rows! Investigate first:
  - Scroll through data to find rows showing "Error"
  - Click on an error to see details about what's wrong
  - Often errors are due to locale/date format issues - use "Change Type → Using Locale..."
  - You can go back to earlier steps in Applied Steps to fix the root cause
- Only remove errors if they truly can't be fixed

### "I get a yellow warning when modifying a step"
- This is normal when you edit an earlier step in Applied Steps
- The warning tells you that later steps might be affected
- Power Query will automatically update subsequent steps
- If something breaks, press Ctrl + Z to undo

### "Replace Values didn't work as expected"
- Make sure the column is Text type before using Replace Values
- Check that you typed the exact character to find (including spacing)
- The "Replace With" field can be left empty to remove characters

### "I accidentally deleted a step I needed"
- Press **Ctrl + Z** to undo
- Or click the X next to a later step in Applied Steps
- Or delete the entire query and start over (your source CSV is unchanged)

---

## What's Next?

You've now learned how to **prepare data** using Power Query. Your data is clean, well-typed, and ready for analysis.

In the next exercise, you will:
- Learn how to combine multiple tables (orders + products)
- Create relationships between data
- Build a simple data model

But for now, you've mastered the foundation: **ETL and data preparation**.

Return to the [main README](../../README.md) to continue to Step 3.

---

## Questions or Issues?

If you encounter problems:
- Make sure Power Query Editor is available in your Excel version
- Verify the CSV file path is correct
- Check that the data loaded successfully into Power Query before transforming

Remember: Power Query saves your steps, so you can always go back and modify or fix transformations.

Happy transforming! 🔄📊
