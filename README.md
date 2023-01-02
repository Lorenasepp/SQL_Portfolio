# SQL_Portfolio
A portfolio showcasing my SQL skills.


[Project One:GROUP BY, ORDER BY, and LIMITS](https://github.com/Lorenasepp/Lorenasepp/blob/c99bf7c8eb438a18f1f3d4c94579a3020746c64c/SQL%20Portfolio)

  For this project I wanted to find out the top three companies with the most complaints, the top three products with the most complaints, and how the companies compare.
    
    1. First I collected all the data. In this case I downloaded a free database off of kaggle.com and used SQLiteStudio to run the queries.
    
    2. My first SQL query. To begin, I like to look at all of the information in the dataset to get a feel for the data included.
       I started with selecting all of the data from the table named consumer_complaints.
       
        SELECT *
        FROM consumer_complaints;

    3. Next I needed to begin to sort the data. 
       In this step I wanted to find the top three companies with the company with the highest number of complaints on top.
       I selected the company column, counted the company number of appearances, and named the count column: most_frequent_company. 
       Then I grouped the table by company and ordered by the count of the company to be descending so the company with the highest frequency would be on top.
       I then set the limit to 3 so only the top three companies would show. 
    
        SELECT company, COUNT(company) AS most_frequent_company
        FROM consumer_complaints
        GROUP BY company
        ORDER BY COUNT(company) DESC 
        LIMIT 3;

          The query results showed: 
              1.Bank of America, 55998 complaints
              2. Wells Fargo & Company, 42024 complaints
              3. JPMorgan Chase & Co., 33881 complaints

    4. Now that I know the companies with the highest level of complaints, I needed to find out the top three products with the most complaints.
       I used the same query as before but changed the word company to product and named the count column most_frequent_product. 

        SELECT product, COUNT(product) AS most_frequent_product
        FROM consumer_complaints
        GROUP BY product
        ORDER BY COUNT(product) DESC
        LIMIT 3; 

          The query results showed:
              1. Mortgage, 186475 complaints
              2. Debt collection, 101052 complaints
              3. Credit reporting, 91854 complaints

    5. In this step, I wanted to find out what the top three product for each of the top three companies. 
       I decided to look at each company individually so I could gain a deeper understanding of the data. 
       To do this I added a WHERE clause into my previous query.
        
         SELECT product, COUNT(product) AS most_frequent_product
         FROM consumer_complaints
         WHERE company = 'Bank of America'
         GROUP BY product
         ORDER BY COUNT(product) DESC
         LIMIT 3;

         SELECT product, COUNT(product) AS most_frequent_product
         FROM consumer_complaints
         WHERE company = 'Wells Fargo & Company'
         GROUP BY product
         ORDER BY COUNT(product) DESC
         LIMIT 3; 

         SELECT product, COUNT(product) AS most_frequent_product
         FROM consumer_complaints
         WHERE company = 'JPMorgan Chase & Co.'
         GROUP BY product
         ORDER BY COUNT(product) DESC
         LIMIT 3;

           Results: the top three products with the most complaints for Bank of America and Wells Fargo were mortgage, bank account or service, credit card. For JPMorgan Chase the results were in a different order; mortgage, credit card, and bank account or service.

    6. My final step was to go back to my questions from the beginning to make sure I answered them:

        A. The three companies with the most complaints are Bank of America, Wells Fargo, and JPMorgan Chase.
        B. The three products with the most complaints are mortgage, debt collecting, and credit reporting.
        C. All three of the companies had most frequently had problems with the same three products: mortgages, credit cards, and bank account and service.



[Project Two: WHERE, AND/OR, and COUNT](https://github.com/Lorenasepp/project2/blob/main/Portfolio%20project2)

For my second project, I used the same database as project one, Consumer Complaints.
For this project, my goal was to see what the top ten companies with the most complaints are for the state of California for mortgages.

    1. To start off I selected all of the information from the database. 
 
        SELECT *
        FROM consumer_complaints;

    2. Next I needed to filter my results by what I wanted to find out.
       I only wanted to see the results for California and for mortgages. 

        SELECT *
        FROM consumer_complaints
        WHERE state = 'CA'
        AND product = 'Mortgage';

    3.  My results were narrowed down to show what I wanted to see, but needed to be sorted into order to show the results I wanted. 

         SELECT *, COUNT(company)
         FROM consumer_complaints
         WHERE state = 'CA'
         AND product = 'Mortgage'
         GROUP BY company
         ORDER BY COUNT(company) DESC
         LIMIT 10;

       With this query I was able to count how many times a company had a complaint, group the companies together, and see the company with the most complaints on top.
       If I wanted to see the companies with the least complaints I would erase the DESC. 

    4. I now know the companies with the most complaints about their mortgages in the state of California. 
       If I was making the descision to open a mortgage account with one of those companies, I could run another query like this next one:

        SELECT *
        FROM consumer_complaints
        WHERE state = 'CA'
        AND product = 'Mortgage'
        AND company = ' ';   *// insert company name
 
       This query would let me see all of the issues pertaining to the company. 
       For this example I used Bank of America. 
       My results showed that even though Bank of America had the most complaints, looking through all the information on the table I would be comfortable opening an account with them. 
         - Bank of America is one of the biggest banks in the country so it makes sense they would also have more complaints. They have many customers.
         - They more often had a timely response than not showing they have good customer service. 
         - For the customer disputed disputed column, the frequency of any customer disputes was low, showing they have good customer service. 
         
         
[Project Three: Creating and Joining Tables](https://github.com/Lorenasepp/SQL_Portfolio/blob/main/Project%20Three) 
My third project demostrates my skills creating tables from raw data and joining two tables together. 

Objective: Determine the combine two tables to find the movie category for movies that Brad Pitt has acted in. 

  1. First I created two tables. The first table showing the actor name and the the movie category they are most commenly associated with. The second table shows a numerical id for each actor and movie title.

          CREATE TABLE actors (id INTEGER PRIMARY KEY AUTOINCREMENT, fullname TEXT, category TEXT);
          INSERT INTO actors (fullname, category) VALUES ("Brad Pitt", "Action");
          INSERT INTO actors (fullname, category) VALUES ("Tom Cruise", "Action");
          INSERT INTO actors (fullname, category) VALUES ("Jennifer Aniston", "Drama");
          INSERT INTO actors (fullname, category) VALUES ("Tina Fey", "Comedy"); 

          CREATE TABLE movies (id INTEGER PRIMARY KEY AUTOINCREMENT, actor_id INTEGER, title TEXT);
          INSERT INTO movies (actor_id, title) VALUES (1, "Mr. and Mrs. Smith");
          INSERT INTO movies (actor_id, title) VALUES (1, "Fury");
          INSERT INTO movies (actor_id, title) VALUES (2, "Jack Reacher");
          INSERT INTO movies (actor_id, title) VALUES (2, "Top Gun");
          INSERT INTO movies (actor_id, title) VALUES (3, "We're the Millers");
          INSERT INTO movies (actor_id, title) VALUES (3, "Marley & me");
          INSERT INTO movies (actor_id, title) VALUES (4, "Sisters");
          INSERT INTO movies (actor_id, title) VALUES (4, "Mean Girls");
          INSERT INTO movies (actor_id, title) VALUES (1, "Babel");
          INSERT INTO movies (actor_id, title) VALUES (3, "Horrible Bosses");
          INSERT INTO movies (actor_id, title) VALUES (2, "The Last Samurai");

  2. Then I used the two tables to show what category the movie titles most likely fall into based off Brad Pitts most common movie category.

          SELECT movies.title, actors.category
          From movies
          Join actors
          ON actors.id = movies.actor_id
          WHERE actors.category = "Action"
          AND actors.fullname = "Brad Pitt"
          ORDER BY movies.title;

  3. QUERY RESULTS
          title	                 category
          Babel	                 Action
          Fury	                 Action
          Mr. and Mrs. Smith     Action

[Project Four: ROUND, MAX, MIN, AS and CASE](https://github.com/Lorenasepp/SQL_Portfolio/commit/4df8edb316c8cf81932088ac364962bd0d9ebe8b)
My fourth project demostrates my skills using ROUND, MAX, MIN, and CASE functions.

Objective: Categorize countries into three categories based off country size.
/*Data from kaggle.com*/

    1. First, using a data table from kaggle, I rounded the average populations to find the whole number.
            SELECT ROUND(AVG(population)) AS avg_population FROM countries;

    2.Then I found the country with the smallest population:
            SELECT name, MIN(population) AS lowest_population FROM countries;

    3. Thirdly I found the country with the largest population:
            SELECT name, MAX(population) AS max_population FROM countries;

    4. Lastly I set parameters for my three categories I wanted to group the countries by:
           SELECT COUNT(*),
           CASE
             WHEN percent_of_world_pop > 1 THEN "Large"
             WHEN percent_of_world_pop > 0.01 THEN "Average"
             ELSE "Small"
           END AS country_size 
           FROM countries
           GROUP BY country_size;
