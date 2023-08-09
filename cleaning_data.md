What issues will you address by cleaning the data?

Duplicate Records:
Removing the same piece of data being entered more than once, which can lead to biased analyses.

Inconsistent formatting:
Ensuring that each column has the appropriate data type, converting them if needed.

Handle Missing Values: 
Identifying and handling missing values

Text Cleaning:
Removing unnecessary whitespace, special characters, or punctuation in text data.

By addressing these issues, we can ensure that the data is complete, correct, and relevant to the problem we're trying to solve, leading to more accurate and reliable insights.





Queries:
Below, provide the SQL queries you used to clean your data.

# ALL_SESSIONS TABLE

--This query will update only the rows where the value in channelgrouping is exactly (other), removing the parentheses from that specific value. 

```
UPDATE all_sessions
SET channelgrouping = SUBSTRING(channelgrouping, 2, LENGTH(channelgrouping) - 2)
WHERE channelgrouping = '(Other)';
```


--Since the data was gathered before 2018, Retaining the historical name Macedonia (FYROM) might be beneficial but it's not necessary for my analysis

```
UPDATE all_sessions 
SET country = 'Macedonia'
WHERE country = 'Macedonia (FYROM)'
```

--The name change from "Burma" to "Myanmar" is tied to historical, ethnic, and political factors. Myanmar is the official name recognized by the United Nations and many countries so I decided to use it instead of Burma

UPDATE all_sessions 
SET country = 'Myanmar'
WHERE country = 'Myanmar (Burma)'























