# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
Execute the data cleaning and transforming techniques learned throughout the program.
Create and put into action a quality assurance (QA) procedure to compare and verify the transformed data with the original raw data.
Provide insights into business operations and trends through the analysis of data.

## Process
### Understanding the Data
 : I began by analyzing the data prior to cleaning. Before diving into cleaning, it's important that I understand the quality of the data, what it represents, and what the research or business objectives are. By analyzing the data, I was able to identify the issues that need to be addressed during the cleaning process.
    
### Import the Data into PostgreSQL
     1) Create a database named "Ecommerce" and table: Created a table in PostgreSQL for each CSV file with matching structure and appropriate data types
     2) Import the CSV file into the table: Use pgAdmin4 to import the CSV file into the created table

## Data Cleaning and Transformation
     : The goal of this process is to give us data that is complete, correct and relevant to the problems we're trying to solve, which makes analysis easier.
     1) Handle Duplicates: Remove or handle any duplicate rows and columns
     2) Identify missing values: Decide on a strategy to handle missing values, such as deletion or filling with default values.
     3) Data transformation: Convert data types if needed and normalize values.

## Quality Assurance Process
     1) Data Quality Checks: Regularly verify the accuracy and consistency of the data. This may include validating that imported data matches the raw data, checking for missing values or inconsistencies, 
        and ensuring that any transformations have been applied correctly.
     2) Documentation: Maintain clear and detailed documentation of the data cleaning and analysis steps. This ensures that the process can be easily reviewed, understood, and replicated.


## Results
     : With these dataset, I was able to discover
     -all_sessions
     1) Information about various user sessions, possibly related to an ecommerce platform, including user behavior, transactions, and interactions with different products.
     2) Information about the user (such as country and city) and how they reached the platform (through direct channels, referrals, or search) is provided.

    -analytics
     1) Information about website visits, including details about visitors, engagement, units sold, pageviews, time on site, bounces, revenue, and unit price.

     -products
     1) Information about various products

     -

(fill in what you discovered this data could tell you and how you used the data to answer those questions)

## Challenges 


1) Data cleaning and transformation consumed a lot of my time.
2) Several columns had missing values. Deciding how to handle these missing values required careful consideration and understanding of the domain context.
3) It was challenging to find a suitable primary and foreign key for some of the tables.
4) Some columns, such as "currrencycode," contained constant values across all rows. These constant columns may not contribute meaningful information, and deciding whether to keep or remove them required analysis.
5) Some columns may require conversion to more appropriate data types or formats. It was challenging without clear documentation or understanding of the data.
6) Making informed decisions about interpreting columns and cleaning was challenging to make accurately.
7) A lot of columns has missing values and is not suitable for analysis.
8)  When changes were made in the names of the columns, I kept getting this error:
   ERROR:  cached plan must not change result type
   Solved it by simply opening a new query tool
9) I assumed the time columns were minutes but it could be hours





## Future Goals
(what would you do if you had more time?)
