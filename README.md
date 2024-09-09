# Data-Analytics-Power-BI-Report
Documentation for Power BI Report Setup
Date Table Creation
Create a Continuous Date Table:

Cover the period from the earliest Orders[Order Date] to the latest Orders[Shipping Date].
Use any preferred DAX formula to generate this table.
Add Columns to the Date Table:

Day of Week: FORMAT([Date], "dddd")
Month Number: MONTH([Date])
Month Name: FORMAT([Date], "MMMM")
Quarter: QUARTER([Date])
Year: YEAR([Date])
Start of Year: DATE(YEAR([Date]), 1, 1)
Start of Quarter: DATE(YEAR([Date]), QUARTER([Date])*3-2, 1)
Start of Month: DATE(YEAR([Date]), MONTH([Date]), 1)
Start of Week: DATEADD([Date], -WEEKDAY([Date], 2)+1, DAY)
Relationships
Define Relationships:
Products[product_code] to Orders[product_code]
Stores[store code] to Orders[Store Code]
Customers[User UUID] to Orders[User ID]
Date[date] to Orders[Order Date] (Active Relationship)
Date[date] to Orders[Shipping Date]
All relationships are one-to-many with a single filter direction from dimension to fact tables.
Measures Table
Create a Measures Table:

In the Model view, select Enter Data and create a table named Measures Table.
Define Key Measures:

Total Orders: COUNTROWS(Orders)
Total Revenue: SUMX(Orders, Orders[Product Quantity] * RELATED(Products[Sale_Price]))
Total Profit: SUMX(Orders, (RELATED(Products[Sale_Price]) - RELATED(Products[Cost_Price])) * Orders[Product Quantity])
Total Customers: DISTINCTCOUNT(Orders[User ID])
Total Quantity: SUM(Orders[Product Quantity])
Profit YTD: TOTALYTD([Total Profit], Date[date])
Revenue YTD: TOTALYTD([Total Revenue], Date[date])
Hierarchies
Date Hierarchy:

Levels: Start of Year, Start of Quarter, Start of Month, Start of Week, Date
Geography Hierarchy:

Country Column:

DAX
Copy code
IF([Country Code] = "GB", "United Kingdom",
IF([Country Code] = "US", "United States",
IF([Country Code] = "DE", "Germany")))
Geography Column:

DAX
Copy code
[Country Region] & ", " & [Country]
Levels: World Region, Country, Country Region

Report Pages
Create Report Pages:

Executive Summary
Customer Detail
Product Detail
Stores Map
Add Navigation Buttons:

Use white icons for default and cyan for hover.
Set actions for page navigation and group buttons for ease of use.
Visuals Setup
Executive Summary Page:

Add card visuals for Total Revenue, Total Orders, and Total Profit.
Create and format visual elements including donut charts, line charts, and KPIs.
Add gauges and placeholder shapes for slicer states.
Configure slicers and bookmarks for a dynamic user interface.
Customer Detail Page:

Include card visuals, donut charts, line charts, and tables.
Set up filters and slicers for detailed customer insights.
Product Detail Page:

Configure scatter charts, donut charts, and top products table.
Adjust visual interactions and filtering.
Stores Map Page:

Add a map visual with custom tooltip functionality.
Implement slicers for filtering by country.
Stores Drillthrough Page:

Set up drillthrough functionality and add detailed performance visuals.
Custom Tooltips and Interactions
Tooltips:

Create a custom tooltip page and configure it to display year-to-date profit performance on hover.
Interactions:

Adjust visual interactions per page as specified for effective filtering and cross-filtering.
Final Steps
Update Documentation:

