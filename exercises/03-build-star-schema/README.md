# Step 3: Build a Star Schema Data Model

Welcome to the third exercise! In this workshop, you'll learn how to build a proper data model using the Star Schema approach. You'll transform multiple tables, create relationships, and see how a well-designed data model makes analysis much easier.

## What You'll Learn

- How to prepare dimension tables (products, customers, employees) in Power Query
- How to identify and prepare a fact table (orders)
- How to create a Date dimension for time-based analysis
- How to build relationships between tables
- How to test your data model with PivotTables
- Why Star Schema matters for business intelligence

## Prerequisites

- Microsoft Excel 2016 or newer (including Microsoft 365)
- Completed Exercise 02 (Power Query basics)
- The following CSV files from the `data` folder:
  - **orders.csv** (fact table)
  - **products.csv** (dimension)
  - **customers.csv** (dimension)
  - **employees.csv** (dimension)

---

## Goal of This Workshop

The goal is to move from working with individual tables to building a **complete data model**. You will:

- Understand the difference between **fact tables** (transactions) and **dimension tables** (descriptive data)
- Prepare multiple tables so they work together
- Create relationships that enable powerful analysis
- Build a Date dimension for time intelligence
- Experience how a proper data model simplifies reporting

**Estimated time:** 75-90 minutes

---

## What is a Star Schema?

A **Star Schema** is a data modeling approach where:

- **One central fact table** contains measurable events (like orders, sales, transactions)
- **Multiple dimension tables** surround the fact table and provide context (who, what, when, where)
- **Relationships** connect the fact table to dimensions via keys (IDs)

**Why Star Schema?**
- Makes analysis faster and easier
- Simplifies PivotTables and reports
- Separates "what happened" from "who/what/when/where"
- Standard approach in business intelligence

---

## SECTION 1: Understanding Your Starting Point

### The Tables You'll Work With

Before we start transforming data, let's understand what each table represents:

| Table | Role | Purpose |
|-------|------|---------|
| **orders** | Fact Table | Contains transaction data - WHAT HAPPENED (sales events, quantities, amounts) |
| **products** | Dimension | Describes products - WHAT was sold (product names, categories, prices) |
| **customers** | Dimension | Describes customers - WHO bought (customer names, locations) |
| **employees** | Dimension | Describes employees - WHO sold (employee names, titles) |

### Fact vs. Dimension Tables

**Fact Table (orders):**
- Contains **measurements** or **metrics** (quantities, prices, totals)
- Contains **foreign keys** that reference dimensions (ProductID, CustomerID, EmployeeID)
- Typically has many rows (grows over time)
- Answers "What happened?"

**Dimension Tables (products, customers, employees):**
- Contains **descriptive attributes** (names, categories, descriptions)
- Has a **primary key** (ProductID, CustomerID, EmployeeID)
- Typically has fewer rows (relatively stable)
- Answers "Who, What, When, Where?"

> 💡 **Think of it like this:** The fact table is your bank transactions (amounts, dates), and dimensions are your categories (groceries, utilities) and merchants (store names, locations).

---

## SECTION 2: Prepare Dimension Tables

We'll start by preparing the dimension tables. These describe the "context" around your transactions.

### Why Prepare Dimensions First?

- Dimensions are usually smaller and simpler
- You'll reference them from the fact table
- It's easier to test relationships when dimensions are ready first

---

## Step 1: Load and Prepare the Products Dimension

Products describe **what** was sold.

### Load Products into Power Query

1. Use the existing **Excel workbook** with orders table already transformed
2. Go to **Data** tab → **Get Data** → **From File** → **From Text/CSV**
3. Select **products.csv**
4. In the preview window, click **Transform Data** (NOT Load)

### Inspect the Data

Look at the products data in Power Query. You should see columns like:
- ProductID
- ProductName
- ProductNumber
- Color
- StandardCost
- ListPrice
- ProductCategoryID
- ProductSubcategoryID
- Model

**Question to consider:** What is the primary key? (The unique identifier for each product)

> ✅ **Answer:** ProductID - each product has a unique ID.

### Fix Data Types

Check the data type icons on each column header:

1. **ProductID**: Should be **Whole Number**
2. **ProductNumber**: Should be **Text**
3. **ProductName**: Should be **Text**
4. **ModelName**: Should be **Text**
5. **MakeFlag**: Should be **Whole Number**
6. **StandardCost**: Should be **Currency**
7. **ListPrice**: Should be **Currency**
8. **SubCategoryID**: Should be **Whole Number**

**To change data types:** Click column header → Transform tab → Data Type → select correct type

### Rename Columns for Clarity

Make column names user-friendly by adding spaces:

| Original | New Name |
|----------|----------|
| `ProductID` | `Product ID` |
| `ProductNumber` | `Product Number` |
| `ProductName` | `Product Name` |
| `ModelName` | `Model Name` |
| `MakeFlag` | `Make Flag` |
| `StandardCost` | `Standard Cost` |
| `ListPrice` | `List Price` |
| `SubCategoryID` | `SubCategory ID` |

> 💡 **Tip:** Right-click column header → Rename or double click on the name

### Remove Unnecessary Columns (Optional)

If there are columns you don't need for analysis (like internal codes or technical fields), you can remove them:
- Right-click column header → **Remove**

**For this exercise, keep all columns** - they might be useful later.

### Rename the Query

Before loading, give your query a clear name:

1. In the **Query Settings** pane (right side), find **Properties** → **Name**
2. Change "products" to **"Products"**
3. Rename the "orders" table to **Orders**

> 💡 **Why?** Clear query names make your data model easier to understand.

### Load to Excel

1. Click **Close & Load** (Home tab)
2. Power Query creates a new worksheet with the Products table

**Checkpoint:** You should now have a worksheet named "Products" with clean, user-friendly column names.

---

## Step 1a: Discover the Problem (No Relationships Yet!)

Before we continue loading more tables, let's see what happens when we try to analyze data from multiple tables WITHOUT relationships.

### Create a PivotTable from Products

You now have two tables:
- **Orders** (from Exercise 02)
- **Products** (just loaded)

Let's try to answer a simple question: **How many products does each order contain?**

1. Click anywhere in the **Products** table
2. Go to **Insert** tab → **PivotTable**
3. In the dialog:
   - Table/Range should show **Products**
   - Select **New Worksheet**
   - **Do NOT check** "Add this data to the Data Model" (not yet!)
4. Click **OK**

You now have a PivotTable based on the Products table.

### Add the Orders Table to the Analysis

In the PivotTable Fields pane (right side), you should see:
- Fields from the **Products** table (Product ID, Product Name, etc.)
- At the bottom: **"More Tables..."** link

Now let's add the Orders table:

1. Click **"More Tables..."** at the bottom of the PivotTable Fields pane
2. A dialog appears asking to create a new Pivot Table - confirm by clicking Yes
3. A new worksheet has opened with a new Pivot Table and two tables now - **Orders** and **Products**

### Build the Analysis

Now let's count products per order:

1. Expand the **Products** table
2. Drag **Product Name** to the **Rows** area
3. Expand the **Orders** table
4. Drag **Sales Order ID** to the **Values** area
5. Change the aggregation to **Count**

### What Do You See? 🤔

Look at the PivotTable results. **Every product shows 60919 orders!**

**Is this correct?** No! It's unlikely that each product has exactly 60919 orders.

### Why Is This Happening?

Look at the yellow warning message at the top of the PivotTable Fields pane:

> ⚠️ **"Relationships between tables may be needed."**

**What's going on:**
- Excel doesn't know how Orders and Products connect
- Without a relationship, Excel creates a **Cartesian product** (every order × every product)
- Since there are 60919 orders in the Orders table, every product appears to have 60919 orders
- This is completely wrong!

> 💡 **This is the core problem that relationships solve.** Excel needs to know: "When Order ID 43659 has Product ID 712, look up Product ID 712 in the Products table."

### Create the First Relationship

Let's fix this by creating a model and a relationship:

1. Select **CREATE...** in the warning message on top of the PivotTable Fields Property section
   1. Alternatively, you can go to the Ribbon and select **Data** → **Data Model** → **Manage Data Model**
   2. If asked to enable Data Analysis add-ins, hit **Enable**
   3. Select **Design** in the Ribbon, click on **Create Relationships**
2. In the **Create Relationship** dialog:
   - **Table**: Select **Orders**
   - **Column (Foreign)**: Select **Product ID**
   - **Related Table**: Select **Products**
   - **Related Column (Primary)**: Select **Product ID**
3. Click **OK**

**What you just did:** You told Excel that the Product ID in Orders matches the Product ID in Products.

### Test the Fix

In your existing PivotTable, the numbers should automatically update. If not, refresh the PivotTable (right-click → Refresh).

**What changed?** The counts should now be realistic! Each product now shows the actual number of orders it appears in (between 2 and 1192 orders per product is right, not 60919!).

> ✅ **Success!** The relationship fixed the analysis. Now Excel knows how to correctly connect the two tables.

### Understanding What Just Happened

**Before the relationship:**
- Excel didn't know Product ID in Orders connects to Product ID in Products
- Result: Every order matched with every product (Cartesian product)
- Analysis was meaningless

**After the relationship:**
- Excel uses Product ID as the connection
- Result: Each product only matches its actual orders
- Analysis is correct!

**This is why data modeling matters.** Without proper relationships, your analysis will be wrong.

---

## Step 2: Load and Prepare the Customers Dimension

Customers describe **who** bought the products.

### Load Customers into Power Query

1. Go to **Data** tab → **Get Data** → **From File** → **From Text/CSV**
2. Select **customers.csv**
3. Click **Transform Data**

### Inspect the Data

Look at the customers data. You should see columns like:
- CustomerID
- FirstName
- LastName
- FullName

**Primary key:** CustomerID

### Fix Data Types

1. **CustomerID**: Should be **Whole Number**
2. **FirstName**: Should be **Text**
3. **LastName**: Should be **Text**
4. **FullName**: Should be **Text**

### Rename Columns

Split CamelCase names into readable names:

| Original | New Name |
|----------|----------|
| `CustomerID` | `Customer ID` |
| `FirstName` | `First Name` |
| `LastName` | `Last Name` |
| `FullName` | `Full Name` |

### Rename the Query and Load

1. In **Query Settings**, change the name to **"Customers"**
2. Click **Close & Load**

**Checkpoint:** You now have a Customers worksheet with a clean customer dimension table.

---

## Step 3: Load and Prepare the Employees Dimension

Employees describe **who** sold the products (the sales team).

### Load Employees into Power Query

1. **Data** tab → **Get Data** → **From File** → **From Text/CSV**
2. Select **employees.csv**
3. Click **Transform Data**

### Inspect the Data

You should see columns like:
- EmployeeID
- ManagerID
- FirstName
- LastName
- FullName
- JobTitle
- OrganizationLevel
- MaritalStatus
- Gender
- Territory
- Country
- Group

**Primary key:** EmployeeID

### Fix Data Types

1. **EmployeeID**: **Whole Number**
2. **ManagerID**: **Whole Number**
3. **FirstName**: **Text**
4. **LastName**: **Text**
5. **FullName**: **Text**
6. **JobTitle**: **Text**
7. **OrganizationLevel**: **Whole Number**
8. **MaritalStatus**: **Text**
9. **Gender**: **Text**
10. **Territory**: **Text**
11. **Country**: **Text**
12. **Group**: **Text**

### Rename Columns for Clarity

Add spaces to make column names more readable:

| Original | New Name |
|----------|----------|
| `EmployeeID` | `Employee ID` |
| `ManagerID` | `Manager ID` |
| `FirstName` | `First Name` |
| `LastName` | `Last Name` |
| `FullName` | `Full Name` |
| `JobTitle` | `Job Title` |
| `OrganizationLevel` | `Organization Level` |
| `MaritalStatus` | `Marital Status` |

> 💡 **Note:** Keep Gender, Territory, Country, and Group as single words (no renaming needed).

### Rename Query and Load

1. In the **Properties** panel (right side), change the **Name** field to **"Employees"**
2. **Close & Load**

**Checkpoint:** You now have three dimension tables loaded: Products, Customers, and Employees.

---

## SECTION 3: Review the Fact Table (Orders)

The **orders table** is your fact table - it contains the actual transactions/events.

### What Makes It a Fact Table?

- Contains **measurable values** (quantities, prices, totals)
- Contains **foreign keys** that link to dimensions (ProductID, CustomerID, EmployeeID)
- Many rows (one per order line item)
- Grows over time as new orders come in

### Review the Orders Query

You already loaded and transformed the Orders table in Exercise 02. Let's review it:

1. Go to **Data** tab → **Queries & Connections**
2. In the pane that appears, you should see your **Orders** query
3. Right-click **Orders** → **Edit**

This opens Power Query Editor with your existing orders query.

> 💡 **Remember:** You already cleaned this data in Exercise 02 (fixed date types, renamed columns, handled errors).

### Inspect the Orders Data

You should see columns like:
- SalesOrderID
- SalesOrderDetailID
- OrderDate
- DueDate
- ShipDate
- EmployeeID
- CustomerID
- ProductID
- OrderQty
- UnitPrice
- UnitPriceDiscount
- Revenue (or Line Total, depending on your naming)

### Identify the Keys (Important!)

Look at the ID columns:
- **SalesOrderID + SalesOrderDetailID**: Composite primary key (uniquely identifies each line item)
- **EmployeeID**: Foreign key → links to Employees dimension
- **CustomerID**: Foreign key → links to Customers dimension
- **ProductID**: Foreign key → links to Products dimension

> 💡 **This is how the star schema connects!** These foreign keys will become relationships.

### Verify Data Types

Make sure all columns have correct data types (you should have done this in Exercise 02, but let's verify):

1. **SalesOrderID** (or **Order ID** if already renamed): **Whole Number**
2. **SalesOrderDetailID** (or **Order Detail ID**): **Whole Number**
3. **OrderDate** (or **Order Date**): **Date**
4. **DueDate** (or **Due Date**): **Date**
5. **ShipDate** (or **Ship Date**): **Date**
6. **EmployeeID** (or **Employee ID**): **Whole Number**
7. **CustomerID** (or **Customer ID**): **Whole Number**
8. **ProductID** (or **Product ID**): **Whole Number**
9. **OrderQty** (or **Quantity**): **Whole Number**
10. **UnitPrice** (or **Unit Price**): **Decimal Number**
11. **UnitPriceDiscount** (or **Unit Price Discount**): **Decimal Number**
12. **Revenue** (or **Line Total**): **Decimal Number**

> ✅ **If everything looks good from Exercise 02, you don't need to make changes.**

### Verify Column Names

If you haven't already renamed columns in Exercise 02, make sure they match the friendly names from the table above (with spaces).

### Close Power Query

1. If you made any changes, click **Close & Apply** (Home tab)
2. If no changes were needed, click **Close**

**Checkpoint:** You now have all four tables loaded: Orders (fact), Products, Customers, and Employees (dimensions).

---

## SECTION 4: Create a Date Dimension

A **Date dimension** is a special dimension table that contains one row for each date. It enables powerful time-based analysis.

### Why Do You Need a Date Dimension?

**🚨 Critical Problem: Missing Dates in Reports!**

If you only use the OrderDate field from the Orders table, you have a major issue:
- **You can only see dates where orders exist**
- **Days without orders are completely missing from your reports**
- If no one ordered on January 15th → January 15th doesn't appear in your analysis
- Your time-series charts have gaps and look incomplete
- You can't see "zero sales days" which are important for business insights!

**Example:**
- If you create a report showing "Daily Sales", you'll only see the 60 days that had orders
- The other 305 days of the year? **Missing!** Your boss will ask: "Where's the rest of the year?"

This is why we need a **Date dimension** - a complete table with ALL dates (every single day), whether orders happened or not.

**Without a Date dimension:**
- You can only analyze by dates in the Orders table (incomplete!)
- Limited to basic grouping (year, month)
- Hard to create fiscal year analysis
- Can't easily compare periods
- **Missing dates = incomplete reports**

**With a Date dimension:**
- Every date appears in your reports (complete coverage!)
- Pre-calculated attributes (Year, Quarter, Month Name, Day of Week)
- Easy fiscal year analysis
- Consistent date hierarchies
- Better performance
- Days with zero sales show up correctly

### Create the Date Table Using Power Query

We'll create a Date table using M code (you don't need to understand every line - just follow along).

1. Go to **Data** tab → **Get Data** → **From Other Sources** → **Blank Query**
2. A new blank query opens in Power Query Editor
3. Go to **View** tab → **Advanced Editor**
4. **Delete** all existing text
5. **Copy and paste** this code:

```m
let
    StartDate = #date(2011, 1, 1),
    EndDate = #date(2014, 12, 31),
    NumberOfDays = Duration.Days(EndDate - StartDate) + 1,
    DateList = List.Dates(StartDate, NumberOfDays, #duration(1,0,0,0)),
    DateTable = Table.FromList(DateList, Splitter.SplitByNothing(), {"Date"}),
    ChangedType = Table.TransformColumnTypes(DateTable,{{"Date", type date}}),
    
    // Add Year
    AddYear = Table.AddColumn(ChangedType, "Year", each Date.Year([Date]), Int64.Type),
    
    // Add Quarter
    AddQuarter = Table.AddColumn(AddYear, "Quarter", each "Q" & Text.From(Date.QuarterOfYear([Date])), type text),
    
    // Add Month Number
    AddMonthNum = Table.AddColumn(AddQuarter, "Month Number", each Date.Month([Date]), Int64.Type),
    
    // Add Month Name
    AddMonthName = Table.AddColumn(AddMonthNum, "Month Name", each Date.MonthName([Date]), type text),
    
    // Add Day
    AddDay = Table.AddColumn(AddMonthName, "Day", each Date.Day([Date]), Int64.Type),
    
    // Add Day of Week
    AddDayOfWeek = Table.AddColumn(AddDay, "Day of Week", each Date.DayOfWeekName([Date]), type text),
    
    // Add Year-Month for sorting
    AddYearMonth = Table.AddColumn(AddDayOfWeek, "Year-Month", each Date.ToText([Date], "yyyy-MM"), type text)
in
    AddYearMonth
```

6. Click **Done**
7. **What just happened?** Power Query created a table with one row for each date from 2011 to 2014, with helpful columns.

### Inspect the Date Table

Look at the columns that were created:
- **Date**: The actual date (primary key)
- **Year**: e.g., 2011, 2012, 2013, 2014
- **Quarter**: e.g., Q1, Q2, Q3, Q4
- **Month Number**: e.g., 1, 2, 3...12
- **Month Name**: e.g., January, February
- **Day**: e.g., 1, 2, 3...31
- **Day of Week**: e.g., Monday, Tuesday
- **Year-Month**: e.g., 2011-01, 2011-02

> 💡 **This is powerful!** Now you can slice and dice your orders by any time attribute.

### Rename Query and Load

1. Change query name to **"Date"**
2. **Close & Load**

**Checkpoint:** You now have five tables: Orders (fact), Products, Customers, Employees, Date (dimensions).

---

## SECTION 5: Complete the Star Schema Relationships

You already created one relationship in Step 1a (Orders → Products). Now let's create the remaining relationships to complete the star schema.

### Recap: Why We Need Relationships

Remember from Step 1a:
- Without relationships, Excel creates a Cartesian product (every order × every product)
- Relationships tell Excel how to correctly connect tables
- Foreign keys in the fact table (Orders) link to primary keys in dimensions

Now we'll create relationships for Customers, Employees, and the Date dimension.

### Review: The Product Relationship (Already Created)

In Step 1a, you already created:
- **Orders.Product ID** → **Products.Product ID**

✅ This relationship is complete. No need to create it again.

### Create the Customer Relationship

1. Go to **Data** tab → **Data Model** → **Relationships**
2. Click **New** to create a new relationship
3. In the dialog:
   - **Table**: Select **Orders**
   - **Column**: Select **Customer ID**
   - **Related Table**: Select **Customers**
   - **Related Column**: Select **Customer ID**
4. Click **OK**

**What you created:** A link from Orders.Customer ID → Customers.Customer ID

### Create the Employee Relationship

1. Click **New** again
2. Settings:
   - **Table**: **Orders**
   - **Column**: **Employee ID**
   - **Related Table**: **Employees**
   - **Related Column**: **Employee ID**
3. Click **OK**

**What you created:** A link from Orders.Employee ID → Employees.Employee ID

### Create the Date Relationship

1. Click **New**
2. Settings:
   - **Table**: **Orders**
   - **Column**: **Order Date**
   - **Related Table**: **Date**
   - **Related Column**: **Date**
3. Click **OK**

**Checkpoint:** You should now have 4 relationships:
- Orders → Products (via Product ID)
- Orders → Customers (via Customer ID)
- Orders → Employees (via Employee ID)
- Orders → Date (via Order Date / Date)

### View Your Star Schema (Optional)

If Excel supports Diagram View:
1. Go to **Power Pivot** → **Manage** → **Diagram View**
2. You should see Orders in the center with lines connecting to the four dimensions

**This is your Star Schema!** ⭐

---

## SECTION 6: Test Your Data Model

Now let's see the power of a properly modeled star schema.

### Create a PivotTable

1. Go to **Insert** tab → **PivotTable**
2. **Important:** Select **Use this workbook's Data Model**
3. Click **OK**

**What's different?** Now you see ALL tables in the field list!

### Analysis 1: Sales by Product

Let's see which products generate the most revenue:

1. Expand the **Products** table in the field list
2. Drag **Product Name** to **Rows**
3. Expand the **Orders** table
4. Drag **Revenue** to **Values**

**What you see:** Total sales for each product!

> 💡 **This works because:** Excel uses the relationship to match Product IDs and look up product names.

### Analysis 2: Sales by Customer

1. Create a new PivotTable (Insert → PivotTable → Use Data Model)
2. Drag **Customer Name** (from Customers) to **Rows**
3. Drag **Revenue** (from Orders) to **Values**

**What you see:** Total sales per customer!

### Analysis 3: Sales Over Time

Let's use the Date dimension:

1. Create a new PivotTable
2. Drag **Year** (from Date) to **Rows**
3. Drag **Quarter** (from Date) below Year in Rows
4. Drag **Month Name** (from Date) below Quarter
5. Drag **Revenue** (from Orders) to **Values**

**What you see:** A beautiful time hierarchy showing sales by year, quarter, and month!

> 💡 **This is the power of the Date dimension** - you can slice time any way you want.

### Analysis 4: Sales by Employee

Who are your top sales performers?

1. Create a new PivotTable
2. Drag **Employee Name** (from Employees) to **Rows**
3. Drag **Revenue** (from Orders) to **Values**
4. Right-click any value → **Sort** → **Largest to Smallest**

**What you see:** Sales performance by employee!

### Challenge: Combine Multiple Dimensions

Try this advanced analysis:

1. Create a new PivotTable
2. Drag **Year** (from Date) to **Columns**
3. Drag **Product Name** (from Products) to **Rows**
4. Drag **Revenue** (from Orders) to **Values**

**What you see:** A matrix showing product sales across years!

---

## Analysis Questions

Test your new data model by answering these questions:

### Question 1: Top 5 Products by Revenue
Which 5 products generated the most revenue overall?

**Hint:** PivotTable with Product Name and Revenue, sorted descending.

<details>
<summary><b>Click to see answer</b></summary>

| Product Name | Total Revenue |
|--------------|---------------|
| Mountain-200 Black, 38 | $3,105,726.66 |
| Mountain-200 Black, 42 | $2,646,352.67 |
| Mountain-200 Silver, 38 | $2,354,215.24 |
| Mountain-200 Silver, 42 | $2,181,044.29 |
| Mountain-200 Silver, 46 | $2,133,156.84 |

</details>

### Question 2: Sales by Quarter
How much revenue did we generate in each quarter of 2013?

**Hint:** Use Year and Quarter from the Date dimension. Filter to Year = 2013.

<details>
<summary><b>Click to see answer</b></summary>

| Quarter | Revenue |
|---------|----------|
| Q1 | $6,309,986.20 |
| Q2 | $8,876,224.19 |
| Q3 | $9,820,157.70 |
| Q4 | $7,883,983.64 |

**Total 2013:** $32,890,351.73

</details>

### Question 3: Top Customer
Which customer spent the most money across all years?

**Hint:** PivotTable with Customer Name and Revenue.

<details>
<summary><b>Click to see answer</b></summary>

**Roger Harui** is the top customer across all years.

</details>

### Question 4: Top Sales Employee
Which employee sold the most in 2014?

**Hint:** PivotTable with Employee Full Name and Revenue. Filter to Year = 2014.

<details>
<summary><b>Click to see answer</b></summary>

**Jae Pak** with $1,382,996.58 in sales for 2014.

</details>

---

## Reflection Questions

Take a moment to think about what you learned:

- What's the difference between a fact table and a dimension table?
- Why did we create relationships? What would happen without them?
- How does the Star Schema make analysis easier compared to working with flat files?
- Why did we create a separate Date dimension instead of just using Order Date?

---

## Common Issues and Solutions

### "I can't see all tables in my PivotTable"
- Make sure you selected **Use this workbook's Data Model** when creating the PivotTable
- Check that all tables loaded successfully (Data → Queries & Connections)

### "Relationships aren't working"
- Verify that the data types match (e.g., both sides are Whole Number or both are Date)
- Check that column names are exactly the same (including spaces)
- Ensure there are no null values in key columns

### "Date table doesn't show up in PivotTable"
- Make sure you created the relationship between Orders.Order Date and Date.Date
- Verify the Date table loaded (it should have 1,461 rows for 2011-2014)

### "Power Query is running slowly"
- This is normal with larger datasets
- Consider closing unused queries
- Only load tables you need for analysis

### "I made a mistake in Power Query"
- Go to Data → Queries & Connections
- Right-click the query → Edit
- Fix the issue in Power Query Editor
- Close & Load to refresh

---

## What's Next?

You've built a complete Star Schema data model! 🎉

You now understand:
- How to prepare fact and dimension tables
- How to create relationships
- How the Star Schema enables powerful analysis
- How to use the Data Model in PivotTables

For now, you've mastered the foundation: **the Star Schema**.

---

## Questions or Issues?

If you encounter problems:
- Check that all CSV files are in the correct location
- Verify that Power Query queries loaded successfully
- Ensure relationships were created correctly (Data → Relationships)
- Make sure PivotTables use the Data Model

Remember: Building a data model takes practice. Don't worry if it doesn't click immediately - work through the steps carefully and test as you go.

Happy modeling! 🌟📊
