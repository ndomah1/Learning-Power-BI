# Learning Power BI

## Table of Contents
- [Installing Power BI and Building the First Visualization](#installing-power-bi-and-building-the-first-visualization)
  - [Downloading and Installing Power BI Desktop](#downloading-and-installing-power-bi-desktop)
  - [Importing Data into Power BI](#importing-data-into-power-bi)
  - [Transforming Data Using Power Query](#transforming-data-using-power-query)
- [Building the First Visualization](#building-the-first-visualization)
  - [Objective: Identify the Best Store for Purchasing Items](#objective-identify-the-best-store-for-purchasing-items)
  - [Customizing the Dashboard](#customizing-the-dashboard)
- [Using Power Query in Power BI](#using-power-query-in-power-bi)
- [Cleaning and Transforming Data](#cleaning-and-transforming-data)
- [Creating and Managing Relationships in Power BI](#creating-and-managing-relationships-in-power-bi)
- [Introduction to DAX (Data Analysis Expressions)](#introduction-to-dax-data-analysis-expressions)
  - [DAX Essentials: Measures vs. Calculated Columns](#dax-essentials-measures-vs-calculated-columns)
- [Using Drill Down in Power BI](#using-drill-down-in-power-bi)
- [Conditional Formatting in Power BI](#conditional-formatting-in-power-bi)
- [Bins and Lists in Power BI](#bins-and-lists-in-power-bi)
- [Popular Visualizations in Power BI](#popular-visualizations-in-power-bi)

## **Installing Power BI and Building the First Visualization**

### **Downloading and Installing Power BI Desktop**

- Power BI Desktop is free to download from the [Microsoft Store](https://www.microsoft.com/en-us/download/details.aspx?id=58494).
- Once installed, open Power BI by searching for it in the Start menu.

### **Importing Data into Power BI**

1. Click on **"Get Data"** in the Power BI interface.
2. A window opens showing multiple data source options:
    - Databases (SQL, PostgreSQL)
    - Cloud services (Google Analytics, Blob Storage)
    - Local files (Excel, CSV, JSON)
3. For this tutorial, an **Excel Workbook** is used:
    - Click **Excel Workbook** → **Connect**.
    - Select the file (e.g., "Apocalypse Food Prep.xlsx").
    - Power BI will display available sheets. Select the desired sheet.
    - Click **Load** to import the data.

![image.png](image.png)

### **Transforming Data Using Power Query**

- After loading the data, you can either:
    - **Load it directly** into Power BI.
    - **Transform it first** using Power Query.
- Power Query allows for:
    - Renaming columns.
    - Removing unnecessary data.
    - Filtering rows (e.g., removing milk from an apocalypse food prep list).

#### **Example Transformation Steps:**

1. Renaming the "Date" column to **"Date_Purchased"**.
2. Filtering out unwanted data (e.g., removing "Milk" as it's not useful for long-term storage).
    
    ![image.png](image%201.png)
    

### **Understanding the Power BI Interface**

Power BI consists of three main tabs:

1. **Report Tab** - Where visualizations and dashboards are created.
2. **Data Tab** - Allows you to inspect and modify imported data.
3. **Model Tab** - Helps create relationships between multiple tables (covered in later tutorials).

![image.png](image%202.png)

## **Building the First Visualization**

### **Objective: Identify the Best Store for Purchasing Items**

- The dataset includes **store names, product types, and prices**.
- The goal is to find:
    1. Where the least amount of money is spent for the same product.
    2. Whether all products should be purchased at one store or different stores.

### **Steps to Create Visualizations:**

1. Select **"Store"** and **"Price"** columns.
2. Use a **Stacked Column Chart** to visualize total spending per store.
    - Costco appears to be the cheapest overall.
    - Target is the cheapest for rice.
3. Create a **Clustered Column Chart** to compare price differences per product across stores.
    - Most products are cheapest at Costco.
    - Rice is significantly cheaper at Target.
- The Stacked Column Chart showing spending at each store.
- The Clustered Column Chart comparing product prices across stores.

![image.png](image%203.png)

### **Customizing the Dashboard**

- Resize visualizations for a clearer layout.
- Change titles:
    - "Best Store for Each Product"
    - "Total Spending by Store"
- Add **Data Labels** to display exact numbers.
- Adjust display settings to show full numeric values instead of rounded figures.

![image.png](image%204.png)

### **Using Power Query in Power BI**

#### **What is Power Query?**

Power Query is a **data transformation tool** within Power BI that allows you to:

- Clean and reshape data before loading it into Power BI.
- Remove, add, or modify columns.
- Change data types.
- Apply transformations such as filtering, splitting, and unpivoting columns.

**Why use Power Query?** It makes raw data more structured and usable for creating accurate visualizations.

#### **Importing Data into Power Query**

1. Click **"Get Data"** → Select **Excel Workbook** → **Connect**.
2. Choose the **Apocalypse Food Prep.xlsx** file.
3. Select both:
    - **Pivot Table**
    - **Purchase Overview**
4. Click **Transform Data** instead of Load.

#### **Understanding the Power Query Interface**

- **Left Sidebar**: Shows queries (imported tables).
- **Top Ribbon**:
    - **Home Tab**: Remove columns, keep/remove rows, split columns.
    - **Transform Tab**: Change data types, pivot/unpivot columns, use first row as headers.
    - **Add Column Tab**: Add calculated, index, or conditional columns.
- **Right Sidebar (Query Settings)**:
    - Applied Steps: Tracks every modification for easy rollback.

## **Cleaning and Transforming Data**

### **Step 1: Remove Unnecessary Rows**

- The first two rows in the **Purchase Overview** table contain null values.
- Go to **Home Tab** → **Remove Rows** → **Remove Top Rows** → Enter **2** → **O**

### **Step 2: Use First Row as Headers**

- The actual column names are in the first row.
- Go to **Transform Tab** → Click **Use First Row as Headers**.

### **Step 3: Changing Data Types**

- Power Query automatically assigns data types.
- Ensure numbers representing money use a **Fixed Decimal** format.
    - Click on the **data type icon** (e.g., "1.2") → Select **Fixed Decimal Number**.
    - Apply this to all price-related columns.

### **Step 4: Removing Totals and Subtotals**

- The dataset contains **Costco Total, Target Total, Walmart Total, and Grand Total**, which are unnecessary.
- Filter them out:
    - Click **Dropdown on Product Column** → **Text Filters** → **Does Not Contain "Total"** → **OK**.
- Remove the **Grand Total column**:
    - Click on **Grand Total Column** → **Remove Columns**.

### **Step 5: Unpivoting Data for Better Analysis**

- Dates (January 1st, February 1st, etc.) are column headers but should be in rows.
- Select **all date columns**.
- Go to **Transform Tab** → Click **Unpivot Columns**.
- Rename the new columns:
    - **Attribute → Date**
    - **Value → Product Cost**

![image.png](image%205.png)

### **Finalizing and Loading the Data**

- Click **Close & Apply** to load the cleaned data into Power BI.
- Verify the data in the **Data View**.
- If more adjustments are needed, click **Transform Data** to return to Power Query.

![image.png](image%206.png)

## **Creating and Managing Relationships in Power BI**

### **What are Relationships in Power BI?**

- When working with multiple tables from **different sources or the same source**, relationships allow data to be **connected** for analysis.
- Power BI automatically **detects relationships**, but they can also be **manually created** or **edited**.

#### **Why relationships?**

- They help connect datasets **logically** for meaningful analysis.
- Avoids unnecessary duplication of data.
- Enables cross-table calculations in reports and dashboards.

**Key Tables Used in This Example:**

1. **Apocalypse Store** (Products being sold)
    - Product ID
    - Product Name
    - Price
    - Production Cost
2. **Apocalypse Sales** (Sales transactions)
    - Customer ID
    - Product ID
    - Order ID
    - Units Sold
    - Date Purchased
3. **Customer Information** (Customer details)
    - Customer ID
    - Address, City, State, Zip Code

### **Importing Data and Navigating to the Model View**

1. Click **"Get Data"** → Select **Excel Workbook** → **Connect**.
2. Choose all three tables (**Apocalypse Store, Apocalypse Sales, Customer Information**).
3. Click **Load** (No need to transform the data in this case).
4. Navigate to **Model View (third tab on the left sidebar)** to see automatically created relationships.

![image.png](image%207.png)

### **Understanding Relationships in Power BI**

#### **Existing Automatically Created Relationships**

- Power BI detects relationships **based on matching column names** and **similar data types**.
- Relationships appear as **lines** connecting tables.
- **Double-clicking a relationship line** brings up the **Edit Relationship** window.

#### **Key Relationship Properties**

1. **Cardinality**:
    - **One-to-Many (1:*M*)** – One table has unique values, and another has multiple corresponding values (e.g., Customers → Sales).
    - **Many-to-One (*M*:1)** – Same as above, but flipped direction.
    - *Many-to-Many (M:M)* – Both tables have non-unique values.
    - **One-to-One (1:1)** – Both tables have unique values (rare case).
2. **Cross Filter Direction**:
    - **Single** – One table filters another, but not vice versa.
    - **Both** – Tables filter each other, treating them as a single table.
3. **Active vs. Inactive Relationships**:
    - **Active** – The default relationship used for calculations.
    - **Inactive** – Not used unless explicitly referenced in formulas.

![image.png](image%208.png)

#### **Editing an Existing Relationship**

1. **Open Model View** → **Double-click a relationship line**.
2. **Change the Join Column** (e.g., use **Customer ID** instead of **Customer Name** for better consistency).
3. **Set Cardinality** (e.g., Many-to-One for Sales and Customer Information).
4. **Change Cross Filter Direction** to **Both** if necessary.
5. **Click OK** to save changes.

![image.png](image%209.png)

#### **Manually Creating Relationships**

If Power BI **does not detect** a relationship, it can be manually created:

1. Open **Model View**.
2. Drag **Customer ID** from **Customer Information** → Drop onto **Customer ID** in **Apocalypse Sales**.
3. Drag **Product ID** from **Apocalypse Store** → Drop onto **Product ID** in **Apocalypse Sales**.
4. Double-click each new relationship to **set properties**.
    - Change **Cross Filter Direction** to **Both** if needed.
    - Set **Cardinality** correctly (**One-to-Many** for Customers → Sales).

![image.png](image%2010.png)

#### **Verifying Relationships with a Visualization**

1. **Create a Table Visualization**.
2. Add **State** (from Customer Information).
3. Add **Product ID Count** (from Apocalypse Store).
4. Initially, the count might be incorrect (showing all products in all states).
5. **Switch Cross Filter Direction to Both** → The visualization updates to show the correct counts per state.

![image.png](image%2011.png)

## **Introduction to DAX (Data Analysis Expressions)**

### **What is DAX?**

DAX (Data Analysis Expressions) is a **formula language** used in Power BI to create **calculated columns, measures, and tables**. It is similar to Excel formulas but optimized for Power BI's data model.

#### **Why use DAX?**

- Performs **advanced calculations** that cannot be done with basic visualizations.
- Enables **dynamic aggregations** (e.g., total sales, average revenue).
- Helps in creating **custom metrics** for reports and dashboards.

### **DAX Essentials: Measures vs. Calculated Columns**

| Feature | Measures | Calculated Columns |
| --- | --- | --- |
| **Stored in** | Data model (optimized) | Dataset (increases size) |
| **Calculation Timing** | Calculated **on the fly** | Calculated **when data is refreshed** |
| **Usage** | Summarized results | Row-level calculations |
| **Best For** | Aggregations (SUM, COUNT, AVERAGE) | Derived fields (profit, categories) |

📌 **Example:**

- **Measure**: `Total Sales = SUM(Sales[Revenue])`
- **Calculated Column**: `Profit = Sales[Revenue] - Sales[Cost]`

### **Creating a DAX Measure**

#### **Example: Counting Total Sales**

1. Navigate to the **Report Tab**.
2. Right-click **Apocalypse Sales** → **New Measure**.
3. Enter the following formula:
    
    ```
    Count of Sales = COUNT(Apocalypse Sales[Order ID])
    ```
    
4. Press **Enter**. The measure now appears in the Fields pane.
5. Drag it into a table visualization to display the count.

![image.png](image%2012.png)

### **Using DAX Aggregations**

#### **Example: Summing Total Products Sold**

1. Create a new measure:
    
    ```
    Sum of Products Sold = SUM(Apocalypse Sales[Units Sold])
    ```
    
2. Drag it into a table visualization to see total products sold.

**Key Takeaway**: `SUM()` is an **aggregator function**, summing all values in a column.

![image.png](image%2013.png)

### **Iterator vs. Aggregator Functions**

#### **Understanding SUM vs. SUMX**

- `SUM()` adds all values in a column (aggregates).
- `SUMX()` calculates **row by row** before summing the results.

#### **Example: Calculating Profit**

1. Create a new measure:
2. This calculates **total** profit across all products.

**Problem**: If we want **profit per product**, `SUM()` won’t work correctly. We need `SUMX()`.

#### **Solution: Using SUMX for Row-Level Calculation**

1. Create a new column:
    
    ```
    Profit_Column = SUMX(Apocalypse Sales, Apocalypse Store[Price] - Apocalypse Store[Production Cost])
    ```
    
2. This ensures profit is calculated for each **row** before summing.

📌 **Screenshot Suggestion**: Show the difference between `SUM()` and `SUMX()` in a table.

![image.png](image%2014.png)

![image.png](image%2015.png)

### **Working with Date Functions in DAX**

DAX provides several **date-based functions** to analyze trends.

#### **Example: Extracting the Day of the Week**

1. Create a new column:
    
    ```
    Day of Week = WEEKDAY(Apocalypse Sales[Date Purchased], 2)
    ```
    
    - `2` makes Monday = `1`, Sunday = `7`.
2. Use this to analyze **sales trends by day**.

![image.png](image%2016.png)

### **Using IF Statements in DAX**

The `IF()` function helps classify data.

#### **Example: Categorizing Order Sizes**

1. Create a new column:
    
    ```
    Order_Size = IF(Apocalypse Sales[Units Sold] > 25, "Big Order", "Small Order")
    ```
    
2. This classifies **large vs. small orders**.

![image.png](image%2017.png)

## **Using Drill Down in Power BI**

### **What is Drill Down?**

Drill Down allows users to **explore data hierarchically**, from a **high-level summary to detailed insights** within a visualization. It helps in:

- **Adding depth** to visualizations without cluttering the initial view.
- **Providing interactive insights** during presentations.
- **Allowing users to navigate up and down different data levels.**

#### **Drill Down Actions:**

1. **Drill Down** - Click a category to see its detailed breakdown.
2. **Drill Up** - Move back to a higher-level summary.
3. **Next Level** - Move down the hierarchy in a linear manner.
4. **Expand All** - Show all levels at once instead of drilling down one at a time.

### **Creating a Drill Down Hierarchy**

#### **Example: Exploring Store and Product Purchases**

1. Create a **Clustered Column Chart** visualization.
2. Add **Store Name** to the **X-axis**.
3. Add **Total Purchase Cost** to the **Y-axis**.
4. Add **Product Name** beneath **Store Name** in the X-axis.
5. Power BI will automatically create a **hierarchy**.

**What happens?**

- The visualization starts at the **store level**.
- Users can **drill down into a store** to see **product-level spending**.

### **Enabling Drill Down**

Once a hierarchy is created, **Drill Down options** appear:

1. **Drill Down Mode (Click to Expand)**:
    - Turn on the **drill mode**.
    - Click on a **store** (e.g., Target) to see a breakdown by **products purchased** there.
2. **Next Level in Hierarchy**:
    - Click **“Go to Next Level”**.
    - The chart shifts to show **only the product-level breakdown**, ignoring the store grouping.
3. **Expand All Levels**:
    - Click **“Expand All”**.
    - The chart displays **both store and product details together**, instead of separating them.

![image.png](image%2018.png)

![image.png](image%2019.png)

### **Example Use Cases for Drill Down**

#### **1. Sales Analysis**

- Start with **Total Sales by Region**.
- Drill down to **Sales by State**.
- Further drill down to **Sales by City**.

#### **2. Customer Order Tracking**

- Show **Total Orders by Customer**.
- Drill down to **Order IDs for each Customer**.
- Further drill down to **Products in each Order**.

#### **3. Financial Reporting**

- Begin with **Total Company Expenses**.
- Drill down to **Department-Level Expenses**.
- Further drill down to **Expense Categories (e.g., Salaries, Rent, Software)**.

### **Real-World Example: Order Tracking**

1. Create a **Bar Chart** with:
    - **Customer Name** on the X-axis.
    - **Units Sold** on the Y-axis.
2. Add **Order ID** beneath **Customer Name** in the X-axis.
3. Enable **Drill Down Mode**.
4. Click on a **customer** to see **their specific order IDs**.

**Use Case**: This is useful when a **stakeholder** wants to analyze specific orders behind high-volume customers.

![image.png](image%2020.png)

![image.png](image%2021.png)

## **Conditional Formatting in Power BI**

### **What is Conditional Formatting?**

Conditional Formatting allows users to **visually highlight** important data within tables and matrices by applying:

- **Color scales** (e.g., green for low values, red for high values).
- **Icons** to indicate specific thresholds.
- **Data bars** to show relative magnitude within cells.

#### **Why use Conditional Formatting?**

- Helps in **identifying trends and outliers quickly**.
- Provides **context to raw numbers**.
- Enhances **data storytelling in reports**.

### **Applying Conditional Formatting**

1. Create a **Table or Matrix visualization**.
2. Add relevant fields (e.g., **Product Name, Price, Units Sold**).
3. Right-click on a numeric column (e.g., **Price**).
4. Select **Conditional Formatting** → Choose one of the following:
    - **Background Color**
    - **Font Color**
    - **Icons**
    - **Data Bars**

### **Types of Conditional Formatting**

#### **1. Background Color Formatting**

- Colors the cell background based on value.
- Useful for identifying **low and high values at a glance**.

**Example: Coloring Products by Price**

1. Select **Price** column.
2. Apply **Gradient Scale**:
    - **Low values** = Green (cheaper items).
    - **High values** = Red (expensive items).
3. Click **OK**.

![image.png](image%2022.png)

#### **2. Data Bars for Visual Emphasis**

- **Adds horizontal bars** inside table cells to compare values visually.
- Only available for **aggregated fields** (e.g., total sales, revenue).

📌 **Example: Comparing Units Sold**

1. Select **Units Sold**.
2. Apply **Data Bars**:
    - **Short bars** for low sales.
    - **Long bars** for high sales.
3. Click **OK**.

![image.png](image%2023.png)

#### **3. Rule-Based Formatting**

- Custom **if-then rules** to color-code cells.
- Example: Flagging **low-selling products**.

**Example: Marking Low Sales in Red**

1. Select **Units Sold**.
2. Apply **Rule-Based Formatting**:
    - **If Units Sold < 200 → Color: Red** (Low Sales).
    - **If Units Sold ≥ 200 and ≤ 500 → Color: Yellow** (Average Sales).
    - **If Units Sold > 500 → Color: Green** (High Sales).
3. Click **OK**.

#### **4. Icon-Based Formatting**

- Adds **icons** (e.g., arrows, checkmarks, flags) to visually categorize data.
- Works similarly to **Excel icon sets**.

**Example: Performance Indicator for Revenue**

1. Select **Revenue**.
2. Apply **Icon Formatting**:
    - **Red Down Arrow** = Low Revenue.
    - **Yellow Dash** = Average Revenue.
    - **Green Up Arrow** = High Revenue.
3. Click **OK**.

### **Best Practices for Conditional Formatting**

- **Use sparingly** – Too many colors/icons can clutter reports.
- **Stick to meaningful colors** (e.g., Red = warning, Green = positive).
- **Use a combination** – **Data bars + color formatting** work well together.
- **Keep it accessible** – Ensure colors/icons are readable by all users.

![image.png](image%2024.png)

## **Bins and Lists in Power BI**

### **What are Bins and Lists?**

Bins and Lists allow users to **group data into categories** for easier analysis.

- **Lists** group **specific values** together (e.g., grouping customers into "Top Buyers" and "Low Buyers").
- **Bins** categorize **numerical data into ranges** (e.g., age groups: 18-29, 30-39, etc.).

#### **Why use Bins and Lists?**

- **Simplifies large datasets** by grouping values into meaningful segments.
- **Improves visualization clarity** by reducing unique data points.
- **Helps in trend analysis** by focusing on grouped data instead of individual values.

### **Creating a List in Power BI**

A **List** groups categorical data manually.

#### **Example: Grouping Customers by Performance**

1. Navigate to **Apocalypse Sales** → Select **Customer**.
2. Right-click on **Customer** → Click **New Group**.
3. Rename the group to **Customer List**.
4. Select **Top-performing customers** → Click **Group**.
5. Rename this group to **Best Prepping Stores**.
6. Select **Low-performing customers** → Click **Group**.
7. Rename this group to **Worst Prepping Stores**.
8. Click **OK**.

**What happens?**

- A new column is created that classifies customers as **Best or Worst Prepping Stores**.
- This can now be used in visualizations.

![image.png](image%2025.png)

### **Using Lists on Numerical Fields**

Lists can also be created for **numeric values**, such as **Order ID**.

#### **Example: Categorizing Order IDs**

1. Navigate to **Order ID**.
2. Right-click → Click **New Group**.
3. Rename the group to **Order Categories**.
4. Select **First 50 Order IDs** → Click **Group** → Rename to **First Orders**.
5. Select **Last 50 Order IDs** → Click **Group** → Rename to **Latest Orders**.
6. Click **OK**.

**Use Case**: This allows tracking of **early vs. recent orders** in a dataset.

![image.png](image%2026.png)

### **Creating Bins in Power BI**

A **Bin** divides **numerical data into predefined ranges**.

#### **Example: Categorizing Customers by Age**

1. Navigate to **Customer Information** → Select **Age**.
2. Right-click **Age** → Click **New Group**.
3. Under **Bin Type**, select **Bin**.
4. Set **Bin Size** to **10** (to group ages by decade).
5. Click **OK**.

**What happens?**

- A new column is created grouping customers into age ranges:
    - 10-19
    - 20-29
    - 30-39
    - 40-49, etc.

![image.png](image%2027.png)

### **Using Bins on Date Fields**

Bins can also be applied to **date-based data**.

#### **Example: Grouping Sales by Month**

1. Navigate to **Apocalypse Sales** → Select **Date Purchased**.
2. Right-click **Date Purchased** → Click **New Group**.
3. Under **Bin Type**, select **Bin**.
4. Set **Bin Size** to **1 Month**.
5. Click **OK**.

**What happens?**

- A new column is created that groups sales into **monthly periods**.
- This simplifies trend analysis.

![image.png](image%2028.png)

### **Visualizing Bins and Lists**

#### **1. Comparing Age Groups (Bins)**

1. Create a **Bar Chart**.
2. Add **Age Bins** to the X-axis.
3. Add **Number of Buyers** to the Y-axis.
4. Analyze which age group has the most buyers.

![image.png](image%2029.png)

#### **2. Analyzing Customer Performance (Lists)**

1. Create a **Clustered Column Chart**.
2. Add **Customer List (Best/Worst Prepping Stores)** to the X-axis.
3. Add **Units Sold** to the Y-axis.
4. Compare sales between **Best and Worst Prepping Stores**.

![image.png](image%2030.png)

## **Popular Visualizations in Power BI**

### **Choosing the Right Visualization**

Power BI offers **various visualization types**, each suited for different kinds of analysis. This section covers **the most commonly used** visualizations.

#### **Why visualizations matter?**

- Helps in **interpreting complex data** easily.
- Enhances **data storytelling** in reports and dashboards.
- Different visualizations **highlight different insights**.

### **1. Stacked Bar Chart**

- **Best for** comparing **categories and subcategories**.
- Displays a total sum while breaking it into parts.

**Example: Units Sold by Product**

1. Select **Stacked Bar Chart**.
2. Add **Product Name** to the Y-axis.
3. Add **Units Sold** to the X-axis.
4. Drag **Product Name** to the **Legend** (color-coded by product).

![image.png](image%2031.png)

### **2. 100% Stacked Column Chart**

- **Best for** understanding category proportions.
- Each column represents 100%, with sections showing **relative contributions**.

**Example: Customer Purchase Breakdown**

1. Select **100% Stacked Column Chart**.
2. Add **Customer** to the X-axis.
3. Add **Units Sold** to the Y-axis.
4. Add **Product Name** to the **Legend** (breaks sales into product categories).

![image.png](image%2032.png)

### **3. Line Chart**

- **Best for** tracking trends over time.
- Ideal for **date-based analysis**.

**Example: Sales Over Time**

1. Select **Line Chart**.
2. Add **Date Purchased** to the X-axis.
3. Add **Units Sold** to the Y-axis.
4. Drag **Product Name** to the **Legend** (separate lines per product).

![image.png](image%2033.png)

### **4. Line & Clustered Column Chart**

- **Best for** showing **two different types of measures** together.
- Combines **bar and line visualizations**.

**Example: Price vs. Production Cost**

1. Select **Line & Clustered Column Chart**.
2. Add **Product Name** to the X-axis.
3. Add **Price** to **Column Y-axis**.
4. Add **Production Cost** to **Line Y-axis**.

![image.png](image%2034.png)

### **5. Scatter Plot**

- **Best for** identifying **outliers and relationships between variables**.
- Helps in **correlation analysis**.

**Example: Price vs. Production Cost**

1. Select **Scatter Chart**.
2. Add **Price** to the X-axis.
3. Add **Production Cost** to the Y-axis.
4. Add **Product Name** to **Values** (each product becomes a point).
5. Add **Product Name** to **Legend** (color-coded points).

![image.png](image%2035.png)

### **6. Donut & Pie Charts (Use with Caution)**

- **Best for** **showing parts of a whole**, but **not always the most readable**.
- **Difficult to compare segment sizes** accurately.

**Example: Purchases by State**

1. Select **Donut Chart**.
2. Add **State** to **Category**.
3. Add **Total Purchased** to **Values**.

**Why analysts avoid pie charts?**

- **Hard to distinguish slight differences in values**.
- **Bar charts and column charts are often better alternatives**.

![image.png](image%2036.png)

### **7. Card Visualization**

- **Best for** displaying **single summary values**.
- **Commonly used at the top of dashboards**.

**Example: Total Revenue**

1. Select **Card Visualization**.
2. Add **Total Purchased**.

**Use Case**: Shows **total sales, average revenue, or order count** in a **concise, prominent format**.

![image.png](image%2037.png)

### **8. Table Visualization**

- **Best for** displaying **detailed data in a structured format**.
- **Similar to Excel tables**, allowing for row-level analysis.

**Example: Customer Orders**

1. Select **Table Visualization**.
2. Add **Customer Name** and **Units Sold**.

**Use Case**: Ideal for **detailed reports** where users need **raw numbers**.

![image.png](image%2038.png)

### **Less Commonly Used Visualizations**

- **Area Charts** – Similar to line charts but shaded.
- **Maps** – Used when location-based data is involved.
- **Waterfall Charts** – Shows changes in a **measure over time** (e.g., profit/loss).
- **Tree Maps** – Similar to pie charts but rectangular.

**Tip**: Always **choose visualizations that improve readability and insight**.
