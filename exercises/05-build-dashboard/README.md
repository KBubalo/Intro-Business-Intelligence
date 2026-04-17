# Step 5: Build Your First Dashboard

Welcome to the fifth exercise! In this workshop, you'll bring together everything you've learned so far to build a complete business intelligence dashboard in Excel. You'll create a single-screen report that answers real business questions and supports decision-making.

## What You'll Learn

- How to plan a dashboard around business questions (not just charts)
- How to create KPI cards to show key metrics at a glance
- How to build time-trend visuals to track performance over time
- How to build ranking visuals to identify top/bottom performers
- How to add interactivity with slicers
- How to evaluate if your dashboard is fit for decision-making
- How to improve dashboard design through iteration

## Prerequisites

- Microsoft Excel 2016 or newer (including Microsoft 365)
- Completed Exercises 02, 03, and 04
- An existing Excel workbook with:
  - **orders** (fact table) loaded in the Data Model
  - **products** dimension with ProductCategory
  - **customers** dimension
  - **employees** dimension
  - **Date** dimension table (covering all order dates)
  - Relationships already established between tables

**IMPORTANT:** You will continue working in your existing workbook from Exercise 03/04. Do not start a new file.

---

## Goal of This Exercise

The goal is to build a **single-screen dashboard** that answers two critical business questions:

### Business Question 1: "Are we performing better or worse over time?"

You'll create visuals showing:
- Total Revenue
- Revenue Growth (% change over time)
- Number of Orders
- Average Order Value (AOV)

### Business Question 2: "Which products contribute most to our success?"

You'll create visuals showing:
- Revenue by Product (or Product Category)
- Units Sold
- Top and Bottom Performers

**Key principle:** A dashboard is not a collection of random charts. It's a purposeful answer to specific business questions.

**Estimated time:** 60-75 minutes

---

## The Dashboard Building Process

You'll follow a **three-step approach**:

1. **Build a First Draft** (quickly, imperfect is okay)
2. **Evaluate** (does it answer the questions in 30 seconds?)
3. **Improve** (refine design, layout, titles)

This mirrors real-world BI work: iterate, don't aim for perfection on the first try.

---

## SECTION 1: Prepare Your Workspace

**⏱️ Estimated time: 5 minutes**

Before building the dashboard, you need a clean workspace.

### Step 1: Open Your Existing Workbook

1. Open the Excel workbook you used in Exercise 03 (Star Schema model)
2. This workbook should already contain your data model with relationships

### Step 2: Create a New Worksheet for the Dashboard

1. Right-click on any worksheet tab at the bottom
2. Select **Insert** → **Worksheet**
3. Right-click the new worksheet tab
4. Select **Rename**
5. Type: **Dashboard**
6. Press **Enter**

You now have a blank worksheet dedicated to your dashboard.

> 💡 **Why a separate sheet?** Keeping the dashboard separate from your data tables makes it easier to share with stakeholders and keeps your work organized.

### Step 3: Set Up the Canvas

Let's prepare the worksheet for a clean dashboard layout:

1. Select **View** tab on the ribbon
2. Uncheck **Gridlines** (this hides the grid lines)
3. Uncheck **Headings** (this hides row/column headers like A, B, C, 1, 2, 3)

Your worksheet now looks like a blank canvas, perfect for building a professional-looking dashboard.

> 💡 **Checkpoint:** You should see a blank white worksheet named "Dashboard" with no gridlines or headings visible.

---

## SECTION 2: First Draft – Build KPI Cards

**⏱️ Estimated time: 15 minutes**

KPI cards are simple visuals that show **one number prominently**. They answer "How much?" or "How many?" at a glance.

You'll create three KPI cards:
1. Total Revenue
2. Total Number of Orders
3. Average Order Value

### Step 1: Create a PivotTable for Total Revenue

1. In the **Dashboard** worksheet, click on cell **B2** (this will be the top-left corner of your first KPI)
2. Go to **Insert** tab → **PivotTable Dropdown** → **From Data Model**
3. In the dialog box:
   - Ensure your Data Model is selected
   - Choose to place the PivotTable in the existing worksheet at location **B2**
4. Click **OK**

You should now see an empty PivotTable in cell B2.

### Step 2: Configure the Revenue KPI

1. In the **PivotTable Fields** pane:
   - Find the **Orders** table (expand it if needed)
   - **Drag** the **Revenue** field (or **Line Total**, depending on your field name) to the **Values** area
2. Verify it shows **Sum of Revenue** (not Count)
   - If needed, click the field in the Values area → **Value Field Settings** → Choose **Sum**
3. Format the number:
   - Click on the value field in the **Values** area
   - Select **Value Field Settings**
   - Click **Number Format**
   - Choose **Currency** (or **Number**)
   - Set **Decimal places** to **0** (for whole numbers)
   - Ensure **Use 1000 Separator (,)** is checked
   - Click **OK** twice

You should now see a single number showing the total revenue (e.g. 80'487'704).

### Step 3: Style the Revenue KPI Card

Now let's make it look like a KPI card instead of a table:

1. Click on the PivotTable to select it
2. Go to **PivotTable Design** tab (or **Design** tab)
3. In the **Layout** group, click **Report Layout** → **Show in Tabular Form**
4. In the **Layout** group, click **Subtotals** → **Do Not Show Subtotals**
5. In the **Layout** group, click **Grand Totals** → **Off for Rows and Columns**
6. Select the row header (the cell that says "Sum of LineTotal" or similar) and rename it to **Total Revenue**

Now you should see just the number without labels or headers.

### Step 4: Format the KPI Value for Visual Impact

1. Click on the cell showing the revenue value (the number itself in your PivotTable)
2. Go to **Home** tab
3. Increase **Font Size** to **24** or **28** (make it big and prominent)
4. Make it **Bold**
5. (Optional) Change the font color to match your title

### Step 5: Create KPI Card for Number of Orders

Now let's create the second KPI card to the right of the first one.

1. Click on cell **D2** (leaving a column gap for spacing)
2. Go to **Insert** tab → **PivotTable Dropdown** → **From Data Model**
3. In the dialog box:
   - Ensure your Data Model is selected
   - Choose to place the PivotTable in the existing worksheet at location **D2**
4. Click **OK**
5. In the **PivotTable Fields** pane:
   - Drag **Sales Order ID** (or **OrderID**) from the **orders** table to the **Values** area
6. Change the aggregation to count **distinct** orders:
   - Click on the field in the Values area → **Value Field Settings**
   - If **Distinct Count** is available, select it
   - If not, select **Count** (note: this may count duplicate rows, but for most order datasets, Count works)
   - Click **OK**
7. Format the number:
   - Click the field in the Values area → **Value Field Settings** → **Number Format**
   - Choose **Number**
   - Set **Decimal places** to **0**
   - Use **1000 Separator**
   - Click **OK** twice
8.  Repeat the styling steps from Steps 3-5:
   - Turn off subtotals and grand totals
   - Add a title in **D2**: **Number of Orders**
   - Make the value large and bold (24-28 pt)

> 💡 **Note:** If your data model supports Distinct Count, use it to avoid counting the same order multiple times. If not available, Count usually works for fact tables where each row is a unique transaction.

### Step 6: Create KPI Card for Average Order Value

Now let's create the third KPI card showing Average Order Value (AOV).

**Conceptual formula:** AOV = Total Revenue / Number of Orders

**Excel approach:**
1. Click on cell **F2**
2. Go to **Insert** tab → **PivotTable Dropdown** → **From Data Model**
3. In the dialog box:
   - Ensure your Data Model is selected
   - Choose to place the PivotTable in the existing worksheet at location **F2**
4. Click **OK**
5. In the **PivotTable Fields** pane:
   - Drag **Revenue** to the **Values** area
   - Click the field in the Values area → **Value Field Settings**
   - In the **Summarize Values By** tab, scroll down and select **Average**
   - Click **OK**

**Alternative if average per line item isn't correct:**
   - If your orders table has multiple rows per order (e.g., order lines), the average might not be accurate
   - In that case, manually calculate: take the Total Revenue value from KPI 1 and divide by Number of Orders from KPI 2
   - Enter the formula in a regular cell (not PivotTable): `=B2/D2` (adjust cell references as needed)

> 💡 **Checkpoint:** You should check both numbers and decide which one makes more sense

6. Format the number as currency with 2 decimal places
7. Style the KPI card:
   - Turn off subtotals and grand totals (if Pivot Table)
   - Add a title in **F2**: **Average Order Value**
   - Make the value large and bold (24-28 pt)

> 💡 **Checkpoint:** You should now have three KPI cards in a row across the top of your dashboard: Total Revenue, Number of Orders, and Average Order Value.

---

## SECTION 3: First Draft – Build Time Trend Visual

**⏱️ Estimated time: 10 minutes**

Now you'll create a line chart showing **Revenue over Time** to answer "Are we performing better or worse?"

### Step 1: Create a PivotTable for Revenue by Month

1. Click on cell **B6** (below your KPI cards, with some space)
2. Go to **Insert** tab → **PivotTable**
3. Use the Data Model (same steps as before)
4. Place the PivotTable at **B6**
5. In the **PivotTable Fields** pane:
   - From the **Date** table, drag **Year** to the **Rows** area
   - From the **Date** table, drag **Month** (or **MonthName**) to the **Rows** area (below Year)
   - From the **orders** table, drag **Revenue** to the **Values** area
6. Verify it shows **Sum of Revenue**

You should now see a table with years and months in rows, and revenue values.

### Step 2: Fix the Month Sorting Problem

**Stop and look at your PivotTable!** You'll likely notice something strange: the months are sorted **alphabetically** (April, August, December, February, January, July...) instead of chronologically.

**Why does this happen?**  
Excel treats month names as text, so it sorts them alphabetically by default. This makes the time trend meaningless!

**The solution:** Use **Sort by Column** in the Data Model to tell Excel to sort MonthName by MonthNumber (1-12).

#### Fix the Sorting in the Data Model

1. Go to the **Data** tab on the ribbon
2. Click **Manage Data Model** (or **Power Pivot** → **Manage** if you have that option)
   - This opens the Power Pivot window showing your Data Model
3. In the Power Pivot window, click on the **Date** table tab at the bottom (to view the Date dimension)
4. Find and click on the **MonthName** column header to select the entire column
5. Go to the **Home** tab in the Power Pivot ribbon
6. Click **Sort by Column** (in the Sort and Filter group)
7. In the dialog box:
   - **Column:** Should show **Month Name** (the column you selected)
   - **By Column:** Select **Month Number** (or **Month** if it's a number field 1-12)
8. Click **OK**
9. Close the Power Pivot window (click the X or go back to Excel)

**Important:** Your Date dimension table must have both a **Month Name** column (text: "January", "February", etc.) and a **Month Number** column (number: 1, 2, 3, etc.) for this to work. If you built your Date table in Exercise 03, you should have this.

#### Verify the Fix

1. Back in your Excel worksheet, click on your PivotTable
2. Right-click on any month name in the PivotTable
3. Select **Refresh**
4. The months should now appear in correct chronological order: January, February, March, etc.

> 💡 **Data Modeling Insight:** "Sort by Column" is a crucial feature for any text column that has a logical order (months, days of week, custom categories like "Low, Medium, High"). Always sort these in the Data Model, not manually in each PivotTable.

> 💡 **Checkpoint:** Your PivotTable should now show months in chronological order within each year, making the time trend meaningful.

### Step 3: Create a Line Chart

1. Click anywhere in the PivotTable you just created
2. Go to **Insert** tab → **Charts** group
3. Click **Insert Line or Area Chart** (the line chart icon)
4. Select **Line** (the first basic line chart option)

Excel will create a line chart showing revenue over time.

### Step 4: Clean Up the Chart

1. Click on the chart title
2. Type a clear, insight-driven title: **"Revenue Trend Over Time"
3. Ensure the chart is large enough to read easily
   - Click on the chart border and drag the corners to resize
   - Aim for a width of 4-5 columns and height that's easy to read
4. Remove unnecessary elements:
   - If there's a legend, check if it's needed (for a single line, you can remove it)
   - Right-click the legend → **Delete** (if not needed)

> 💡 **Design tip:** A line chart is best for showing trends over time. The slope of the line immediately tells you if things are going up, down, or staying flat.

### Step 5: Add Revenue Growth Percentage

Now let's add **Revenue Growth (% change from previous period)** to show not just the trend, but how fast revenue is growing.

1. In the **PivotTable Fields** pane (for the same PivotTable you just created)
2. Drag **Revenue** to the **Values** area **again** (so you have it twice)
3. Click on the second **Sum of Revenue** in the Values area
4. Select **Value Field Settings**
5. In the **Custom Name** field at the top, type: **Revenue Growth %**
6. Click the **Show Values As** tab
7. In the dropdown, select **% Difference From**
8. In the **Base field**, select your time field (e.g., **Month** or **Year**)
9. In the **Base item**, select **(previous)**
10. Click **OK**

Now your PivotTable shows both the absolute revenue and the % change from the previous period. Your chart will show two lines, but they're on very different scales (revenue in dollars vs. growth in percentages).

### Step 6: Move Growth % to Secondary Axis

Since revenue (thousands/millions) and growth percentage (typically -20% to +50%) use completely different scales, we need to put them on separate axes.

1. Click on the chart to select it
2. Click on one of the data points or the line representing **Revenue Growth %** (the percentage line)
   - You may need to click twice: once to select the chart, again to select the specific line
   - When correctly selected, only that line's data points will be highlighted
3. Right-click on the selected line
4. Select **Change Series Chart Type** 
5. In the **Change Chart Type** dialog that appears:
   - Under **Series Options**, find the Secondary Axis checkbox for the **Revenue Growth %** series
   - Mark the checkbox **Secondary Axis**
6. Click **OK**

Now your chart has two Y-axes:
- **Primary axis (left):** Shows revenue in currency
- **Secondary axis (right):** Shows growth percentage

This makes both lines readable and meaningful!

### Step 6: Add the Legend Back

Since you now have two different measures on the chart, you need a legend to identify which line is which.

1. Click on the chart to select it
2. Go to the **Chart Design** tab (or **Design** tab)
3. Click **Add Chart Element** (or **Chart Elements** button with the + icon next to the chart)
4. Hover over **Legend**
5. Select **Bottom** (or **Right**, depending on your preference)

The legend will reappear, showing:
- One label for "Sum of Revenue"
- One label for "Revenue Growth %"

### Step 7: Clean Up Axis Titles (Optional but Recommended)

To make the chart crystal clear, add axis titles:

1. Click on the chart
2. Go to **Chart Design** tab → **Add Chart Element** → **Axis Titles**
3. Select **Primary Vertical** (for the left axis)
   - A text box will appear on the left axis
   - Type: **Revenue ($)**
   - Format it to be readable (rotate if needed)
4. Go to **Chart Design** tab → **Add Chart Element** → **Axis Titles**
5. Select **Secondary Vertical** (for the right axis)
   - A text box will appear on the right axis
   - Type: **Growth (%)**

Now your chart clearly shows both the revenue trend and growth rate, with proper labeling!

> 💡 **Checkpoint:** You should see a line chart with two lines: one showing revenue (left axis) and one showing growth % (right axis), with a legend identifying each line.

---

## SECTION 4: First Draft – Build Product Ranking Visual

**⏱️ Estimated time: 10 minutes**

Now you'll create a bar chart showing **which products (or product categories) generate the most revenue**.

**Pro tip:** For dashboards, you can create a PivotChart directly without showing a separate PivotTable on the worksheet. This keeps your dashboard cleaner!

### Step 1: Create a PivotChart Directly from the Data Model

1. Click somewhere on your worksheet where you want the chart to appear (e.g., to the right of your time trend chart, around column H or I)
2. Go to **Insert** tab → **Charts** group
3. Click **PivotChart** (there's a small dropdown arrow next to it)
4. In the dialog box:
   - Select **Use this workbook's Data Model**
   - Select **Existing Worksheet**
   - Click **OK**

Excel will create an empty PivotChart with the **PivotChart Fields** pane on the right. Notice there's no visible PivotTable on your worksheet—the data is stored behind the chart!

### Step 2: Configure the Chart to Show Revenue by Model Name

1. In the **PivotChart Fields** pane on the right:
   - From the **Products** table, drag **Model Name** to the **Axis (Categories)** area at the bottom
   - From the **Orders** table, drag **Revenue** to the **Values** area
2. Verify it shows **Sum of Revenue** in the Values area
   - If not, click the field → **Value Field Settings** → Select **Sum**
3. Format the revenue numbers:
   - Click on the value field in the Values area
   - Select **Value Field Settings**
   - Click **Number Format**
   - Choose **Currency** or **Number**
   - Set **Decimal places** to **0**
   - Ensure **Use 1000 Separator (,)** is checked
   - Click **OK** twice

You should now see a chart with model names and their revenue values.

### Step 3: Change to Horizontal Bar Chart and Sort

By default, Excel might create a column chart. Let's change it to a horizontal bar chart (better for ranking) and sort by value.

1. With the chart selected, go to **PivotChart Design** tab (or **Design** tab)
2. Click **Change Chart Type**
3. Select **Bar** → **Clustered Bar** (horizontal bars)
4. Click **OK**
5. Now sort the bars by value:
   - Click on any model name in the chart (on the vertical axis)
   - Right-click and select **Sort** → **More Sort Options** → **Ascending (A to Z) by Sum of Revenue**

Now your models are ranked from highest to lowest revenue, with the top performer at the top.

### Step 4: Clean Up the Chart

1. Click on the chart title
2. Type an insight-driven title: **"Top Models by Revenue"**
3. Resize the chart to make it readable (drag the corners)
4. Remove field buttons (the dropdown buttons on the chart):
   - With the chart selected, go to **PivotChart Analyze** tab (or **Analyze** tab)
   - Click **Field Buttons** → **Hide All**
   - This removes the clutter and makes your chart look more professional
5. Remove unnecessary legends (if you only have one data series)
6. (Optional) Add data labels:
   - Click on the bars → Right-click → **Add Data Labels**

> 💡 **Design tip:** Horizontal bar charts are perfect for ranking. The longest bar immediately shows the winner, and it's easy to compare lengths.

> 💡 **PivotChart advantage:** Notice how clean your dashboard looks without a visible PivotTable! The data is still there — it's just hidden behind the chart. This is perfect for dashboards where you want to show insights, not raw tables.

---

## SECTION 5: Add Interactivity with Slicers

**⏱️ Estimated time: 5 minutes**

Slicers allow users to filter the dashboard interactively (e.g., "Show me revenue for 2022 only" or "Show me only Electronics").

### Step 1: Insert a Slicer for Year

1. Click on any PivotTable **or PivotChart** in your dashboard
   - If you created PivotCharts directly (Section 4), click on one of those charts
   - Even though there's no visible PivotTable, PivotCharts have a hidden PivotTable behind them
2. Go to **PivotChart Analyze** tab (or **PivotTable Analyze** tab, or **Analyze** tab)
3. Click **Insert Slicer**
4. In the dialog box, you'll see all fields from your Data Model
5. Check the box next to **Year** (from the Date table)
6. Click **OK**

A slicer window will appear on your dashboard.

### Step 2: Position and Style the Slicer

1. Drag the slicer to a convenient location (e.g., top-right corner of your dashboard)
2. Resize it if needed (drag the corners)
3. (Optional) Style the slicer:
   - With the slicer selected, go to **Slicer** tab (or **Options** tab)
   - Click **Slicer Styles** and choose a color scheme
   - In **Slicer Settings**, you can change the number of columns

### Step 3: Connect the Slicer to All Visuals

By default, a slicer may only connect to the PivotTable/PivotChart you clicked on. You need to connect it to ALL PivotTables and PivotCharts on your dashboard.

1. Right-click on the slicer
2. Select **Report Connections** (or **PivotTable Connections**)
3. In the dialog box, check the boxes next to **all items** in your dashboard
   - This includes both visible PivotTables (like your KPI cards) and hidden PivotTables (behind your PivotCharts)
   - You should see entries for each visual/table on your dashboard
4. Click **OK**

Now, when you click a year in the slicer, all visuals will filter to show data for that year only.

### Step 4: Test the Slicer

1. Click on a year in the slicer (e.g., 2012)
2. Watch all your KPI cards and charts update to show only 2012 data
3. Click **Clear Filter** icon in the top-right of the slicer

> 💡 **Why slicers matter:** Slicers turn a static report into an interactive dashboard. Users can explore the data themselves and answer their own questions.

### Step 5 (Optional): Add More Slicers

If you have time and space, consider adding slicers for:
- **Model Name**
- **Employee Name**
- **Month**

Follow the same steps as above for each slicer.

> 💡 **Checkpoint:** You should have at least one slicer (e.g., Year) that filters all visuals on your dashboard when clicked.

---

## SECTION 6: The 30-Second Test – Evaluate Your Dashboard

**⏱️ Estimated time: 5 minutes**

Now step back and evaluate your dashboard. Imagine you're a manager who just opened this file. Can you answer the business questions in **30 seconds or less**?

### The 30-Second Test

Try to answer these questions using ONLY your dashboard:

1. **Are we performing better or worse over time?**
   - Is revenue growing, declining, or flat?
   - Can you see this immediately from your time trend chart?

2. **Which Model generates the second highest revenue in 2013?**
   - Can you identify the top 3 models at a glance?
   - Is the ranking obvious from your bar chart?

3. **What is our total revenue, and how many orders did we process?**
   - Are your KPI cards readable from a distance?
   - Do the numbers stand out?

### Dashboard Evaluation Checklist

Answer these questions honestly:

| Criteria | Yes | No | Notes |
|----------|-----|----|-------|
| **Clarity:** Can I answer the business questions in 30 seconds? | ☐ | ☐ | |
| **Visual Hierarchy:** Do the most important numbers stand out? | ☐ | ☐ | |
| **Chart Choice:** Are line charts used for trends and bar charts for ranking? | ☐ | ☐ | |
| **Sorting:** Are ranking charts sorted by value (not alphabetically)? | ☐ | ☐ | |
| **Titles:** Do chart titles communicate insights (not just data descriptions)? | ☐ | ☐ | |
| **Formatting:** Are numbers formatted consistently (currency, decimals, separators)? | ☐ | ☐ | |
| **Interactivity:** Can I filter the dashboard using slicers? | ☐ | ☐ | |
| **Layout:** Is the dashboard organized logically (e.g., KPIs at top, details below)? | ☐ | ☐ | |
| **Clutter:** Is the dashboard free of unnecessary gridlines, legends, and decorations? | ☐ | ☐ | |

**If you answered "No" to 3 or more criteria, your dashboard needs improvement.**

> 💡 **Reflection:** A good dashboard answers questions immediately. If someone has to study it for minutes, squint at labels, or ask you to explain it, the design needs work.

---

## SECTION 7: Improve Your Dashboard

**⏱️ Estimated time: 10-15 minutes**

Based on your evaluation, now improve your dashboard. Here are common improvements:

### Improvement 1: Make KPI Cards Stand Out More

- Increase the font size of the KPI values even more (try 32 or 36 pt)
- Add a subtle background color to the KPI card area:
  - Select cells around the KPI (e.g., B1:C3)
  - Go to **Home** tab → **Fill Color** → Choose a light gray or light blue
- Add a border around each KPI card:
  - Select the KPI card area → **Home** tab → **Borders** → **All Borders**

### Improvement 2: Improve Chart Titles

Replace generic titles with **insight-driven titles** that tell the story:

**Before:** "Revenue Trend Over Time"  
**After:** "Revenue Grew 25% Year-over-Year" or "Revenue Reached $2M in 2013"

**Before:** "Top Product Categories by Revenue"  
**After:** "Electronics Generates 40% of Total Revenue"

**How to create insight-driven titles:**
1. Look at your chart
2. Ask: "What's the one thing I want the viewer to remember?"
3. Write that as the title

### Improvement 3: Align and Space Elements Evenly

- Use Excel's **Align** tools to line up charts and KPI cards:
  - Select multiple objects (hold **Ctrl** and click each one)
  - Go to **Shape Format** tab → **Align** → **Align Top** (or **Align Left**, etc.)
- Ensure consistent spacing between elements:
  - Leave at least 1 column between KPI cards
  - Leave at least 1-2 rows between chart sections

### Improvement 4: Remove Unnecessary Elements

- Delete field buttons from PivotCharts:
  - Click on a PivotChart
  - Go to **PivotChart Analyze** tab (or **Analyze** tab)
  - Click **Field Buttons** → **Hide All**
- Remove gridlines from charts (if they clutter the visual)
- Remove legends that state the obvious

### Improvement 5: Add a Dashboard Title

1. Click on cell **A1**
2. Type a dashboard title: **"Sales Performance Dashboard"** or **"Executive Summary – Q4 2023"**
3. Make it **Bold**, **Large** (18-20 pt), and consider a distinctive color
4. Center it across the top of your dashboard

### Improvement 6: Add Context or Annotations (Optional)

If a chart shows something surprising or important:
- Add a text box with a comment:
  - Go to **Insert** tab → **Text Box**
  - Draw a box near the relevant chart
  - Type a short insight (e.g., "Holiday season spike in December")
  - Format the text box (remove border, set font size)

> 💡 **Design principle:** Every element on your dashboard should have a purpose. If it doesn't help answer the business questions, remove it.

### Improvement 7: Test Again with the 30-Second Rule

After making improvements:
1. Close the Excel file and reopen it (or move to a different worksheet and come back)
2. Set a timer for 30 seconds
3. Try to answer the business questions again
4. **Did it get easier?** If yes, your improvements worked!

---

## SECTION 8: Final Deliverable Checklist and Reflection

**⏱️ Estimated time: 5 minutes**

Before you finish, verify your dashboard meets all requirements:

### Final Deliverable Checklist

- ☐ **Dashboard worksheet created** and named "Dashboard"
- ☐ **At least 3 KPI cards** (Total Revenue, Number of Orders, Average Order Value)
- ☐ **At least 1 time-trend visual** (e.g., Revenue over Time line chart)
- ☐ **At least 1 ranking visual** (e.g., Revenue by Product Category bar chart)
- ☐ **At least 1 slicer** (e.g., Year slicer) that filters all visuals
- ☐ **All PivotTables built from the Data Model** (not from worksheet tables)
- ☐ **Charts are sorted correctly** (time charts chronologically, ranking charts by value)
- ☐ **Numbers are formatted consistently** (currency with thousand separators where appropriate)
- ☐ **Chart titles communicate insights** (not just data descriptions)
- ☐ **Layout is clean and organized** (no gridlines, consistent spacing, logical flow)
- ☐ **Dashboard answers both business questions** in 30 seconds or less

---

## Congratulations!

You've built your first business intelligence dashboard! 🎉

You've learned that:
- Dashboards exist to answer business questions, not just show data
- Less is more: simplicity beats complexity
- Visualization choice matters: line charts for trends, bar charts for ranking, KPIs for key metrics
- Iteration is key: build fast, evaluate, improve

### What's Next?

In future work, you can:
- Learn more advanced Excel features (calculated fields, custom measures)
- Explore Power BI for more sophisticated dashboards
- Practice storytelling with data (how to present findings)
- Build dashboards for different audiences (executives, managers, analysts)

### Save Your Work

Make sure to save your Excel workbook. You've built something valuable that you can reference in the future or include in your portfolio!

---

**You've completed Step 5!** You now have the skills to build decision-ready dashboards in Excel. Keep practicing and exploring new ways to visualize data! 📊✨
