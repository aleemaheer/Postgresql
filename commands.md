#### POSTGRESQL COMMANDS:
##### Getting into the shell:
1. To enter into the psql shell type the command: 
``` bash
    psql -U <username> -W
```
2. If you want some commands or need help type the command:
``` bash
    help
```
if you are not in the psql shell you can type 
``` bash
    pslq --help
```
3. If you want to get list of databases type the command:
``` bash
    \l
```

##### Creating a database:
1. If you want to create a new database type the command:
``` bash
    CREATE DATABASE <name of database>;
```
##### Connecting to a database:
1. If you want to directly connect to a existing database, if you are not in the psql shell you can type the command:
``` bash
    psql -h <hostname> -p <port> -U <username> <name_of_database>
```
2. If you want to connect to a database and you are in the psql shell you can type the command:
``` bash
    \c
```
##### A very dangerous command:
1. If you want to delete a database you can write the command:
``` bash
    DROP DATABASE <name_of_database>;
```
##### Creating tables:
1. If you want to create a table in a database you can write the command:
``` bash
    CREATE TABEL <name_of_table> (
        Column name + datatype + constraints if any
    )
```
For example, 
``` bash
    CREATE TABLE person (
        id int,
        firstname VARCHAR(50),
        lastname VARCHAR(50),
        gender VARCHAR(6),
        date_of_birth TIMESTAMP,
    )
```
and a better table, 
``` bash
    CREATE TABLE person (
        id BIGSERIAL NOT NULL PRIMARY KEY,
        firstname VARCHAR(50) NOT NULL,
        lastname VARCHAR(50) NOT NULL,
        gender VARCHAR(6) NOT NULL,
        date_of_birth DATE NOT NULL,
        email VARCHAR(150),
    )
```

##### Inserting data into the tables:
1. If you want to insert the data in a table you can use like,
``` bash
    INSERT INTO <table_name> (
        firstname,
        lastname,
        gender,
        date_of_birth
    )
    VALUES ('Aleem', 'Aheer', 'Male', DATE '2004-01-06');
```
2. You can also get mock data from mockaro just to test the database.
3. If you want to run the SQL file that you have downloaded from the mockaro you can write the command:
``` bash
    \i<path_of_file>
```

##### Some commands:
1. SELECT * FROM person ORDER BY id ASC; => this will select all the data from the table person by ASC order.
2. SELECT * FROM person ORDER BY first_name DESC; => this will select all the data from the person table by descending order of first_name.
3. SELECT DISTINCT country_of_birth FROM person ORDER BY country_of_birth DESC; => this will select the country of birth, this will not repeat the country order by country of birth in descending order.
4. SELECT * FROM person LIMIT 10; => this will select the first 10 rows.
5. SELECT * FROM person OFFSET 5 LIMIT 5; => this will select the rows from id 6 to onwards 5, this is the postgres syntax.
6. SELECT * FROM person OFFSET 5 FETCH FIRST 5 ROW ONLY; => this will also select the five rows from 6 to onwards five, this is the SQL syntax.
7. SELECT * FROM person WHERE country_of_birth IN ('china', brazil', 'russia'); => this will select the rows or users that have country_of_birth china, brazil and russia.
8. SELECT * FROM person WHERE country_of_birth BETWEEN DATE '2000-01-01' AND '2015-01-01'; => this will select the rows or persons having date_of_birth from 2004 to 2015 only.
9. SELECT * FROM person WHERE email LIKE "%.com'; => this will select the rows or persons that includes .com domain.
10. SELECT * FROM person WHERE email LIKE '___a@%'; => this will select the person or row that have email that includes a@ after three characters.
11. SELECT * FROM person WHERE country_of_birth ILIKE 'p%'; => this will select the rows or persons whose country_of_birth are starting with letter p, it neglects the difference of uppercase and if we want to take care of case we can use LIKE instead of ILIKE.
12. SELECT country_of_birth, count(*) FROM person GROUP BY country_of_birth ORDER BY country_of_birth; => this will select the country_of_birth of persons and count how many persons are in a country, in ascending order.
13. SELECT country_of_birth, count(*) FROM person GROUP BY country_of_birth HAVING COUNT(*) < 5 ORDER BY country_of_birth;
14. SELECT MAX(price) FROM car; => this will select the maximum price from the table car. You can use other functions like min, avg and you can round off the value by writing the syntax SELECT ROUND(MAX(price)) FROM car; => this will select the max price and round off it.
15. SELECT make, model, MAX(price) FROM car GROUP BY make, model; => this will select the make, model and their max price from the column car.
16. SELECT SUM(price) FROM car; => this will select the total price of all cars from the car table.
17. SELECT make, model, SUM(price) FROM car GROUP BY make, model; => this will select the make, model and the sum of the same type of cars.
18. We can perform arithematic operations like SELECT 2 + 2;, SELECT 5 * 5;, SELECT 5 % 5; SELECT 5 / 10; etc.
19. SELECT id, make, model, price, ROUND(price * .10) FROM car; => this will select the all the mentions values with one more column that have 10% of actual price, means that with 10% off.
20. SELECT make, model, price, ROUND(price * .10, 2) AS ten_percent_off_price FROM car; => this will select the make, model, price and ten% off price of the original price and named this column as ten_percent_off_price.
21. SELECT price, price - (price * .10) FROM car; => this will select the price and ten% of price.
22. SELECT id, make, model, price, ROUND(price * .10) AS ten_percent_value, ROUND(price - (price * .10)) AS price_after_ten_percent_discount FROM car; => this will select the id, make, model, price, ten percent of value and value after 10 percent discount.
23. SELECT COALESCE(NULL, NULL, 1); => this will select the 1 and ignores the null values and SELECT COALESCE(NULL, NULL, 1, 100); => this will select the only 1 and ignores the others.
24. SELECT first_name, COALESCE(email, 'email not provided') FROM person; => this will select the first_name and emails of the person and the persons who don't have emails this will writes the email not provided.
25. SELECT NULLIF(10, 10); => this will get the answer of nullif because 10 is equal to 10. If the numbers are not equl to each other then this will get the first number e.g SELECT NULLIF(10, 100); => this will return the answer 10.
26. SELECT NOW(); => this will select the date and time, SELECT NOW()::TIME; => this will select the only time and SELECT NOW()::DATE; => this will select the only date.
27. SELECT NOW() - INTERVAL '1 YEAR'; => this will subtract the 1 year from the present datetime.
28. SELECT EXTRACT(YEAR FROM NOW()); => this will select the only present year from the now() which means date and time.
29. If we want to add a primary key to the table we can use the command ALTER TABLE person ADD PRIMARY KEY (id);
30. SELECT email, count(*) FROM person GROUP BY email HAVING COUNT(*) > 1; => this will select the emails that have the range of greater than 1.
31. ALTER TABLE person ADD CONSTRAINT unique_email_address UNIQUE (email); => this will add the constraint of the unique email address to the person.
32. ALTER TABLE person DROP CONSTRAINT unique_email_address; => this will drop the unique constraint of unique_email_address.
33. ALTER TABLE person ADD CONSTRAINT gender_constraint CHECK (gender = 'Male' OR gender = 'Female'); => by this command there will be a limit applied to the gender means that the user cannot enter invalid gender he can only enter male or female gender.
34. UPDATE person SET email = 'minguel@gmail.com' WHERE id = 3; => this will update the person email of id 3.
35. We can handle cases that have same id's by typing ON CONFLICT (id) DO NOTHING; in the end.
36. UPDATE person SET car_id = 2 WHERE id = 1; => this will set the person of id 1 to the car_id. You can see the file relation.sql where tables are joint.
37. \n this will expand the display.
38. If we want to join the two tables we can use the commmand SELECT * FROM person JOIN car ON person.car_id = car.id;
39. SELECT * FROM person  LEFT JOIN car ON person.car_id = car.id; => this will joins the two tables and select all the rows and columns from the left tabel and select the common data from the other table this is called left join.
40. We can check the extensions that are installed or not installed by typing select * from pg_available_extensions;
41. If we want to install the extension we can type CREATE EXTENSION IF NOT EXISTS "uuid-ossp"; => this will install the extension of uuid.
42. We can get a list of different functions by typing \df.