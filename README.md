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

*  How many Vine & non-Vine reviews were there
  * test
* How many Vine reviews were 5 stars?
  ** test  
* How many non-Vine reviews were 5 stars?
  *  
* What % of Vine reviews were 5 stars?
  * 
* What % of non-Vine reviews were 5 stars?
  * 

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

<!--
Summary: In your summary, state if there is any positivity bias for reviews in the Vine program. Use the results of your analysis to support your statement. Then, provide one additional analysis that you could do with the dataset to support your statement.
The summary states whether or not there is bias, and the results support this statement (2 pt)
An additional analysis is recommended to support the statement (2 pt)
-->
