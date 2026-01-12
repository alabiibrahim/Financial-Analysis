# Financial-Analysis


# Plant Co. Global Performance

![GIF](Images/PlanGIF.gif)

##   Table of Contents

- [Project brief](#Projectbrief)
- [Data Architecture](#DataArchitecture)
- [Questions](#Questions)
- [Data source](#Datasource)
- [Tools](#Tools)
- [Dashboards](#Dashboard)
- [Chart types and why](#ChartTypesandWhy?)
- [Stages](#Stages)
- [Data Transformation](#DataTransformation)
- [Findings](#Findings)
- [Recommendations](#Recommendations)
- [challenges&solution](#Chalenges&Solution)



## Project brief 

This project features a 3 page, interactive Power BI dashboard designed for Plant Co. to monitor global performance across three key business pillars: Sales, Quantity, and Gross Profit.

The dashboard provides a detailed breakdown experience, allowing stakeholders to identify not just what happened in 2023, but why it happened by comparing Year-to-Date (YTD) performance against the Previous Year (PYTD).


## Data Architecture 

![DataModeling](Images/Data%20Modeling.PNG)

This project is built on a Star Schema architecture, optimized for analytical performance, scalable reporting, and reliable DAX calculations in Power BI.

- Fact Table: contains transactional sales data acting as a central table connecting all business dimensions with key metrics (Quantity, Sales, COGs). 

- Plant_Products Table: This here contains the product attributes and hierarchy to help in analysis with product size, type, group e.t.c

- Accounts Table: Contains customer and account information includes geographic and location for regional a nalysis.

- Calendar Table: Created to help in time intelligence analysis. It helps in calculating YTD, PYTD and SAMEPERIODLASTYEAR.

- Measures Table: This is not connected to other table but used for all DAX measures to help in reusability, readability.

- Slic_Values: This is also diconnected from other tables. It helps in calculating dynamic slicers measures and a conditional measures.Also, this slicers is not connected intentionally as to be flexible.


### Benefit of data modeling

- Improves query performance and report responsiveness

- Simplifies DAX logic by enforcing a single-direction filter flow

- Ensures accurate time-intelligence calculations

- Follows industry best practices for Power BI and enterprise BI solutions.


## Questions
 Overall Performance & Growth: Is Plant Co. growing or shrinking?

- How did our 2023 YTD Sales perform compared to the same period last year?What is the exact dollar value of our performance gap?

- Are we selling more but making less? Is our Gross Profit margin of stable, or has it eroded since the previous year?

- Which customers are our Whales (High Volume/High Profit versus our Resource Drainers (High Volume/Low Profit)?

- Which accounts are falling below our profitability threshold?

- Which product segment is responsible for the largest profit decline?

- We sold 17K more units this year—why didn't our revenue increase accordingly?

- Which global regions are currently our strongest growth engines?

- In which specific months did we lose our momentum?


## Data Source

![Data](https://github.com/alabiibrahim/Plant-Co.-Global-Performance/blob/main/Datasets/Plant%20co.DTS.xls)

## Tools

| Tools | Purpose | 
| --- | --- | 
| Power BI | DAX, Power Query | 


## Stages 
- Load data to Power Query, Standardize data-types and remove duplicates.
- Create a 'calendar' table and toggle button to view across 3 pillars of business. (Quantity, Sales and Gross Profit).
- Data modeling. Create DAX measures. 


## Chart types and Why? 

- Card Visuals - Shows the KPIs metrics (YTD, PYTD and GP%), and also the dynamic report title.

- Scatter Charts - Shows accouint segmentation by GP % vs Sales. This allows stakeholders to identify high-volume, low-margin "risk" accounts versus high-margin "premium" accounts.

- Waterfall charts - Shows the "YTD vs PYTD" comparison by Month, to provide a clear narrative of seasonal fluctuations.

- Map - Shows the global YTD Sales, Quantity and GP %  by country, providing a spatial understanding of the company's market footprint.

- Stacked Bar chart - Helps show the break down performance by product type (Indoor, Landscape, Outdoor).

- Column chart - Display the breakdown performance by Product Size (Small, Medium, Large)


## Dashboard
 
 This dashboard allows the Sales Director to pivot from 'General Observation' to 'Targeted Action' for example, specifically investigating the November slump or renegotiating low-margin accounts identified in the scatter plot.

![Dashboard](Images/F1.PNG)

![Dashboard](Images/f2.PNG)

![Dashboard](Images/F3.PNG)


## Data Transformation

Here are the DAX formulas used in this project:

- Sales = SUM('Fact'[Sales_USD])
        - This measure total all sales values from the Fact table.  

- Qty = SUM('Fact'[Quantity])
        - This measure total all quantity from the Fact table.

- COGs = SUM('Fact'[COGS_USD])
        - This measure total the Cost of Good sold from the Fact table  

- GrossProfit = COGs - Sales
        - This measure subtract the COGs from Sales to get the Gross Profit.

- YTD Sales = TOTALYTD('Measures'[Sales], 'Calendar'[Date]) 
        - This measure is used to calculate the YTD sales, quantity, and gross profit from the start of the year to the end. 

- PYTD Sales = CALCULATE([YTDSales], SAMEPERIODLASTYEAR('Calendar'[Date]))
      - This measure is used to calculate the YoY comparison of sales, quantity, and gross profit. Just as seen in the waterfall chart.

- GP% = DIVIDE([GrossProfit], [Sales])
        - This measure is used to calculate the GP %. 


## Findings

1. 86.2% of all loans are "Good Loans" (Fully Paid or Current), totaling $370.2M in funded value.

2. Most borrowers are highly stable, with 10+ years of employment history and living in rented or mortgaged homes.

3. Debt Consolidation is by far the most common reason people apply for loans, followed by Credit Card payments.

4. There is a clear upward trend in loan applications from the start of the year toward the end (peaking in December).

5. About 13.8% of loans are "Bad Loans" (Charged Off), which represents roughly $65.5M in total funded amount.


## Recommendations

1. Create marketing campaigns specifically for employees with 10+ years of experience, as they are your most active and reliable customers.

2. Since this is the #1 loan purpose, offer a streamlined "Express" approval process for debt consolidation to capture more market share.

3. Focus marketing spend on California (CA), Texas (TX), and New York (NY), as these states show the highest demand and volume.

4. Investigate the "60-month" loan terms more closely; longer terms often carry higher risks. Consider stricter credit requirements for 5-year loans.


## Challenges & Solution 

1. The stakeholders needed to see Sales, Quantity, and Gross Profit performance, but putting all three on one page created a cluttered and "noisy" dashboard that was hard to read.

    - How I solved it: I created a "Slicer Table" for easy toggling between 3 key pillars of business using DAX. This allowed the user to switch the entire context of the page with one click, maintaining a clean and simple report while providing three times the analytical depth.


2. Standard YTD functions can sometimes fail if the fiscal calendar is non-standard or if there are gaps in the data, leading to misleading variance figures.

    - How I solved it: I created a Date Table and utilized SAMEPERIODLASTYEAR combined with TOTALYTD logic to ensure the waterfall charts accurately show comparisons for the $512K sales variance.


3. With hundreds of accounts, a standard bar chart was insufficient for identifying profitability outliers.

    - How I solved it: I used a Scatter Plot with a Profitability Quadrant. By adding a constant line at the 20K sales mark and a GP% axis, I created an instant visual diagnostic tool to separate "High-Volume/Low-Margin" accounts from "Premium" partners.




