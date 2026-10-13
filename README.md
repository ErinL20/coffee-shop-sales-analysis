# Coffee Shop Sales & Operations Analysis

## Summary
This project analyzes transaction data for a local coffee shop to identify sales trends, evaluate menu item performance, and highlight ingredient inventory and cost management.

- Timing & Marketing Strategy-:
  Wednesdays experience the lowest transaction volume. Recommend testing promotions (e.g., a mid-week BOGO or double loyalty points) to     drive traffic on that day.
  
- Product Performance-: Revenue is heavily driven by cold specialty beverages—led mostly by Cold Mocha—making iced drinks our primary drivers.
  
- Operations & Inventory-: Cold Mocha being in high demand places Cocoa Powder at high risk of depletion during peak hours. In addition, Ham represents our highest overall ingredient expense.

## SQL Queries Used

1. Total Items Sold by Day of the Week
   ``` sql
     SELECT
 	 CASE strftime ('%w', created_at)
    	when '0' Then 'Sunday'
        when '1' then 'Monday'
        WHEN '2' THEN 'Tuesday'
        WHEN '3' THEN 'Wednesday'
        when '4' then 'Thursday'
        WHEN '5' then 'Friday'
        when '6' then 'Saturday'
     end as day_of_the_week,
    count (*) as total_items_sold
    FROM orders
 
 group by date (created_at)
order by total_items_sold asc
;
```

2. Total Sales by Item
   ``` sql
   SELECT item_price, SUM(item_price) as total_price, item_name, 
   count (*) as total_items_sold
    FROM orders
 
inner JOIN items
	On orders.item_id = items.item_id
    
group by item_name
order by total_items_sold DESC
;
```

3. Total Ingredient Cost
``` sql
SELECT ing_name, ing_price
from ingredients

order by ing_price DESC
;
```
