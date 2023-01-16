# AW-Saless-Power-BI-Project-1
Adventure Works Sale Reports Using Power BI
All Measure for AW Sale Reports

1. # of Product = COUNTROWS('d-Products')
2. Total Order Qty = SUM('f-Sales'[OrderQuantity])
3. Total # of Orders = DISTINCTCOUNT('f-Sales'[OrderNumber])
4. All Orders = CALCULATE([Total # of Orders],ALL('f-Sales'))
5. % of All Orders = DIVIDE([Total # of Orders],[All Orders],0)
6. Total Return Qty = SUM('f-Returns'[ReturnQuantity])
7. All Returns Qty = CALCULATE([Total Return Qty],ALL('f-Returns'))
8. % All Return Qty = DIVIDE([Total Return Qty],[All Returns Qty],0)
9. All Product Avg Price = CALCULATE(AVERAGE('d-Products'[ProductPrice]),ALL('d-Products'))
10. Bikes Sold LY = 
    var
        bikes = FILTER('d-ProductCategories','d-ProductCategories'[Category Name] = "Bikes")
    var
        ly = SAMEPERIODLASTYEAR('d-Calendar'[Date])
    return
        CALCULATE([Total # of Orders],bikes,ly)
11. Clothing Orders = CALCULATE([Total # of Orders],'d-ProductCategories'[Category Name] = "Clothing")
12. Country Wise Customer Avg Income = CALCULATE(AVERAGE('d-Customers'[AnnualIncome]),CROSSFILTER('d-Customers'[CustomerKey],'f-Sales'[CustomerKey],Both))
13. High price Points = CALCULATE([# of Product],'d-Products'[Price Point] = "high")
14. High Value Orders = CALCULATE([Total # of Orders],FILTER('d-Products','d-Products'[ProductPrice]>[All Product Avg Price]))
15. Max Revenue = MAXX('f-Sales','f-Sales'[OrderQuantity]*RELATED('d-Products'[ProductPrice]))
16. Min Revenue = MINX('f-Sales','f-Sales'[OrderQuantity]*RELATED('d-Products'[ProductPrice]))
17. Revenue = SUMX('f-Sales','f-Sales'[OrderQuantity]*RELATED('d-Products'[ProductPrice]))
18. Total Cost = SUMX('f-Sales','f-Sales'[OrderQuantity]*RELATED('d-Products'[ProductCost]))
19. Profit = [Revenue]-[Total Cost]
20. Pre. Month Return Quantity = CALCULATE([Total Return Qty],DATEADD('d-Calendar'[Date],-1,MONTH))
21. Pre. Month Revenue = CALCULATE([Revenue],DATEADD('d-Calendar'[Date],-1,MONTH))
22. Previous Montrh Order Qty = CALCULATE([Total Order Qty],DATEADD('d-Calendar'[Date],-1,MONTH))
23. Previous Year Revenue = CALCULATE([Revenue],DATEADD('d-Calendar'[Date],-1,YEAR))
22. Prevoius Month Revenue = CALCULATE([Revenue],PREVIOUSMONTH('d-Calendar'[Date]))
25. Return Rate = DIVIDE([Total Return Qty],[Total Order Qty],0)
26. Selected Year = "Revenue by Category for " & SELECTEDVALUE('d-Calendar'[Year],"all years")
27. Target Order Qty = [Previous Montrh Order Qty]*1.02
28. Target Revenue = [Prevoius Month Revenue]*1.02
29. Weekend Ordders = CALCULATE([Total # of Orders],'d-Calendar'[Weekend]="yes")
30. YoY % Revenue Growth = DIVIDE(([Revenue]-[Previous Year Revenue]),[Previous Year Revenue],0)
31. YTD Revenue = CALCULATE([Revenue],DATESYTD('d-Calendar'[Date]))
