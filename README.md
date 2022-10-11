# Amazon_Vine_Analysis

## Overview of the analysis: 
The purpose of this analysis was to analyze Amazon reviews using a PySpark connection and an AWD RDS instance. The data was then loaded into PGAdmin tables and pandas was used to evaluate bias towards reviews from paid Vine members specifically. 

## Results:
* A dataframe was created for the Health & Personal Care category using PySpark: 
```
from pyspark import SparkFiles
url = "https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Health_Personal_Care_v1_00.tsv.gz"
spark.sparkContext.addFile(url)
df = spark.read.option("encoding", "UTF-8").csv(SparkFiles.get("amazon_reviews_us_Health_Personal_Care_v1_00.tsv.gz"), sep="\t", header=True, inferSchema=True)
df.show()
```
* Dataframes were then created to match the tables within PGAdmin. The example for the vine review table is shown below. Once all dataframes were created, they were loaded into PGAdmin with an Amazon RDS as the server.
```
# Create the vine_table. DataFrame
vine_df = df.select(["review_id","star_rating","helpful_votes","total_votes","vine","verified_purchase"])

vine_df.show(10)
```
* The number of paid (Vine reviews) and unpaid reviews were calculated within the Vine_Review_Analysis.ipynb file. 

![image](https://user-images.githubusercontent.com/105991478/195216511-56dd112e-9cb9-49b5-8360-0ed81f806fd0.png)

* There were also 191 paid 5-start ratings, and 59921 unpaid 5-star ratings:
![image](https://user-images.githubusercontent.com/105991478/195216812-bbc9c07d-71a6-4e77-a4d0-4ddc81a33e1f.png)

The percentage of paid and unpaid reviews that are 5-starts are shown below. 
![image](https://user-images.githubusercontent.com/105991478/195216861-94956fd7-1ebb-48f0-8939-245875940add.png)

Summary: 

According to the analysis for this dataset, there does not appear to be a positivity bias for paid reviews because the percentage of 5-star reviews is higher for unpaid reviews. The sample set for the unpaid reviews is also substantially larger than the paid reviews. It may make sense to complete this analysis on other related shopping categories with higher paid review counts to ensure this holds true. 
