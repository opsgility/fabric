# Lab Guide

## Transform data with Spark and query with SQL

### Overview
In this lab you will transform and query data using a Spark notebook.
 
### Time Estimate

- 45 minutes

## Exercise 1: Transform data with Spark and query with SQL

### Overview

In this exercise, you will upload data to a lakehouse and then create a notebook to transform data. You will write data to a file and create a table using PySpark. Then you will use SparkSQL to query the table. 

### Time Estimate

- 45 minutes

### Task 1: Upload Data

1. In a web browser, navigate to the Fabric home page at https://app.fabric.microsoft.com/home. 

2. Select the Synapse Data Engineering experience. 

    ![](Exercise1images/media/Lab9_Image1.png)

3. In the menu on the left, select Workspaces and then choose the FabricWS2 workspace. 

    ![](Exercise1images/media/Lab9_Image2.png)

3. Download the zip file located at https://github.com/MicrosoftLearning/dp-data/raw/main/orders.zip.

4. On your local machine (or Lab VM), extract the CSV files from the zipped folder. After extracting the zipped archive, verify that you have a folder named orders that contains CSV files named 2019.csv, 2020.csv, and 2021.csv.

    ![](Exercise1images/media/Lab9_Image3.png)

5. Return to the web browser tab containing your FabricWS2. Select the Lakehouse2 Lakehouse item. 

    ![](Exercise1images/media/Lab9_Image4.png)

 6. In the ellipses menu for the Files folder in the Explorer pane, select Upload and Upload folder, and then upload the orders folder from your local computer (or lab VM) to the lakehouse.

    ![](Exercise1images/media/Lab9_Image5.png)

 7. After the files have been uploaded, expand Files and select the orders folder; and verify that the CSV files have been uploaded. 
 
    ![](Exercise1images/media/Lab9_Image6.png)


### Task 2: Explore data with a Spark notebook
1. While viewing the contents of the orders folder in your datalake, in the Open notebook menu, select New notebook.

    ![](Exercise1images/media/Lab9_Image7.png)

2. Select the first cell (which is currently a code cell), and then in the dynamic tool bar at its top-right, use the M↓ button to convert the cell to a markdown cell.

    ![](Exercise1images/media/Lab9_Image8.png)

3. Use the 🖉 (Edit) button to switch the cell to editing mode, then modify the markdown by replacing it with the following:  
```
# Sales order data exploration

Use the code in this notebook to explore sales order data.
```
4. Click anywhere in the notebook outside of the cell to stop editing it and see the rendered markdown.

    ![](Exercise1images/media/Lab9_Image9.png)

5. With the notebook visible, expand the Files list and select the orders folder so that the CSV files are listed next to the notebook editor. 

     ![](Exercise1images/media/Lab9_Image10.png)

6. In the ellipsis menu for 2019.csv, select Load data > Spark. 

     ![](Exercise1images/media/Lab9_Image11.png)

7. A new code cell containing the following code should be added to the notebook. Use the ▷ Run cell button on the left of the cell to run it.

     ![](Exercise1images/media/Lab9_Image12.png)

8. When the cell command has completed, review the output below the cell.

     ![](Exercise1images/media/Lab9_Image13.png)

9. Modify the code to set the header option to false as follows: 
```
df = spark.read.format("csv").option("header","false").load("Files/orders/2019.csv")
# df now is a Spark DataFrame containing CSV data from "Files/orders/2019.csv".
display(df)
```

10. Re-run the cell and review the output. 

     ![](Exercise1images/media/Lab9_Image14.png)

11. Modify the code as follows to define a schema and apply it when loading the data:
```
from pyspark.sql.types import *

orderSchema = StructType([
    StructField("SalesOrderNumber", StringType()),
    StructField("SalesOrderLineNumber", IntegerType()),
    StructField("OrderDate", DateType()),
    StructField("CustomerName", StringType()),
    StructField("Email", StringType()),
    StructField("Item", StringType()),
    StructField("Quantity", IntegerType()),
    StructField("UnitPrice", FloatType()),
    StructField("Tax", FloatType())
    ])

df = spark.read.format("csv").schema(orderSchema).load("Files/orders/2019.csv")
display(df)
```
12. Run the modified cell and review the output

     ![](Exercise1images/media/Lab9_Image15.png)

13. The dataframe includes only the data from the 2019.csv file. Modify the code so that the file path uses a * wildcard to read the sales order data from all of the files in the orders folder:
```python from pyspark.sql.types import *

orderSchema = StructType([ StructField("SalesOrderNumber", StringType()), StructField("SalesOrderLineNumber", IntegerType()), StructField("OrderDate", DateType()), StructField("CustomerName", StringType()), StructField("Email", StringType()), StructField("Item", StringType()), StructField("Quantity", IntegerType()), StructField("UnitPrice", FloatType()), StructField("Tax", FloatType()) ])

df = spark.read.format("csv").schema(orderSchema).load("Files/orders/*.csv") 

display(df) 
```

14. Run the modified code cell and review the output, which should now include sales for 2019, 2020, and 2021.

     ![](Exercise1images/media/Lab9_Image16.png)

15. Use the + Code icon below the cell output to add a new code cell to the notebook, and enter the following code in it:
```
customers = df['CustomerName', 'Email']
print(customers.count())
print(customers.distinct().count())
display(customers.distinct())
```

16. Run the new code cell, and review the results.

     ![](Exercise1images/media/Lab9_Image17.png)

17. Modify the code as follows: 
```
customers = df.select("CustomerName", "Email").where(df['Item']=='Road-250 Red, 52')
print(customers.count())
print(customers.distinct().count())
display(customers.distinct())
```

18. Run the modified code to view the customers who have purchased the Road-250 Red, 52 product.

     ![](Exercise1images/media/Lab9_Image18.png)

19. Add a new code cell to the notebook. 

20. Paste the following code in the cell: 
```
productSales = df.select("Item", "Quantity").groupBy("Item").sum()
display(productSales)
```

21. Run the code cell you added, and note that the results show the sum of order quantities grouped by product.

     ![](Exercise1images/media/Lab9_Image19.png)

22. Add another new code cell to the notebook, and enter the following code in it:
```
from pyspark.sql.functions import *

yearlySales = df.select(year(col("OrderDate")).alias("Year")).groupBy("Year").count().orderBy("Year")
display(yearlySales)
```

23. Run the code cell you added, and note that the results show the number of sales orders per year.

     ![](Exercise1images/media/Lab9_Image20.png)


### Task 2: Use Spark to transform data files

1. Add another new code cell to the notebook, and enter the following code in it:
```
from pyspark.sql.functions import *

## Create Year and Month columns
transformed_df = df.withColumn("Year", year(col("OrderDate"))).withColumn("Month", month(col("OrderDate")))

# Create the new FirstName and LastName fields
transformed_df = transformed_df.withColumn("FirstName", split(col("CustomerName"), " ").getItem(0)).withColumn("LastName", split(col("CustomerName"), " ").getItem(1))

# Filter and reorder columns
transformed_df = transformed_df["SalesOrderNumber", "SalesOrderLineNumber", "OrderDate", "Year", "Month", "FirstName", "LastName", "Email", "Item", "Quantity", "UnitPrice", "Tax"]

# Display the first five orders
display(transformed_df.limit(5))
```
2. Run the code to create a new dataframe from the original order data. Validate that Year and Month columns have been added, FirstName and LastName columns have been added, and the custom column has been revoved. 

     ![](Exercise1images/media/Lab9_Image21.png)

3. Add a new cell with the following code: 
```
transformed_df.write.mode("overwrite").parquet('Files/transformed_data/orders')
print ("Transformed data saved!")
```

4. Run the cell and wait for the message that the data has been saved.

     ![](Exercise1images/media/Lab9_Image22.png)

5. Add a new cell with the following code to load a new dataframe from the parquet files in the transformed_orders/orders folder:
```
orders_df = spark.read.format("parquet").load("Files/transformed_data/orders")
display(orders_df)
```
6. Run the cell and verify that the results show the order data that has been loaded from the parquet files.

     ![](Exercise1images/media/Lab9_Image23.png)

### Task 3: Save the data as a table and query with SQL

1. Add a new code cell to the notebook, and enter the following code, which saves the dataframe of sales order data as a table named salesorders:
```
# Create a new table
df.write.format("delta").saveAsTable("salesorders")

# Get the table description
spark.sql("DESCRIBE EXTENDED salesorders").show(truncate=False)
```

2. Run the cell and review the results. 

     ![](Exercise1images/media/Lab9_Image24.png)

3. In the Explorer pane, in the ellipsis menu for the Tables folder, select Refresh. Then expand the Tables node and verify that the salesorders table has been created.

     ![](Exercise1images/media/Lab9_Image25.png)

4. In the ellipsis menu for the salesorders table, select Load data > Spark.

5. A new code cell containing code similar to the following example is added to the notebook. Run the new code cell. 

     ![](Exercise1images/media/Lab9_Image26.png)

6. Add a new code cell to the notebook, and enter the following code in it:
```
%%sql
SELECT YEAR(OrderDate) AS OrderYear,
       SUM((UnitPrice * Quantity) + Tax) AS GrossRevenue
FROM salesorders
GROUP BY YEAR(OrderDate)
ORDER BY OrderYear;
```

7. Run the cell and review the results.

     ![](Exercise1images/media/Lab9_Image27.png)

### Summary

In this exercise, you upload data to a lakehouse and then created a notebook to transform data. You used PySpark to query and explore the data, and then write the data to a file. You then used PySpark to create a table. Finally, you used SparkSQL to query the table. 