
**Case Study - Restaurant Sales Analysis - MYSQL**

**Introduction :**

This project involved analyzing a dataset of restaurant sales to identify trends, optimize operations, and increase revenue.
The project focused on understanding factors such as sales order, periods, customer preferences 



**Technology Used :**

* MYSQL


**Objective 1**

**EXPLORE THE ITEMS TABLE :**

1. View the Menu_items Table 


      ANS :   select * from menu_items;

![image](https://github.com/user-attachments/assets/26186ea1-ac81-4318-8587-77821bcebe7e)


2. write a query to find the number of items on the menu

       ANS : select count(*) menu_item_id from menu_items;


![image](https://github.com/user-attachments/assets/3cd42fdd-97a8-44dd-8677-37da70e46fd8)


3. What are the least expensive items on the menu?

        ANS :    select * from menu_items order by price;


![image](https://github.com/user-attachments/assets/21571de5-75b0-45a2-ba84-e71ba4600d56)

4. What are the Most expensive items on the menu?

         ANS : select * from menu_items order by price desc;
        
![image](https://github.com/user-attachments/assets/70df181f-5508-45b6-bde9-e98fb4f42ba5)



5. How many Italian dishes are on the menu? 

         ANS :  select count(*) from menu_items where category = "Italian";

![image](https://github.com/user-attachments/assets/bc92d12b-2a9a-4eff-8f62-a767a347d6e5)


6. What are the least  expensive Italian dishes on the menu?

        ANS : select * from menu_items where category = "Italian" order by price ;

![image](https://github.com/user-attachments/assets/45cf4a19-098d-4bc6-9145-ef02f4a27175)


7. What are the Most expensive Italian dishes on the menu?

       ANS : select * from menu_items where category = "Italian" order by price DESC ;

![image](https://github.com/user-attachments/assets/546ab5d8-5fee-4de7-815b-17621f68ee8d)

8. How many dishes are in each category?

      ANS : select count(item_name) as No_dish , category from menu_items group by category ;


![image](https://github.com/user-attachments/assets/a8ba6987-4383-46b3-a4ee-ca3eeb6257cc)


9. What is the average dish price within each category?

     ANS : select category, avg(price) as Avg_price
      from menu_items 
      group by category 

![image](https://github.com/user-attachments/assets/864cfeae-e7a1-4c5a-8596-6b83f88ed206)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**EXPLORE THE ORDER TABLE :**

**1. View the order_details table**

          ANS : select * 
          from order_details;


![image](https://github.com/user-attachments/assets/0269de60-fe97-4150-82c8-65d36caf2184)


**2. What is the date range of the table?**

         Ans : select min(order_date) , max(order_date)
        from order_details;

![image](https://github.com/user-attachments/assets/d0be658f-6a12-41c9-b1aa-48db4362dd21)


**3. How many orders were made within this date range?** 
 
         ANS : select  count(distinct order_id) from order_details;


![image](https://github.com/user-attachments/assets/6d39916c-4392-4012-b07e-be40654e028d)

**4. How many items were ordered within this date range?**

         ANS : select  count(*) from order_details;

![image](https://github.com/user-attachments/assets/bb1436ba-b93e-4024-957e-8be5f9cea8d3)


**5. Which orders had the most number of items?**

           ANS : select order_id, 
           count(item_id) as num_items 
           from order_details
           group by order_id
           order by num_items Desc;

![image](https://github.com/user-attachments/assets/fe3daf22-66e1-4a79-b526-120bf25c1ba7)


**6. How many orders had more than 12 items?**

          ANS:  select count(*) 
          from
          (select order_id, count(item_id) as num_items 
          from  order_details 
          group by order_id
          having num_items > 12) as num_orders;

![image](https://github.com/user-attachments/assets/c6e2560c-07ea-481a-8d82-3219aabef054)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------


**ANALYZE CUSTOMER BEHAVIOUR :**

**1. Combine the menu_items and order_details tables into a single table**

         ANS : select * 
        from   order_details o
        left join menu_items m on o.item_id = m.menu_item_id;

![image](https://github.com/user-attachments/assets/07249aa7-d534-4ec6-8b32-d56736a2f17c)

2. What were the least ordered items? 

         ANS : select item_name, 
         category, 
         count(order_details_id) as tot_orders
         from order_details o
        left join menu_items m on o.item_id = m.menu_item_id
        group by item_name, category
        order by tot_orders limit 1;

![image](https://github.com/user-attachments/assets/d757abe6-5be5-4c78-8749-9e0e0114bce6)


3. What were the Most ordered items? 
   
         ANS : select item_name, 
         category, 
         count(order_details_id) as tot_orders
         from order_details o
        left join menu_items m on o.item_id = m.menu_item_id
        group by item_name, category
        order by tot_orders DESC limit 1;

![image](https://github.com/user-attachments/assets/d0de5a7e-915e-46f5-bb62-af8e9ff22e5d)


4. What were the top 5 orders that spent the most money?

          ANS :   select order_id, 
          sum(price) as tot_spend
           from order_details o 
          left join menu_items m on o.item_id = m.menu_item_id
          group by order_id
          order by tot_spend DESC 
          limit 5;

![image](https://github.com/user-attachments/assets/65f7537a-c028-4658-851c-0abcc267ce14)


5.  View the details of the highest spend order. 

         ANS : select category, 
         count(item_id) as num_itms
         from order_details o
        left join menu_items m on o.item_id = m.menu_item_id
        where order_id = 440
         group by category;


![image](https://github.com/user-attachments/assets/45f7f0b8-95f2-43a5-bf34-209b467283ae)

6.  View the details of the top 5 highest spend orders 

         ANS :  select order_id, category, 
         count(item_id) as num_itms
         from order_details o
         left join menu_items m on o.item_id = m.menu_item_id
         where order_id in (440, 2075, 330, 2675, 1957)
         group by order_id,category;


![image](https://github.com/user-attachments/assets/0366ee5c-3048-4076-8542-0925375cc351)










