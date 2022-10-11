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


How many Vine reviews and non-Vine reviews were there?
How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?
What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?
Summary: In your summary, state if there is any positivity bias for reviews in the Vine program. Use the results of your analysis to support your statement. Then, provide one additional analysis that you could do with the dataset to support your statement.
