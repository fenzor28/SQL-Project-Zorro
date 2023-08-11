# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
1) Execute the data cleaning and transforming techniques learned throughout the program.
2) Create and put into action a quality assurance (QA) procedure to compare and verify the transformed data with the original raw data.
3) Provide insights and trends through the analysis of data.

## Process

### Understanding the Data 
     : I began by analyzing the data prior to cleaning. Before diving into cleaning, it's important that I understand the quality of the data, what it represents, and what the research or business objectives are. By analyzing the data, I was able to identify the issues that need to be addressed during the cleaning process.

    
### Import the Data into PostgreSQL
     1) Create a database named "Ecommerce" and table: Create a table in PostgreSQL for each CSV file with matching structure and appropriate data types
     2) Import the CSV file into the table: Use pgAdmin4 to import the CSV file into the created table

### Data Cleaning and Transformation
     : The goal of this process is to give us data that is complete, correct and relevant to the problems we're trying to solve, which makes analysis easier.
     1) Handle Duplicates: Remove or handle any duplicate rows and columns
     2) Identify missing values: Decide on a strategy to handle missing values, such as deletion or filling with default values.
     3) Data transformation: Convert data types if needed and normalize values.

### Quality Assurance Process
     1) Data Quality Checks: Regularly verify the accuracy and consistency of the data. This may include validating that imported data matches the raw data, checking for missing values or inconsistencies, 
        and ensuring that any transformations have been applied correctly.
     2) Documentation: Maintain clear and detailed documentation of the data cleaning and analysis steps. This ensures that the process can be easily reviewed, understood, and replicated.

### Data Analysis
     1) I executed SQL queries to solve each problem and interpreted the results to provide insights.

## Results
 With these datasets, I was able to discover

### all_sessions
     1) Information about various user sessions, possibly related to an ecommerce platform, including user behavior, transactions, and interactions with different products.
     2) Information about the user (such as country and city) and how they reached the platform (through direct channels, referrals, or search) is provided.

### analytics
     1) Information about website visits, including details about visitors, engagement, units sold, pageviews, time on site, bounces, revenue, and unit price.

### products
     1) Information about various products

### sales_report
     1) Information about various products and their sales

### sales_sku
     1) Information about the summarized number of products ordered
     2) The values on this table matches with the sales_report table except that there are eight products that aren't in the sales_report table. 
     3) Six out of the eight products have a 'total_ordered' value of 0, indicating that these products have not been sold yet or new additions. This is a potential reason they might not appear in the sales_report table.

## With this data I was able to
1) Find products that are at a risk of going out of stock soon
2) Find products indicating potential overstocking
3) Find which products were commonly bought together
4) Find if there is any pattern in the categories of products ordered from visitors in each city and country
5) Summarize the impact of revenue generated from each city/country
6) Find top-selling products from each city/country and finds pattern in the products sold
7) Find the average number of products ordered from visitors in each city and country

## Challenges 
1) Data cleaning and transformation consumed a lot of my time.
2) I was not able to find a suitable column to serve as the primary key in some of the tables so I deicide to add an Auto-Incremented ID.
3) Several columns had missing values. Deciding how to handle these missing values required careful consideration and understanding of the domain context.
4) It was challenging to find a suitable primary and foreign key for some of the tables.
5) Some columns, such as "currrencycode," contained constant values across all rows. These constant columns may not contribute meaningful information, and deciding whether to keep or remove them required analysis.
6) Some columns may require conversion to more appropriate data types or formats. It was challenging without clear documentation or understanding of the data.
7) Making informed decisions about interpreting columns and cleaning was challenging to make accurately.
8) A lot of columns has missing values and is not suitable for analysis.
9)  When changes were made in the names of the columns, I kept getting this error:
   ERROR:  cached plan must not change result type
   Solved it by simply opening a new query tool
10) I assumed the time columns were minutes but it could be hours
11) I encountered issues when importing the all_sessions csv file
12) Not enough practice on data cleaning and the quality assurance process


## Future Goals
If I had more time I would:
1) Do a more rigorous QA process
2) Use complex data transformation queries for proper text normalization
3) Spend more time understanding why there is a lot of missing data before deciding on a strategy for dealing with it
4) Understand the distribution of data to find out potential outliers
5) Practice data cleaning
6) Document each single error to save time
7) Visualize data using charts and graphs to understand distributions, relationships, and patterns.
