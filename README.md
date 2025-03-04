# Home_Sales

In this project, we used PySpark to analyze home sales data stored in an Amazon Web Services (AWS) S3 bucket. The goal is to leverage big data processing techniques to extract insights, optimize query performance, and explore how caching and Parquet formatting affect execution speed. This project demonstrated the power of PySpark for handling and analyzing large datasets efficiently. By leveraging SparkSQL, caching, and Parquet optimizations, we improved query performance and explored big data best practices.

The purpose of this challenge is to:

* Load large-scale home sales data into PySpark.
* Perform SQL-based analysis using SparkSQL.
* Optimize performance through caching and Parquet partitioning.
* Compare query execution times for different optimizations.
* Work with distributed computing techniques in big data processing.

The following tools were used for this project:

* Python / Jupyter Notebook
* PySpark
* Google Colab
* Amazon Web Services S3
* Parquet 
* SparkSQL

This project was conducted in Google Colab, so it's recommended to install and configure PySpark in Google Colab to follow the steps.

The first step was to load the dataset from AWS. The home sales dataset was fetched from an AWS bucket and loaded into a PySpark DataFrame. The createOrReplaceTempView function was then used to create a temporary view of the DataFrame to enable SQL-based analysis in PySpark. An SQL query is used to calculate the average home prices for four-bedroom houses and homes with 3 bedrooms and 3 bathrooms. Some more similar calculations were done using SQL. Next we cached the home_sales table and reran the last query to compare execution times. Then the partitionBy funciton was used to partition the data by date_built and save in Parquet Format.

The spark.read.parquet(parquet_path) funciton was used to read the parquet data and the createOrReplaceTempView funciton was used to create a temporary table. Finally, the query was rerun on parquet data and the runtimes were compared again.

Runtimes:
* Uncached: 1.2010 seconds
* Cached: 0.6916 seconds
* Parquet: 0.6685 seconds

We can see by comparing the results that caching improved query performance significantly (42.4%) by keeping the data in memory. This confirms that caching helps when re-running the same query by keeping data in memory. However Parquet storage provided even better performance (44.3% faster than baseline). This means that Parquet's optimized columnar storage is reducing query execution time. Therefore, Parquet Storage is fastest, making it the best option for repeated queries.