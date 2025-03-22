# blinkit_grocery_data
#1. Find the total sales for each outlet
#Identify which outlet generates the highest total sales.

	select outlet_identifier, sum(sales) total_sales from grocery_data
    group by outlet_identifier
    order by total_sales;

#2. Identify the top 5 best-selling products
#Find the highest-selling products based on total revenue.

	select item_identifier, item_type, sum(sales) total_sales from grocery_data
	group by item_identifier, item_type
	order by total_sales
	limit 5 ;

#3. Analyze sales trends over the years
#Observe how sales vary based on the year the outlet was established.

	select outlet_establishment_year, sum(sales) as total_sales from grocery_data
	group by outlet_establishment_year  
	order by outlet_establishment_year;

#4. Find the contribution of each product category to total sales
#Determine which product category generates the highest revenue.

	select item_type, sum(sales) as total_sales from grocery_data 
	group by item_type
	order by total_sales desc
	limit 5;

#5. Calculate the average sales by outlet type
#Compare the average sales performance of different types of outlets.

	select outlet_type, avg(sales) avg_sales from grocery_data
	group by outlet_type;

#6. Identify underperforming outlets (Sales below average)
#Find outlets whose total sales are below the overall average.

	
	SELECT Outlet_Identifier, SUM(Sales) AS Total_Sales
	FROM Grocery_Data
	GROUP BY Outlet_Identifier
	HAVING avg(Sales) < (SELECT AVG(Sales) FROM Grocery_Data)
	order by total_sales ;

#7. Find the most frequently sold product
#Identify the most popular product based on the number of times it appears in transactions.

	select item_identifier, count(*) as product_count from grocery_data
	group by item_identifier
	order by product_count desc
	limit 1
	;

# 8. Identify the most profitable store location
# Compare sales across different store locations to find the best-performing location type.

	select outlet_location_type, sum(sales) total_sales_across_store_location from grocery_data
	group by outlet_location_type
	order by total_sales_across_store_location;

#9. Analyze the relationship between product ratings and sales
#Determine whether higher-rated products have higher sales.

	select rating,sum(sales) as total_sales from grocery_data
	group by rating
	order by rating desc;

#10. Count the number of missing values in the Item Weight column
#Find out how many products have missing weight data.

	select count(*) as missing_weight from grocery_data 
	where item_weight is null;
