# Step 6: Extend Your Data Model

Welcome to the sixth exercise! In this workshop, you'll learn how to extend an existing data model by adding a new dimension table. You'll import product category data, create new relationships, and update your dashboard to use better, more descriptive category names.

## What You'll Learn

- How to add a new table to an existing Data Model without breaking what's already built
- How to import CSV files and load them into the Data Model using Power Query
- How to create relationships between new and existing tables
- How to update PivotTables and PivotCharts to use fields from the new dimension
- Why proper dimensional modeling makes reporting easier and more flexible
- How to verify that relationships are working correctly

## Prerequisites

- Microsoft Excel 2016 or newer (including Microsoft 365)
- Completed Exercises 03, 04, and 05
- An existing Excel workbook with:
  - A working Data Model (orders, products, customers, employees, Date)
  - A dashboard from Exercise 05 showing revenue by product categories
  - Relationships already established
- The **productcategories.csv** file from the `data` folder

**IMPORTANT:** You will continue working in your existing workbook from Exercise 05. Do not start a new file.

---

## Goal of This Exercise

The goal is to **extend your existing data model** by adding a new dimension table for product categories. Currently, your dashboard might show generic subcategory names. After this exercise, you'll have:

- A new **ProductCategories** dimension table in your Data Model
- A relationship connecting **Products** → **ProductCategories**
- An updated dashboard showing proper category names and descriptions
- A better understanding of how dimensional modeling makes reporting flexible

**Key principle:** Good data models grow and evolve. You should be able to add new dimensions without rebuilding everything from scratch.

**Estimated time:** 30-45 minutes

---

## The Business Problem

Right now, your dashboard shows product categories, but there's a problem:

**Current situation:**
- Your **products** table might have a **SubCategoryID** field (like 1, 2, 3) or generic category names
- You can see revenue by subcategory, but the names might not be descriptive
- If you want to add subcategory descriptions or group subcategories further, you'd have to change the products table

**The solution:**
- Create a separate **ProductSubCategories** dimension table
- Store all subcategory information (ID, Name, Description) in one place
- Link products to subcategories through a relationship
- Now you can update subcategory names in one place, and all reports automatically update

This is called **dimensional modeling**—separating descriptive attributes into dedicated dimension tables.

---

## SECTION 1: Understand the Current State

**⏱️ Estimated time: 5 minutes**

Before adding new tables, let's understand what we currently have.

### Step 1: Open Your Workbook and Review the Data Model

1. Open the Excel workbook you used in Exercise 05 (with the dashboard)
2. Go to the **Data** tab on the ribbon
3. Click **Manage Data Model** (or **Relationships** if you want a quick view)

This opens the Power Pivot window (or the Manage Relationships dialog).

### Step 2: Review Your Current Model

Look at the tables you already have:
- **orders** (fact table)
- **products** (dimension)
- **customers** (dimension)
- **employees** (dimension)
- **Date** (dimension)

Look at the **products** table specifically:
- Does it have a **SubCategoryID** column? (a number like 1, 2, 3)
- Does it have a **ProductSubCategory** column? (a text name)

**Current limitation:** All category information is embedded in the products table. If you want richer category data (like descriptions or groupings), you'd need to add columns to products, which can become messy.

> 💡 **Checkpoint:** You should see your existing Data Model with 5 tables. The products table has some category information, but it's limited.

---

## SECTION 2: Import the Product Categories Table

**⏱️ Estimated time: 10 minutes**

Now let's import the **productcategories.csv** file and load it into the Data Model.

### Step 1: Import the CSV File Using Power Query

1. Go back to your Excel worksheet (close Power Pivot if it's open)
2. Go to the **Data** tab on the ribbon
3. Click **Get Data** → **From File** → **From Text/CSV**
4. Navigate to the `data` folder in the repository
5. Select **productcategories.csv**
6. Click **Import**
7. A preview window will appear showing the data

**Review the preview:**
- You should see columns like:
  - **CategoryID** (a number: 1, 2, 3, ...)
  - **CategoryName** (text: "Electronics", "Home & Garden", ...)
  - **CategoryDescription** (optional, descriptive text)

### Step 2: Transform the Data (If Needed)

Before loading, let's make sure the data is clean.

1. In the preview window, click **Transform Data** (this opens Power Query Editor)
2. In Power Query, check the following:
   - **Data types:** Ensure **CategoryID** is set to **Whole Number** (not text)
   - **Data types:** Ensure **CategoryName** is set to **Text**
   - **Column headers:** Ensure the first row is used as headers (should be automatic)
3. (Optional) Remove any unnecessary columns (if any)
4. (Optional) Rename the query to **ProductCategories** (click on the query name in the Queries pane on the left)
5. In Power Query Editor, go to the **Home** tab
6. Click **Close & Load**

### Step 3: Load the Table to the Data Model

**CRITICAL STEP:** You must load this table to the Data Model, not just to a worksheet.

1. In the Ribbon, select **Data** → **Data Model** drop down → **Relationships**
2. Create a New relationship
3. Select Productsubcategories as Table and SubCategoryID as Column (Primary Key)
4. Select Products as Related Table and SubCategoryID as Column (Foreign Key)
5. Confirm with **OK**
6. **Close** the Manage Relationships dialog

> 💡 **Understanding the relationship:** This creates a link where each product's **SubCategoryID** points to a matching **SubCategoryID** in the ProductSubCategories table. Now when you use SubCategoryName from ProductSubCategories in a PivotTable, Excel knows how to connect it to your orders data through the products table.

### Step 3: Verify the Relationship in Diagram View (Optional)

If you want to see the relationship visually:

1. Go to **Data** tab → **Manage Data Model**
2. In Power Pivot, go to **Home** tab → **Diagram View**
3. You should see your tables as boxes with lines connecting them
4. Look for the line connecting **products.SubCategoryID** → **ProductSubCategories.SubCategoryID**

The line should show:
- **\* (asterisk)** on the products side (many)
- **1** on the ProductSubCategories side (one)

This confirms the **Many-to-One** relationship.

> 💡 **Checkpoint:** You have a new relationship connecting products to ProductSubCategories. When you use SubCategoryName from ProductSubCategories in a report, Excel will automatically connect it to your orders data.

---

## SECTION 4: Update Your Dashboard

**⏱️ Estimated time: 10-15 minutes**

Now let's update your dashboard from Exercise 05 to use the new, better category names from the ProductCategories table.

### Step 1: Navigate to Your Dashboard

1. Go to the **Dashboard** worksheet you created in Exercise 05
2. Locate the bar chart showing **Revenue by Model Name**

### Step 2: Update the Product Ranking Chart

Currently, this chart might be using **Model Name** from the products table. Let's change it to use **Sub Category Name** from the ProductSubCategories table.

1. Click on your product ranking bar chart to select it
2. The **PivotChart Fields** pane should appear on the right
3. In the **Axis (Categories)** area at the bottom:
   - **Remove** the current field (e.g., drag **Model Name** out of the Axis area, or click the X)
4. Now add the new field:
   - Expand the **ProductSubCategories** table in the field list
   - **Drag** the **SubCategoryName** field to the **Axis (Categories)** area
5. The chart will update to show the subcategory names from the ProductSubCategories table

**You should immediately see better, more descriptive category names!**

### Step 3: Verify the Chart Still Sorts Correctly

1. Right-click on any category name in the chart
2. Select **Sort** → **More Sorting Options...** → **Sort Largest to Smallest**
3. Select Ascending (A to Z) by **Sum of Revenue**
4. Confirm with **OK**

The chart should still rank categories by revenue, from highest to lowest.

### Step 4: Update Chart Titles (If Needed)

Since you now have better category names, you might want to update your chart title to reflect the actual categories:

1. Click on the chart title
2. Update it to be more specific (e.g., **"Electronics and Home & Garden Lead Revenue"** becomes more accurate if those are the actual category names)

> 💡 **Checkpoint:** Your dashboard should now show subcategory names from the ProductSubCategories dimension table. The chart should still sort and filter correctly, but with better labels.

---

## SECTION 5: Test the Model with Slicers

**⏱️ Estimated time: 5 minutes**

Let's verify that your relationships are working correctly by testing with slicers.

### Step 1: Add a SubCategory Slicer (If You Don't Have One)

1. Click on any PivotChart in your dashboard
2. Go to **PivotChart Analyze** tab → **Insert Slicer**
3. In the dialog box, expand the **ProductSubCategories** table
4. Check the box next to **SubCategoryName**
5. Click **OK**
6. Position the slicer somewhere convenient on your dashboard

### Step 2: Connect the Slicer to All Visuals

1. Right-click on the new slicer
2. Select **Report Connections**
3. Check all boxes to connect the slicer to all PivotTables and PivotCharts
4. Click **OK**

### Step 3: Test the Slicer

1. Click on one category in the slicer (e.g., "Electronics")
2. Watch your dashboard update:
   - The KPI cards (Total Revenue, Number of Orders) should filter to show only that category
   - The time trend chart should show revenue over time for that category only
   - The product ranking chart might show just that one category (or you can add product names to see products within that category)
3. Click the slicer again to deselect (or click **Clear Filter**)

**If the dashboard filters correctly, your relationships are working!**

> 💡 **What's happening behind the scenes:** When you filter by SubCategoryName in ProductSubCategories, Excel follows the relationship chain: ProductSubCategories → products → orders. This filters the orders data to show only orders for products in the selected subcategory.

> 💡 **Checkpoint:** Your subcategory slicer should filter all visuals on your dashboard. Revenue, orders, and trends should all update based on the selected subcategory.

---

## SECTION 6: Key Takeaways and Best Practices

Before you finish this exercise, reflect on these core lessons:

### 1. Data Models Are Living Systems

- Models evolve as business needs change
- You should be able to add new tables and relationships without breaking existing reports
- Design for flexibility from the start

### 2. Dimensional Modeling Makes Reporting Easier

- **Fact tables** (orders) store measurements
- **Dimension tables** (products, subcategories, categories, customers) store descriptive attributes
- Relationships connect them, enabling flexible analysis

**The pattern:**
```
Orders (Fact)
  └─ ProductID → Products (Dimension)
                    └─ SubCategoryID → ProductSubCategories (Dimension)
                                        └─ CategoryID → ProductCategories (Dimension)
```

This is called a **snowflake schema** (a variation of star schema with normalized dimensions).

### 3. Relationships Are the Foundation

- **Many-to-One** is the most common relationship type
  - Many orders → One product
  - Many products → One category
- **Primary Keys** (CategoryID in ProductCategories) must be unique
- **Foreign Keys** (CategoryID in products) can repeat

### 4. Load Dimension Tables to the Data Model

- Always use **"Only Create Connection"** + **"Add this data to the Data Model"**
- This keeps your workbook clean
- Tables are available in PivotTables without cluttering worksheets

### 5. Test After Every Change

- After adding a relationship, test it with a simple PivotTable or slicer
- Verify that filtering works as expected
- If numbers look wrong, check your relationship cardinality

---

## Bonus Challenge (Optional)

If you have extra time, try these advanced exercises:

### Challenge 1: Add Product Categories

The repository includes a **productcategories.csv** file. Can you:
1. Import it into the Data Model
2. Create relationships: Products → Subcategories → Categories
3. Update your dashboard to show revenue by category

### Challenge 2: Add Category Descriptions as Tooltips

Can you:
1. Add a **CategoryDescription** field to your ProductCategories table (if it exists)
2. Show this description as a tooltip when hovering over bars in your chart
3. Hint: Look for "Tooltips" or "Data Labels" options in chart formatting

## Congratulations!

You've extended your data model by adding a new dimension table! 🎉

You've learned that:
- Data models can grow and evolve without breaking existing work
- Dimensional modeling (separating descriptive attributes into dimensions) makes reporting flexible
- Relationships are the glue that connects your data
- Good design makes maintenance easier and reporting more powerful

---

## What's Next?

Congratulations on completing all 6 exercises! 🎓

You've built a solid foundation in business intelligence:
- ✅ Data exploration and import
- ✅ Data cleaning with Power Query (ETL)
- ✅ Star Schema data modeling
- ✅ Visualization best practices
- ✅ Dashboard building
- ✅ Extending and evolving data models

### Continue Your Learning Journey:

**Next steps in Excel:**
- Learn DAX (Data Analysis Expressions) for calculated measures
- Explore Power Pivot advanced features
- Build hierarchies for drill-down analysis
- Practice with more complex business scenarios

**Expand to Power BI:**
- Everything you learned applies to Power BI Desktop
- More powerful visualizations and interactivity
- Cloud-based sharing and collaboration
- Advanced analytics and AI features

**Practice with real data:**
- Find public datasets (Kaggle, government open data)
- Apply these techniques to your own work
- Build a portfolio of dashboards
- Challenge yourself with new business questions

[Return to main README](../../README.md) to review all exercises.

---

**You've completed all 6 exercises!** You now have practical business intelligence skills. Keep building, keep learning! 📊✨🚀
