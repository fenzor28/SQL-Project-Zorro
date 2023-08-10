# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
Execute the data cleaning and transforming techniques learned throughout the program.
Create and put into action a quality assurance (QA) procedure to compare and verify the transformed data with the original raw data.
Provide insights into business operations and trends through the analysis of data.

## Process
### Understanding the Data
     : I began by analyzing the data prior to cleaning. Before diving into cleaning, it's important that I understand the quality of the data, what it represents, 
       and what the research or business objectives are. By analyzing the data, I was able to identify the issues that need to be addressed during the cleaning process.
    
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




(fill in what you discovered this data could tell you and how you used the data to answer those questions)

## Challenges 

###When changes were made in the names of the columns, I kept getting this error:
    ERROR:  cached plan must not change result type 

Opening a new query tool solves the issue

## Future Goals
(what would you do if you had more time?)
