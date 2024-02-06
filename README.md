# Amazon_Sales_Analytics
## Analysis of Amazon Sales(Year:2015-2017) through PowerBI.
1. About the data
   - The data consists of sales made by Amazon from 2015 to 2017.
   - Other data include calendar, customer information, category and subcategory of the products that were sold, price of the products, return information of the products, territory information about sales
2. Different measures were created as needed for the project, mentioned so you can create one according to your needs.
   ```
      PowerBI
      Total cost = Sum(AM_Sales[Purchase cost])
   ```
   ```
      Total Orders = DISTINCTCOUNT(AM_Sales[OrderNumber])
   ```
   ```
      Total Price = SUM(AM_Sales[Purchase Price])
   ```
   ```
     Total Profit = Sum(AM_Sales[OrderQuantity])*[Total Price]-[Total cost]
   ```
   ```
      YTD sales Profit = CALCULATE([Total Profit],DATESYTD(Amazon_Calendar[Date]))
   ```
   ```
      Prev Month Sales = CALCULATE([Total Profit],DATEADD(Amazon_Calendar[Date],-1,MONTH))
   ```
   ```
      High Ticket order = CALCULATE([Total Orders],FILTER(Amazon_Products,Amazon_Products[ProductPrice]>[Overrall retail price1]))
   ```
   ```
      Dynamic Profit/loss target = 
   IF(
    SELECTEDVALUE(Profit_loss_toggle[Values])="Profit",
    [Profit Target],
    [Opportunity Lost Target])
   ```
   ```
     Dynamic Profit/Loss = 
      IF(
    SELECTEDVALUE(Profit_loss_toggle[Values])="Profit",
    [Total Profit],[Opportunity lost]
      )
   ```
   ```
      Bulk order = CALCULATE([Total Orders],AM_Sales[OrderQuantity]>1)
   ```
   ```
      Profit Target = [Prev Month Sales]*1.1
   ```
   ```
      YTD sales Profit = CALCULATE([Total Profit],DATESYTD(Amazon_Calendar[Date]))
   ```
   ```
      Age = DATEDIFF(Amazon_Customers[BirthDate],TODAY(),YEAR) 
   ```
   ```
      BIRTH YEAR = YEAR(Amazon_Customers[BirthDate]) 
   ```
   ```
      Full Name = Amazon_Customers[FirstName]&" "&Amazon_Customers[LastName]
   ```
    ```
      Parent = IF(Amazon_Customers[TotalChildren]>0,"Yes","No") 
   ```
    ```
     Avg Retail Price = AVERAGE(Amazon_Products[ProductPrice])
   ```
   ```
      Overrall retail price1 = CALCULATE([Avg Retail Price],ALL(Amazon_Products))
   ```
   ```
      Opportunity lost = 
      var Price_r=SUM(Amazon_Returns[Return Price])
      var Cost_r=SUM(Amazon_Returns[Return Cost])
      var Quantity_r=SUM(Amazon_Returns[ReturnQuantity])
      return (Price_r-Cost_r)*Quantity_r
   ```
   ```
      Opportunity Lost Target = [Prev Month Opportunity lost]*0.9
   ```
   ```
      Prev Month Opportunity lost = CALCULATE([Opportunity lost],DATEADD(Amazon_Calendar[Date],-1,MONTH))
   ```
   ```
     prev month orders = CALCULATE([Total Orders],DATEADD(Amazon_Calendar[Date],-1,MONTH))
   ```
   ```
      prev month returns = CALCULATE([Total Returns],DATEADD(Amazon_Calendar[Date],-1,MONTH))
   ```
   ```
      Return Cost = RELATED(Amazon_Products[ProductCost])
      Return Price = Related(Amazon_Products[ProductPrice])
   ```
   ```
      Return rate = DIVIDE(SUM(Amazon_Returns[ReturnQuantity]),SUM(AM_Sales[OrderQuantity]),"No sales")
   ```
   ```
      Total Returns = Sum(Amazon_Returns[ReturnQuantity])
   ```
## Toggle 
For creating a toggle between profit and loss, there's a new table added to the data with profit and loss as row values with the column being 'values.'
#Visualization
## Page1
On this page, you can see
1. Table: showing the customer's full names with the total profit they contributed
2. Table 2: product key with opportunity lost information
3. Table 3: This table shows category names along with the model name and the total no of orders with a dynamic profit/loss column and return rate
   - The profit/opportunity loss toggle affects only Table 3 where, whereas the month and year slicer affects all the tables on the page. You can change this by selecting the filter you want and going to format-->edit interactions--> Now, on every table, you can see three options: select/deselect the rightmost one whether you want this filter to affect this table or not. 
## Page2
On this page, you can see
Concentration on product information
1. Total orders based on category name, sub-category name and product distribution by profit/loss
2. Total profit, total orders and total returns for the month and year are chosen, and the goal in this visual indicates if the sales for this month are met or not
3. Top  3 performers/losers products and the orders from different territories of the world
- To get the filter page ctrl+left click you will get the filter page to change month and year, to go back ctrl+left click outside that page
 


