# Lab Guide

## Query a Lakehouse

### Overview
In this exercise, you will use the previously created lakehouses to query the uploaded customer data. 

### Time Estimate

- 30 minutes

## Exercise 1: Query data uploaded to a lakehouse

### Overview

In this exercise, you will query data uploaded to Lakehouse2. Then you will query the same data in Lakehouse1 referenced by a shortcut created in a previous module. 

### Task 1: Upload data

1. Download the sales.csv file from https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/sales.csv, saving it as sales.csv on your local computer (or lab VM if applicable).

    ![](Exercise1images/media/Lab4_Image1.png)

2. In a web browser, navigate to the Fabric home page at https://app.fabric.microsoft.com/home. 

2. Select the Synapse Data Engineering experience. 

    ![](Exercise1images/media/Lab4_Image2.png)

3. In the menu on the left, select Workspaces and then choose the FabricWS2 workspace. 

  ![](Exercise1images/media/Lab4_Image3.png)

4. Select the Lakehouse2 lakehouse item. 

  ![](Exercise1images/media/Lab4_Image4.png)

5. In the Get data menu, choose Upload files.

  ![](Exercise1images/media/Lab4_Image5.png)

6. Select the folder in the dialog on the right and locate the sales.csv file on your machine. Then click Open in the Open File dialog and Upload in the browser window. 

  ![](Exercise1images/media/Lab4_Image6.png)

7. After the file has been uploaded, select the Files/data folder and verify that the sales.csv file has been uploaded

8. In the Explorer for Lakehouse2, select Files. 

  ![](Exercise1images/media/Lab4_Image7.png)

9. Locate the sales.csv file in the Explorer in the web browser. Use the elipsis menu next to the file name to choose Load to Tables and then New Table. 

  ![](Exercise1images/media/Lab4_Image8.png)

10. Name the table Sales and click Load. Wait for the Sales table to load successfully. 

  ![](Exercise1images/media/Lab4_Image9.png)

### Task 2: Query data in the lakehouse

1.  At the top-right of the Lakehouse page, switch from Lakehouse to SQL endpoint. Then wait a short time until the SQL query endpoint for your lakehouse opens in a visual interface from which you can query its tables. 

  ![](Exercise1images/media/Lab4_Image10.png)

2. Use the New SQL query button to open a new query editor, and enter the following SQL query:
```
SELECT Item, SUM(Quantity * UnitPrice) AS Revenue
FROM sales
GROUP BY Item
ORDER BY Revenue DESC;
```

  ![](Exercise1images/media/Lab4_Image11.png)

3. Use the ▷ Run button to run the query and view the results, which should show the total revenue for each product.

  ![](Exercise1images/media/Lab4_Image12.png)

### Task 3: Query data using a shortcut

1. In the menu on the left, select Workspaces and then choose the FabricWS1 workspace. 

  ![](Exercise1images/media/Lab4_Image13.png)

2. Select the Lakehouse1 lakehouse item. 

  ![](Exercise1images/media/Lab4_Image14.png)

3. Right-click on Tables in the Lakehouse explorer. Choose New chortcut. 
  ![](Exercise1images/media/Lab4_Image15.png)

4. Under Internal Sources, choose Microsot OneLake. 

 ![](Exercise1images/media/Lab4_Image16.png)

5. Select Lakehouse2 as your data source. 

 ![](Exercise1images/media/Lab4_Image17.png) 

6. Select the Sales table and then click Create.  

  ![](Exercise1images/media/Lab4_Image18.png) 

7. At the top-right of the Lakehouse page, switch from Lakehouse to SQL endpoint. Then wait a short time until the SQL query endpoint for your lakehouse opens in a visual interface from which you can query its tables. 

8. Use the New SQL query button to open a new query editor, and enter the same SQL query as before:
```
SELECT Item, SUM(Quantity * UnitPrice) AS Revenue
FROM sales
GROUP BY Item
ORDER BY Revenue DESC;
```

9. Use the ▷ Run button to run the query and view the results, which should show the total revenue for each product.

  ![](Exercise1images/media/Lab4_Image19.png)

### Task 4: Create a visual query

1. On the toolbar, select New visual query.

  ![](Exercise1images/media/Lab4_Image20.png)

2. Drag the sales table to the new visual query editor pane.

  ![](Exercise1images/media/Lab4_Image21.png)

3. In the Manage columns menu, select Choose columns. Then select only the SalesOrderNumber and SalesOrderLineNumber columns. Select OK. 

  ![](Exercise1images/media/Lab4_Image22.png)

4. In the Transform menu, select Group by. Then group the data by using the following Basic settings:
- Group by: SalesOrderNumber
- New column name: LineItems
- Operation: Count distinct values
- Column: SalesOrderLineNumber

  ![](Exercise1images/media/Lab4_Image23.png)

5. Click OK and then review the results pane under the visual query to confirm it shows the number of line items for each sales order.

### Summary

In this exercise, you uploaded data to one lakehouse and created a shortcut to the it from another lakehouse. You write a SQL query to access the data. Then you wrote the same SQL query, this time using the shortcut. Finally, you created a visual query that also used the shortcut. 