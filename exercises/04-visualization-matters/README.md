# Step 4: Visualization Matters

Welcome to the fourth exercise! In this workshop, you'll discover how visualization choice directly impacts your ability to answer business questions. You'll experience firsthand why choosing the right chart type matters just as much as having clean data and a good data model.

## What You'll Learn

- How visualization choice affects the speed and confidence of decision-making
- Why the same data can tell different stories depending on how it's presented
- The difference between "technically correct" and "effective" visualizations
- How to evaluate whether a visual helps or hinders understanding
- That good visuals reduce cognitive effort and ambiguity

## Prerequisites

- Microsoft Excel 2016 or newer (including Microsoft 365)
- Completed Exercise 03 (Star Schema data model)
- Understanding of PivotTables and basic PivotCharts
- A working Excel file with:
  - **orders** (fact table)
  - **employees** dimension with Country
  - Relationships already established between tables

---

## Goal of This Exercise

The goal is **not** to create pretty dashboards or master advanced formatting. Instead, you will:

- Experience how a **poor visualization choice** makes simple questions difficult to answer
- Learn to **reflect critically** on why a visual works or doesn't work
- Understand that **visualization is a design choice** that should match the question
- See that **good data models are not enough**—you also need good visuals

**Key principle:** Visualization does not fix bad data, but bad visualization can hide good insights.

**Estimated time:** 30-45 minutes

---

## The Business Question

Throughout this exercise, you'll answer the **same business question** using different visualizations:

> **Which country generates the second highest revenue?**  
> **Roughly how high is the revenue?**  
> **How confident are you in your answer?**

Notice that this question requires you to:
- **Compare** values across countries
- **Rank** them (find the second highest)
- **Read** approximate values from the visual

Keep these requirements in mind as you work through the exercise.

---

## SECTION 1: Your Starting Point

### What You Already Have

By now, you should have an Excel workbook with:
- A **Star Schema data model** (fact table + dimension tables)
- **Relationships** between orders and employees (via EmployeeID)
- The **employees** table contains a **Country** column
- The **orders** table contains measurable data like **Revenue** or **OrderTotal**

### What You'll Do

You will create **two different visualizations** using exactly the same data:
1. A **poor visualization** that makes the question hard to answer
2. An **improved visualization** that makes the answer obvious

---

## SECTION 2: First Attempt – A Poor Visualization Choice

Let's start by creating a visualization that is **technically correct** but **not well suited** to answer the business question.

### Step 1: Create a PivotTable

1. In your Excel workbook (with the Star Schema model), go to the **Insert** tab on the ribbon
2. Click **PivotTable** dropdown and choose **From Data Model**
3. In the dialog box:
   - Choose "New Worksheet" as the destination
   - Click **OK**

You should now see an empty PivotTable on a new sheet.

### Step 2: Add Fields to the PivotTable

Now you'll configure the PivotTable to show revenue by country.

1. In the **PivotTable Fields** pane on the right:
   - **Drag** `Country` (from Employees) to the **Rows** area
   - **Drag** `Revenue` (from Orders) to the **Values** area

2. Verify that the Values field shows **Sum of Revenue** (not Count)
   - If it shows "Count of Revenue", click the field in the Values area
   - Select **Value Field Settings**
   - Choose **Sum**
   - Click **OK**

You should now see a table showing each country and its total revenue.

### Step 3: Create a Pie Chart (The Poor Choice)

Now let's visualize this data using a **pie chart**.

1. Click anywhere in your PivotTable
2. Go to the **Insert** tab
3. In the **Charts** group, click **Insert Pie or Doughnut Chart**
4. Select **Pie** (the first basic pie chart option)

Excel will create a pie chart showing the revenue distribution across countries.

### Step 4: Make It Alphabetically Sorted (Making It Worse)

Let's make this visualization even less effective by sorting the countries alphabetically instead of by value.

1. Click on any country name in the Pivot Table
2. Select **Data** → **Sort A to Z**

Now the pie slices are ordered alphabetically, not by size.

> 💡 **Why are we doing this?** To deliberately create a visualization that is **correct** (shows real data) but **ineffective** (hard to use for decision-making).

---

## SECTION 3: Try to Answer the Question

Now, use your pie chart to answer the business question:

> **Which country generates the second highest revenue?**  
> **Roughly how high is the revenue?**  
> **How confident are you in your answer?**

---

## SECTION 4: Reflection – Why This Visual Is Not Optimal

Let's analyze **why** the pie chart (sorted alphabetically) makes it hard to answer the business question.

### Problem 1: Pie Charts Are Poor for Comparison

**Pie charts show proportions of a whole.** They answer "What percentage does each part represent?"

But our question asks for **ranking** and **comparison**: "Which is second highest?"

**The issue:**
- Human eyes are bad at comparing angles and areas
- Slices that are similar in size are hard to rank
- You have to mentally scan the entire circle to find the largest, then the second largest

> 💡 **Design principle:** Use pie charts only when you want to emphasize parts of a whole (e.g., "Category A is more than half of total revenue"). Avoid them for ranking or precise comparison.

### Problem 2: Alphabetical Sorting Hides the Pattern

By sorting alphabetically, we've **removed the natural order** (high to low revenue).

**The issue:**
- The biggest slice might appear anywhere in the circle
- You can't scan from largest to smallest
- The visual order doesn't match the logical order (by value)

> 💡 **Design principle:** Sort data by value when the question involves ranking, comparison, or identifying top/bottom performers.

### Problem 3: Reading Exact Values Is Hard

Even with data labels showing percentages or currency, you have to:
- Read each label individually
- Mentally convert percentages back to actual revenue (if using %)
- Compare numbers instead of visual patterns

**The issue:**
- The visual doesn't help—you're just reading a table disguised as a chart
- If you're reading numbers anyway, why use a chart at all?

### The Core Problem: Wrong Tool for the Job

**Important:** The data is correct. The model is correct. The chart is technically accurate.

**But the visualization choice doesn't match the question.**

It's like using a hammer to screw in a screw—it might work, but it's not the right tool.

---

## SECTION 5: Second Attempt – An Improved Visualization

Now you'll create a **better visualization** using the exact same data. You won't change the PivotTable data—only the chart type and sorting.

### Step 1: Convert to a Bar Chart

1. Click on your existing pie chart to select it
2. Go to the **Design** tab (or **Chart Design** in some Excel versions)
3. Click **Change Chart Type**
4. In the dialog box:
   - Select **Bar** (or **Horizontal Bar**)
   - Choose the **Clustered Bar** chart (the first one)
5. Click **OK**

Your pie chart will instantly transform into a horizontal bar chart.

> 💡 **Note:** In Excel, "Bar" charts are horizontal, and "Column" charts are vertical. Either works for this exercise, but horizontal bars are often better when category names are long.

### Step 2: Sort by Value (High to Low)

Now let's sort the countries by revenue, from highest to lowest.

1. Right-click on any value (bar) in the chart 
2. Select **Sort** → **Sort Largest to Smallest**

Now the countries are ordered by revenue, with the highest at the top.

### Step 3: Format Numbers with Thousand Separators

Let's make the revenue values easier to read by adding thousand separators and setting 2 decimal places.

1. In the **PivotTable Fields** pane on the right, locate the **Values** area
2. Click on the value field (e.g., "Sum of Revenue") in the **Values** area
3. Select **Value Field Settings** from the dropdown menu
4. In the dialog box, click the **Number Format** button
5. In the Format Cells dialog:
   - Select **Number** from the Category list
   - Set **Decimal places** to **2**
   - Ensure **Use 1000 Separator (')** is checked
   - Click **OK**
6. Click **OK** again to close the Value Field Settings dialog

Your revenue values will now display with thousand separators (e.g., 1'234'567.89 instead of 1234567.89), making them much easier to read at a glance.

> 💡 **Why this matters:** Properly formatted numbers reduce cognitive load. It's instantly clear whether you're looking at thousands, millions, or billions.

### Step 4: Clean Up the Chart 

Make the chart easier to read:

1. **Add a clear chart title:**
   - Click on the chart title (default might be "Sum of Revenue" or "Total")
   - Type: **"Revenue by Country"**

2. **Ensure data labels are visible:**
   - Click on the bars
   - Right-click and select **Add Data Labels**
   - This shows the exact revenue value on each bar

3. **Remove unnecessary elements:**
   - If you see a legend (color key), you can delete it—it's redundant when category names are on the axis
   - Right-click the legend and select **Delete**

---

## SECTION 6: Try to Answer the Question Again

Now, use your **bar chart (sorted by value)** to answer the same business question:

> **Which country generates the second highest revenue?**  
> **Roughly how high is the revenue?**  
> **How confident are you in your answer?**

---

## SECTION 7: Optional Enhancement (If Time Permits)

If you have extra time, try these enhancements to make your bar chart even more effective:

### Enhancement 1: Add an Insight-Driven Title

Instead of a generic title like "Revenue by Country" write a title that **states the insight**:

**Examples:**
- "USA Leads Revenue, Followed by Germany"
- "Top 3 Countries Account for 80% of Revenue"

**Why this matters:**
- Readers immediately know what conclusion to draw
- The chart supports the claim visually
- Reduces ambiguity and speeds up decision-making

**How to do it:**
1. Click on the chart title
2. Type your insight-driven title

### Enhancement 2: Add Simple Data Labels

If you haven't already, add data labels to the bars:

1. Click on the bars in the chart
2. Right-click and select **Add Data Labels**
3. (Optional) Format the labels:
   - Right-click a label → **Format Data Labels**
   - Choose **Currency** or **Number** format in the Label Options, Number section
   - Adjust decimal places as needed

### Enhancement 3: Emphasize the Second Highest (Advanced)

If you want to highlight the second-highest category (since that's what the question asks for):

1. Click **once** on any bar to select all bars
2. Click **again** on the second-highest bar to select only that bar
3. Right-click → **Format Data Point**
4. Choose a different color (e.g., orange or red) to make it stand out in the "Fill & Line", Color section

> 💡 **Design principle:** "Less is more." Don't add decorations, 3D effects, or excessive colors. Every element should have a purpose.

---

## SECTION 8: Key Takeaways

Before you finish this exercise, reflect on these core lessons:

### 1. Visualization Does Not Fix Bad Data

- If your data is wrong or your model is broken, no chart will save you
- Clean data and a solid model are prerequisites
- Visualization is the **last step**, not the first

### 2. Visualization Does Not Replace Thinking

- A chart is a communication tool, not a magic answer generator
- You still need to understand your data and ask the right questions
- Bad questions yield useless visuals, even if the chart looks nice

### 3. Good Visuals Reduce Effort and Ambiguity

- The best visual makes the answer **obvious**
- It respects the viewer's time and cognitive load
- It minimizes the need for explanation

### 4. The Best Visualization Depends on the Question

- **For comparison and ranking:** Use bar or column charts (sorted by value)
- **For trends over time:** Use line charts
- **For parts of a whole:** Use pie charts (sparingly) or stacked bars
- **For distribution:** Use histograms or box plots

> 💡 **Golden rule:** Choose your chart type based on **what question you're answering**, not what looks pretty.

### 5. Simple Is Better Than Complex

- Avoid 3D effects, excessive colors, and decorative elements
- Use color intentionally (to highlight, not decorate)
- A simple, clear chart beats a fancy, confusing one every time

---

## Congratulations!

You've completed the **Visualization Matters** exercise! 🎉

You've learned that:
- The same data can be easy or hard to understand depending on how it's visualized
- Choosing the right chart type is a critical skill in business intelligence
- Good visuals help people make better decisions faster

---

## What's Next?

Now that you understand visualization principles, you're ready to build a complete dashboard! In **Exercise 05: Build Your First Dashboard**, you'll learn how to:
- Combine multiple visuals into a single-screen dashboard
- Create KPI cards, time trends, and ranking charts
- Add interactivity with slicers
- Evaluate and improve dashboard design
- Answer real business questions with your dashboard

[Continue to Exercise 05 →](../05-build-dashboard/README.md)

Or return to the [main README](../../README.md) to see all exercises.

---

**Ready for the next challenge?** Keep building your business intelligence skills! 📊✨
