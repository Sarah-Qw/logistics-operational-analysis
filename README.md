# (Bosta) Logistics & Shipping Data Analysis

## Overview
Analyzed a logistics company's shipment data covering nearly 1 million records across 12 months. The entire project was built in Excel using Power Query to merge and clean the data, Power Pivot to organize the tables, and DAX to calculate key performance numbers.

## Questions Answered
- How does shipment volume change month to month?
- Which cities send and receive the most shipments?
- Which shipping carriers are the most profitable?
- What is the average shipping cost for each destination?
- Which product categories are shipped the most?
- How does profit break down by product category?
  
## Tools Used
- Excel: Main workspace for the entire project.
- Power Query: Merged 12 monthly files and cleaned all tables.
- Power Pivot: Organized tables into a Star Schema and managed relationships.
- DAX: Built measures for Total Orders, Net Profit, and Average Shipping Cost.

## What I Did
1. Merged the Data (Power Query)
- Put all 12 monthly CSV files in one folder.
- Used Get Data > From Folder to automatically stack them into one table.
- Imported 3 additional tables (Customers, Products, Carriers) for context.

2. Cleaned the Data (Power Query)
This was the heaviest part of the project. The data had many issues:

Orders Table:
- Changed the date column from date-and-time to date-only so it works with the calendar table.
- City names had typos, abbreviations, and extra spaces. Used Trim, Clean, and custom rules in M Code to fix them (for example: "Alex" became "Alexandria", "Sharm" became "Sharm El-Sheikh").
- Filled in missing values for distance (with the average: 391 km), quantity (average: 4), weight, shipping fees, and operational costs.
- Removed the text "kg" and "EGP" that was stuck inside number columns so Excel could read them as numbers.
- Found negative costs (which make no sense) and converted them to positive using absolute value.
- Fixed extra spaces in the Status column that were creating fake duplicate categories.

Other Tables (Carriers, Customers, Products):
- Applied the same text cleaning (Trim, Clean, Capitalize).
- Fixed city name abbreviations using custom rules.
- Unified product category names that had different spellings.
- Replaced all empty cells with "N/A" so nothing shows up blank in the dashboard.

3. Built the Data Model (Power Pivot)
- Organized all tables into a Star Schema: Orders in the center, connected to Customers, Products, Carriers, and a Calendar table.
- All connections are one-to-many, flowing from the dimension tables to the Orders table.
- Loaded everything as Connection Only with Add to Data Model to keep the file fast and light.

4. Created Measures (DAX)
- Total Orders: counts all shipment records.
- Total Shipping Fees: total revenue from shipping charges.
- Total Cost: total operational expenses.
- Net Profit: revenue minus costs.
- Average Shipping Cost: average cost per single shipment.

5. Analyzed the Data (Pivot Tables)
- Built separate pivot tables for each business question.
- Used multiple filters on the same field (Label Filter to exclude unknowns + Value Filter to get Top 10) to rank the best carriers by profit.
