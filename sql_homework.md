# SQL Homework

For this lab, we will use sqlite3, it is already available on your machine using the command `sqlite3`, copy the file sql_dump.sql in a folder where your sqlite3 database will be, then type:

```
sqlite3 wishlists.db < sql_dump.sql
```
This will create the database wishlists. Unlike Postgres, sqlite3 create a file in the folder where you are, if you delete this file, you delete the db !

To connect to the database, type `sqlite3 wishlists.db`, then you can execute sql statements.

Write SQL statements that:

    1. Selects the names of all products that are not on sale.
    SELECT * FROM products where on_sale = 'f';

    2. Selects the names of all products that cost less than £20.
    select name from products where price < 20;

    3. Selects the name and price of the most expensive product.
    SELECT name, max(price) FROM products;

    4. Selects the name and price of the second most expensive product.
    SELECT name, max(price) FROM products WHERE price NOT IN (SELECT max(price) FROM products);

    5. Selects the name and price of the least expensive product.
    SELECT name, min(price) FROM products;

    6. Selects the names and prices of all products, ordered by price in descending order.
    SELECT name, price FROM products ORDER BY price;    

    7. Selects the average price of all products.
    SELECT AVG(price) FROM products;

    8. Selects the sum of the price of all products.
    SELECT SUM(price) FROM products;

    9. Selects the sum of the price of all products whose prices is less than £20.
    SELECT SUM(price) FROM products WHERE price<20;

    10. Selects the id of the user with your name.
    SELECT id FROM users where name = 'ALex Chin';

    11. Selects the names of all users whose names start with the letter "J".
    SELECT name FROM users where name LIKE 'j%';

    12. Selects the number of users whose first names are "Spencer".
    select count(name) from users where name like 'spencer%';

    13. Selects the number of users who want a "Teddy Bear".
    select  count(*) from wishlists where product_id =1;

    select  count(*) from wishlists where product_id IN (select id from products where name = 'Teddy Bear');

    14. Selects the count of items on the wishlish of the user with your name.
    select count(*) from wishlists where user_id IN (select id from users where name = 'ALex Chin');

    HARD
    15. Selects the count and name of all products on the wishlist, ordered by count in descending order.

    select (select name from products where id = product_id),  count(product_id) 
    from wishlists 
    group by product_id 
    order by count(product_id) desc;

    HARD
    16. Selects the count and name of all products that are not on sale on the wishlist, ordered by count in descending order.

    almost there:
    select (select name from products where id = product_id AND on_sale = 'f'), product_id
    from wishlists 
    group by product_id 
    order by count(product_id) desc;
|17
Card Against Humanity|16
Cat Ears|15
|9
Teddy Bear|6
|5
|4
|2
Set of 12 Mason Jars|2

    <!-- select * from ( -->
    select (select name from products where id = product_id AND on_sale = 'f'), count(product_id) 
    from wishlists 
    



    17. Inserts a user with the name "Jonathan Anderson" into the users table. Ensure the created_at column is set to the current time.
    insert into users (created_at, name) values (current_timestamp, 'jonathan ander');

    18. Selects the id of the user with the name "Jonathan Anderson"?
    select id from users where name = 'jonathan ander';

    19. Inserts a wishlist entry for the user with the name "Jonathan Anderson" for the product "The Ruby Programming Language".
    nsert into wishlists (created_at, user_id, product_id) values (current_timestamp, 15, 4);

    insert into wishlists (created_at, user_id, product_id) values (current_timestamp, 
        (select id from users where name = 'jonathan ander'), 
        (select id from products where name = 'The Ruby Programming Language')
        );

    20. Updates the name of the "Jonathan Anderson" user to be "Jon Anderson".
    update users set name = 'jon renamed' where name = 'jonathan ander';

    21. Deletes the user with the name "Jon Anderson".
    delete from users where name = 'jon renamed'

    22. Deletes the wishlist item for the user you just deleted.
    delete  from wishlists where user_id not in (select id from users);

Please supply SQL statements, and the results they generate.



###Hints
  - As with anything, if you get stuck, move on, then go back if you have time.
  - Don't spend all night on it!