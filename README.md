# SQL_Portfolio
A portfolio showcasing my SQL skills.


[Project One: Consumer Complaints](https://github.com/Lorenasepp/Lorenasepp/blob/c99bf7c8eb438a18f1f3d4c94579a3020746c64c/SQL%20Portfolio)

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
