# eCommerce Sales Analysis Dashboard
![MainOverview](/Images/MainOverview.png)

## Introduction

This interactive dashboard presents insights derived from eCommerce transaction data sourced from Kaggle, covering the period from August 2022 to August 2025 across ten countries. It provides a comprehensive view of sales performance segmented by country, age group, customer demographics, product categories, and individual products.
A key focus of the analysis is the financial impact of cancelled and returned orders on overall sales. While the dashboard highlights top performing segments, it also surfaces areas of concern particularly the volume of lost revenue due to order reversals. These insights underscore the need for targeted interventions to reduce return rates and improve customer satisfaction.
This tool is designed to support data-driven decision-making by offering a clear, actionable view of sales dynamics and operational inefficiencies.


## Skills Used
**Power Query Editor**: Used the query editor to create `DateTable`:= List.Dates(#date(2022,8,25),1094,#duration(1,0,0,0)),
`Full Name` : Text.Start([first_name],1)&" "&[last_name],
 grouping data, shaping, and cleaning data

**Explicit Measures**: Formulated measures to derive key insights and KPIs as follows:
- `Total Sales`:Total Sales = SUM(eCommerceData[Amount Paid])
- `Total Orders`:Total Orders = COUNTROWS(eCommerceData)
- `Total Customers`: Total Customers = DISTINCTCOUNT(eCommerceData[customer_id])
- `Vs Last Month`: To calculate last month sales as follows: Vs Last Month = 
VAR _cm = [Total Sales]
VAR _pv = 
CALCULATE(
    [Total Sales],
    DATEADD('DateTable'[Date],-1,MONTH))
    VAR _perc = 
    DIVIDE(_cm-_pv,_pv)
    VAR _format = 
    SWITCH(
        TRUE(),
        _perc>0, UNICHAR(11165)& " " & FORMAT(_perc,"0.0%"),
        _perc<0, UNICHAR(11167)& " " & FORMAT(_perc*-1,"0.0%"),
         FORMAT(_perc,"0.0%")
    )
    RETURN
    _format
- `Vs Last Year`: To calculate last year sales as follows: Vs Last Year = 
VAR _cm = [Total Sales]
VAR _pv = 
CALCULATE(
    [Total Sales],
    DATEADD('DateTable'[Date],-1,YEAR))
    VAR _perc = 
    DIVIDE(_cm-_pv,_pv)
    VAR _format = 
    SWITCH(
        TRUE(),
        _perc>0, UNICHAR(11165)& " " & FORMAT(_perc,"0.0%"),
        _perc<0, UNICHAR(11167)& " " & FORMAT(_perc*-1,"0.0%"),
         FORMAT(_perc,"0.0%")
    )
    RETURN
    _format
- `CF Last Month` To conditional format arrows and text used for the dynamic KPI cards: CF Last Month = 
VAR _cm = [Total Sales]
VAR _pv = 
CALCULATE(
    [Total Sales],
    DATEADD('DateTable'[Date],-1,MONTH))
    VAR _perc = 
    DIVIDE(_cm-_pv,_pv)
    VAR _format = 
    SWITCH(
        TRUE(),
        _perc>0, "Green",
        _perc<0, "Dark Red",
         "Grey"
    )
    RETURN
    _format

**Bookmarks:**
Used to capture the available order status: *delivered*, 
![DeliveredView](/Images/Delivered%20View.png)

*pending* 
![Pending View](/Images/Pending%20View.png)

and *cancelled*
![CancelledView](/Images/CancelledView.png)

**Drillthrough:**
*Country details*
![CountryDetails](/Images/DrillThroughView.png)

 and *Customer details*
![CustomerDetails](/Images/CustomerDrillThrough.png)

**KPI Visuals:**
*Total sales, customers and orders*
![Summary KPI](/Images/Summary%20KPI.png)

*current sales vs Last Month and Vs Last Year*
![KPI LM LY](/Images/KPI%20LM%20LY.png)

To show *Total sales, customers, and orders*. Also used KPI visuals to compare *current sales vs Last Month and Vs Last Year*
**Line Chart:**To show the total sales trends over time
**Bar Chart:** to show *totals sales by country, age group, customers, categories, products*
**Pie Chart:** to show percentage total contribution to the total sales
![OrderStatusView](/Images/OrderStatusview.png)

## Conclusion 
Based on the aggregated sales data across all regions, the Electronics category emerged as the top-performing segment, with the iPhone 14 leading as the most purchased product globally. Demographic analysis indicates that the majority of our customer base falls within the adult age group, suggesting strong engagement from this segment.
While total sales reached R7.4 million, it's notable that R2.8 million over 38% of revenue was lost due to order cancellations and product returns. This represents a significant leakage in potential revenue and warrants further investigation. Understanding the underlying causes—whether related to product issues, delivery delays, customer expectations, or other factors—will be critical to improving retention and reducing future losses.


