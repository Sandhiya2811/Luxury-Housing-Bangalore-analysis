# Luxury-Housing-Bangalore-analysis
## Project Documentation: Luxury Housing Bangalore
### Step 1: Load Raw Dataset
  •	File name: Luxury_Housing_Bangalore.csv
  •	Total rows in raw file: ~101,000
  •	Reason: First step in any project is to bring the raw data into Python (using Pandas). Only after loading, we can clean and process it.

### Step 2: Python — Data Cleaning & Feature Engineering
  We started with the raw file Luxury_Housing_Bangalore.csv (around 101,000 rows). Our goal was to prepare a clean dataset ready for database insertion and analysis.
  #### 1.	Remove Duplicates
  o	About 1,000 duplicate rows were found.
  o	These were deleted, leaving 100,000 unique rows.
  o	Reason: Duplicates give wrong results like inflated counts or revenue.
  #### 2.	Drop Unwanted Columns
  o	Columns such as Property_ID and Buyer_Comments were removed.
  o	Reason: These fields are not useful for analysis.
  #### 3.	Fix Inconsistent Formats
  o	Price column (Ticket_Price_Cr) had symbols like “₹” and “Cr”. These were removed, leaving only numeric values.
  o	Spelling mistakes in Configuration and Micro_Market were corrected.
  o	Reason: Clean formats are required for calculations and avoiding duplicate categories.
  #### 4.	Handle Missing Values
  o	Unit_Size_Sqft: Missing values filled with median size grouped by configuration.
  o	Ticket_Price_Cr: Missing values filled with mean price grouped by configuration.
  o	Amenity_Score: Missing values filled with median score grouped by developer.
  o	Reason: Null values disturb analysis. Filling with grouped median/mean keeps values realistic.
  #### 5.	Change Data Types
  o	Purchase_Quarter converted to proper datetime format.
  o	Reason: Date columns must be in datetime type to extract year, quarter, and trends.
  Feature Engineering (New Columns)
  We created new columns to help in analysis:
  •	Price_per_Sqft → Price per square foot. (Helps compare properties fairly.)
  •	Quarter_Number → Extracted quarter (1–4) from purchase date. (Helps check seasonal trends.)
  •	Booking_Status → 1 if booked (Primary), 0 if resale. (Helps measure booking success.)
  •	Year → Extracted purchase year. (For yearly trend analysis.)
  •	Year_Quarter → Combined Year + Quarter (e.g., 2023Q2). (For quarterly trend analysis.)
  #### Output 
  A cleaned dataset with consistent values, no duplicates, no nulls, and additional useful columns. Saved as a new CSV for further use.

### Step 3: SQL — Load Clean Data into PostgreSQL
  After cleaning, we moved the dataset into a SQL database for structured storage and analysis.
  #### 1.	Create Table Schema
  o	Defined column names and proper data types (e.g., numeric, text, date).
  o	Reason: Ensures clean and structured storage in PostgreSQL.
  #### 2.	Insert Data
  o	Loaded the cleaned dataset into PostgreSQL using Python.
  o	Reason: SQL is efficient for large datasets and integrates with BI tools like Power BI.
  #### 3.	Validation Queries
  o	Checked total row count (100,000).
  o	Grouped by booking status to confirm Primary vs Resale counts.
  o	Calculated average ticket price per developer.
  #### Output
  Data successfully stored in PostgreSQL, validated with queries, and ready for dashboards/insights.

### Step 4: Power BI — Connect to PostgreSQL and Load Data
  1. Opened Power BI Desktop.
  2. Went to Get Data and selected PostgreSQL Database.
  3. Entered server name, database name, username, and password.
  4. Selected the Luxury_House table (inserted in Step 2).
  5. Loaded the data into Power BI successfully.
  #### Output
  The Luxury_House dataset from PostgreSQL is now successfully loaded into Power BI.

### Step 5: Power BI — Visualization and Insights
  #### 1. Market Trends
    #### How we built it:
    •	Added Line Chart.
    •	X-axis: Quarter_Number or Year_Quarter.
    •	Y-axis: Booking Count (sum of Booking_Status).
    •	Legend: Micro_Market.
    #### Insight:
    •	Some micro-markets show steady growth in bookings, while others fluctuate.
    •	Helps identify booming areas quarter by quarter.
  
  #### 2. Builder Performance
    #### How we built it:
    •	Added Bar Chart or Table.
    •	Fields: Developer_Name, Sum(Ticket_Price_Cr), Avg(Ticket_Price_Cr).
    #### Insight:
    •	Shows which builders have the highest sales revenue.
    •	Comparison of revenue vs average ticket size highlights premium vs mid-range builders.
  
  #### 3. Amenity Impact
    #### How we built it:
    •	Added Scatter Plot.
    •	X-axis: Amenity_Score.
    •	Y-axis: Booking Conversion Rate (successful bookings / total listings).
    •	Bubble Size: Project Count.
    #### Insight:
    •	Higher amenity scores generally improve booking chances.
    •	Few exceptions highlight cases where price or location dominates.
  
  #### 4. Booking Conversion by Micro-Market
    #### How we built it:
    •	Added Stacked Column Chart.
    •	X-axis: Micro_Market.
    •	Y-axis: Booking Status (as percentage).
    #### Insight:
    •	Some micro-markets have high conversion rates (buyers finalize deals quickly).
    •	Others show low conversion due to high prices or poor infrastructure.
  
  #### 5. Configuration Demand
  How we built it:
  •	Added Pie Chart (or Donut Chart).
  •	Fields: Configuration vs Booking Count.
  Insight:
  •	3BHK and 4BHK dominate demand.
  •	Niche demand for 2BHK (budget buyers) and 5BHK (luxury premium segment).
  
  #### 6. Sales Channel Efficiency
  How we built it:
  •	Added 100% Stacked Column Chart.
  •	X-axis: Sales_Channel.
  •	Y-axis: Booking_Status distribution.
  Insight:
  •	Certain channels (e.g., Online/Direct Sales) perform better than brokers.
  •	Developers can invest more in the most efficient sales channels.
  
  #### 7. Quarterly Builder Contribution
  How we built it:
  •	Added Matrix Table.
  •	Rows: Developer_Name.
  •	Columns: Year_Quarter.
  •	Values: Sum(Ticket_Price_Cr).
  Insight:
  •	Reveals builder dominance by quarter.
  •	Helps spot seasonal patterns and consistent performers.
  
  #### 8. Possession Status Analysis
  How we built it:
  •	Added Clustered Column Chart.
  •	X-axis: Possession_Status (Ready vs Under Construction).
  •	Y-axis: Booking_Status.
  •	Legend: Buyer_Type.
  Insight:
  •	Ready-to-move properties attract NRI and end-user buyers.
  •	Under-construction projects are popular with investors.
  
  #### 9. Geographical Insights
  How we built it:
  •	Used Map Visualization.
  •	Location: Micro_Market (or lat/long if available).
  •	Size: Sum of Booking Count or Revenue.
  Insight:
  •	Certain zones of Bangalore show dense luxury housing projects.
  •	Investors can focus on hotspots with strong demand.
  #### 10. Top Performers (Matrix Table)
  How we built it:
  •	Matrix Table created.
  •	Rows: Developer_Name.
  •	Values: Successful Booking Count and Total Revenue.
  Insight:
  •	Top 5 builders contribute the largest share of market revenue.
  •	They also maintain high booking success, proving strong brand reputation.
