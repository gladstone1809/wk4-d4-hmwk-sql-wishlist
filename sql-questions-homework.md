# SQL Homework

For this homework, we will use sqlite3, it is already available on your machine using the command `sqlite3`, copy the file sql_dump.sql in a folder where your sqlite3 database will be, then type:

```
sqlite3 wishlists.db < sql_dump.sql
```

This will create the database wishlists. Unlike Postgres, sqlite3 create a file in the folder where you are, if you delete this file, you delete the db !

To connect to the database, type `sqlite3 wishlists.db`, then you can execute sql statements.

Write SQL statements that:

    1. Selects the names of all products that are not on sale.

        >>  select * from products where on_sale = 'f';
            
            1|2013-04-01 20:09:41.969902|Teddy Bear|17.99|f
            3|2013-04-01 20:09:41.973999|Cat Ears|99.99|f
            6|2013-04-01 20:09:41.978579|Card Against Humanity|25.0|f
            9|2013-04-01 20:09:41.983386|Set of 12 Mason Jars|6.22|f


    2. Selects the names of all products that cost less than £20.

        >>  select * from products where "price" < 20;

            1|2013-04-01 20:09:41.969902|Teddy Bear|17.99|f
            4|2013-04-01 20:09:41.975612|The Ruby Programming Language|19.99|t
            5|2013-04-01 20:09:41.977249|Silicon Valley Monopoly|10.99|t
            9|2013-04-01 20:09:41.983386|Set of 12 Mason Jars|6.22|f


    3. Selects the name and price of the most expensive product.

        >>  select name, max(price) from products;

            Cat Ears|99.99


    4. Selects the name and price of the second most expensive product.

        >>  select price, name from products order by price desc limit 1 offset 1;

            82.0|Brown Leather Boots


    5. Selects the name and price of the least expensive product.

        >>  select name, min(price) from products;

            Set of 12 Mason Jars|6.22


    6. Selects the names and prices of all products, ordered by price in descending order.

        >>  select price, name from products order by price desc, name desc;

            99.99|Cat Ears
            82.0|Brown Leather Boots
            78.82|Lonely Pillow
            25.0|Hoodie
            25.0|Card Against Humanity
            22.99|Set of silverware
            19.99|The Ruby Programming Language
            17.99|Teddy Bear
            10.99|Silicon Valley Monopoly
            6.22|Set of 12 Mason Jars


    7. Selects the average price of all products.

        >>  select avg(price) from products;
        
            38.899


    8. Selects the sum of the price of all products.

        >>  select sum(price) from products;

            388.99


    9. Selects the sum of the price of all products whose prices is less than £20.

        >>  select sum(price) from products where price < 20;

            55.19


    10. Selects the id of the user with your name.

        >>  select id from users where name = 'Filippo Matoso';

            10


    11. Selects the names of all users whose names start with the letter "J".

        >>  select name from users where name like 'j%';

            Jon Rogers
            James Gotsell

    12. Selects the number of users whose first names are "Spencer".

        >>  select count(id) from users where name like 'spencer%';

            1


    13. Selects the number of users who want a "Teddy Bear".


        >>  select COUNT(product_id) from wishlists where product_id = 1;

            6


    14. Selects the count of items on the wishlish of the user with your name.

        >>  select COUNT(product_id) from wishlists where user_id = 10;

            7 

    15. Selects the count and name of all products on the wishlist, ordered by count in descending order.
    
        >>  select count(product_id), name from products inner join wishlists on products.id = wishlists.product_id group by product_id order by count(product_id) desc;

            17|Hoodie
            16|Card Against Humanity
            15|Cat Ears
            9|The Ruby Programming Language
            6|Teddy Bear
            5|Silicon Valley Monopoly
            4|Brown Leather Boots
            2|Lonely Pillow
            2|Set of 12 Mason Jars


    16. Selects the count and name of all products that are not on sale on the wishlist, ordered by count in descending order.

        >>  select count(product_id), name from products inner join wishlists on products.id = wishlists.product_id and products.on_sale = 'f' group by product_id order by count(product_id)desc;
        
            16|Card Against Humanity
            15|Cat Ears
            6|Teddy Bear
            2|Set of 12 Mason Jars


    17. Inserts a user with the name "Jonathan Anderson" into the users table. Ensure the created_at column is set to the current time.

        >>  Insert into users (name, created_at) values ('Jonathan Anderson', CURRENT_TIME);


    18. Selects the id of the user with the name "Jonathan Anderson"?

        >>  select id from users where name = 'Jonathan Anderson';

            15


    19. Inserts a wishlist entry for the user with the name "Jonathan Anderson" for the product "The Ruby Programming Language".

        >>  insert into wishlists (user_id, product_id) values (15, 4);


    20. Updates the name of the "Jonathan Anderson" user to be "Jon Anderson".

        >>  update users set "name" = "Jon Anderson" where "name" = "Jonathan Anderson";

    21. Deletes the user with the name "Jon Anderson".

        >>  delete from users where name = "Jon Anderson";


    22. Deletes the wishlist item for the user you just deleted.

        >>  delete from wishlists where user_id = 15;


Please supply SQL statements, and the results they generate.



###Hints
  - As with anything, if you get stuck, move on, then go back if you have time.
  - Don't spend all night on it!
  - Use the resources on teh internetz to solve harder ones - there are solutions to these questions that work with what we've learnt today, but other tools exist in SQL that could make the queries 'better' or 'easier'.
