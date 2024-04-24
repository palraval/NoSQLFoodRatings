# NoSQLFoodRatings



## Part 1: NoSQL Set-Up

A datafile titled "establishments.json" is imported as a new database called "uk_food" through the use of mongoimport. The collection within this database is found to be called "establishments". A single document wihin this collection is printed and the collection is assigned to a variable named "establishments". 

A new restaurant and all its respective data is inserted into the collection and then this collection is checked to make sure the new data has been properly inserted into it. The inserted data, which has a value of "Restaurant/Cafe/Canteen" for "BusinessType", is missing a definitive value for "BusinessTypeID". A query is made for only data that has the value "Restaurant/Cafe/Canteen" for "BusinessType" and only the "BusinessType" and "BusinessTypeID" values are printed to find that "BusinessTypeID" has a value of 1 when "BusinessType" is "Restaurant/Cafe/Canteen". Once knowing this, the new data is updated with a value of 1 for "BusinessTypeID". 

The number of documents that have a value of "Dover" for "LocalAuthorityName" is found and then deleted from the "establishments" collection. The number of documents with this same criteria is checked again to make sure the count is 0 now. 

The latitude and longitude values in the "establishments" collection is converted from a String datatype to a Decimal datatype, the values of "RatingValue" that are not 1 through 5 are converted to Null, and the values associated with "RatingValue" are converted to an Integer datatype. Lastly, a check is done on a single document to make sure the coordinates and rating values have become numbers.



## Part 2: Analysis 

An instance of MongoClient is created, the "uk_food" database is assigned to a variable named "db", and the "establishments" collection is assigned to a variable called "establishments". After this set-up is completed, four questions are answered using this collection's data:



**1. Which establishments have a Hygiene score of 20?** 

A query is made where "scores.Hygiene" is equal to 20. The number of documents that fit this criteria are found to be 41 and the first document is printed. All the results that fit this query are converted into a DataFrame called "result_df", which shows the amount of rows in this DataFrame and the first ten rows.




**2. Which establishments in London have a RatingValue greater than or equal to 4?** 

A query is constructed that contains the value "London" for "LocalAuthorityName" and values for "RatingValue" that are greater than or equal to 4. The number of documents that fit this criteria is found to be 33 and the first document is printed. All the results that fulfill this criteria are converted to a DataFrame titled "london_dataframe". The number of rows in this DataFrame is found and the first ten rows are shown.




**3. What are the top 5 establishments with a RatingValue of 5, sorted by lowest to highest Hygiene scoer, nearest to the newly added restaurant ("Penang Flavours")?**


The longitude and latitude values for the "Penang Flavours" is found by querying for the restaurant's name and extracting the coordinates' values. Another query is created which has longitude and latitude values of within a radius of 0.01 from the "Penang Flavours" coordinates and "RatingValue" of exactly 5. The sort is set according to the Hygiene scores in ascending order. Finally, a limit is set to 5 to get the top 5 results. The data from the "establishments" collection that fulfills all this criteria is found and printed. These 5 results are converted to a DataFrame named "coordinates_results" and shown.




**4. How many establishements in each Local Authority area have a Hygiene score of 0?**


For this question, a pipeline is constructed with 3 elements. The first element is called "match_query" and it only gives data that has a Hygiene score of 0. The second element is called "group_query". This seperates each unique value within "LocalAuthorityName" and provides the total count of each value. The third element is named "sort_values", which sorts the count in descending order. The "establishments" collection is aggregated according to this pipeline. The number of documents in this results is found to be 55 and the first ten results are printed. All 55 results are converted into a DataFrame titled "pipeline_df'. The number of rows in this DataFrame is calculated and the first ten rows are displayed. 

