# Amazon_Vine_Analysis
UT Data Bootcamp Module 16 -- BigData introduction using PySpark, AWS-S3, SQL
<!--
There is a title, and there are multiple sections (2 pt)
Each section has a heading and subheading (2 pt)
Links to images are working, and code is formatted and displayed correctly (2 pt).
-->

<!--
Overview of the analysis: Explain the purpose of this analysis.
The purpose of this analysis is well defined (3 pt)
-->
## Overview

This analysis introduces us to use of PySpark in conjunction with Google Colab, AWS S3, and SQL to perform analysis on large datasets ("Big Data").
Resources utilized include:
* https://aws.amazon.com/
* https://spark.apache.org/docs/latest/api/python/index.html
* https://www.pgadmin.org/
* https://colab.research.google.com/notebooks/intro.ipynb

ETL & data manipulation was performed on dataset from https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt.  
For purpose of my specific analysis, I selected:
* https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Video_Games_v1_00.tsv.gz
* Use of Spark for Deliverable 2 data manipulation.

<!--
Results: Using bulleted lists and images of DataFrames as support, address the following questions:
How many Vine reviews and non-Vine reviews were there?
How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?
What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?
There is a bulleted list that addresses the three questions for unpaid and paid program reviews (7 pt)
-->
## Results

[Applies for Game Reviews dataset:](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Video_Games_v1_00.tsv.gz)

![Vine_Results](https://github.com/jt-schmidt/Amazon_Vine_Analysis/blob/main/Vine_Results.PNG)

How many Vine & non-Vine reviews were there
  * Vine = 94
  * Non-Vine = 40,471

How many Vine & non-Vine reviews were 5 stars?
  * Vine = 48
  * Non-Vine = 15,663

What % of Vine & non-Vine reviews were 5 stars?
  * Vine = 51.06%
  * Non-Vine = 38.70%

Method of calculation:
``` Python
#1) Total number of reviews
vine_Y_Total = vine_Y_df.count()
vine_N_Total = vine_N_df.count()

#2) Number of 5-star reviews
vine_Y_5star_Total = vine_Y_df.filter(vine_Y_df.star_rating == '5').count()
vine_N_5star_Total = vine_N_df.filter(vine_N_df.star_rating == '5').count()

#3) Percent of 5-star reviews
vine_Y_5star_percent = ( vine_Y_5star_Total / vine_Y_Total ) * 100
vine_N_5star_percent = ( vine_N_5star_Total / vine_N_Total ) * 100
```

Data modifications to raw result include:
* Total Votes >= 20
 ``` Python
 vine_df.filter((vine_df.total_votes>=20))
 ```
* Helpful Votes / Total Votes >= 50%
 ``` Python
 vine_vote_over20_df.filter( ( vine_vote_over20_df.helpful_votes / vine_vote_over20_df.total_votes ) >= 0.5 )
 ```
* Isolation of Vine vs Non-Vine Reviews ( vine == 'N' or 'Y' )
 ``` Python
 vine_helpful_over50percent_df.filter(  vine_helpful_over50percent_df.vine == 'Y' )
 ```
 
<!--
Summary: In your summary, state if there is any positivity bias for reviews in the Vine program. Use the results of your analysis to support your statement. Then, provide one additional analysis that you could do with the dataset to support your statement.
The summary states whether or not there is bias, and the results support this statement (2 pt)
An additional analysis is recommended to support the statement (2 pt)
-->
## Summary

For reviews of Video Games on Amazon, being a paid Vine subscriber appears to indicate there is positivity bias versus non-subscribers due to the 51.06% versus 38.7% delta.  
However, non-subscribers out number subscribers 430 to 1 (40,471:94).  Due to small subscriber dataset relative to non-subscriber, this leads to conclusion that additional review is necessary for a more confident determination.

For a more thorough analysis, I would recommend additional analysis which does the following:
1.  Look at overall distribution of ratings for paid vs non-paid instead of limiting view to only 5-star.
2.  Select several Amazon review datasets & repeat this analysis for comparison instead of limiting to the one selected.
3.  Consider a join of REVIEW_ID with CUSTOMER_ID to find out if particular customers have a pattern of providing positive versus negative reviews as does or does not relate to subscription status.
4.  Consider a join of REVIEW_ID with PRODUCT_ID to find out if particular products have a pattern of receiving positive versus negative reviews as does or does not relate to subscription status.
