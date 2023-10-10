# Lab Guide

## Implement real-time analytics, query the results, and make a report

### Overview

In this lab you will create a KQL database, write a KQL query, and create a report that uses a KQL dataset. 
 
### Time Estimate

- 30 minutes


## Exercise 1: Create a KQL Database, KQL Query, and a Report

### Overview

In this exercise you will create a KQL database, write a KQL query, and create a report that uses a KQL dataset. 

### Time Estimate

- 30 minutes

### Task 1: Create a KQL Database

1. In a web browser, navigate to the Fabric home page at https://app.fabric.microsoft.com/home. 

2. Select the Synapse Real-Time Analytics experience. 

    ![](Exercise1images/media/Lab13_Image1.png)

3. In the menu on the left, select Workspaces and then choose the FabricWS1 workspace. 

4. Download the data file for this exercise from https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/sales.csv, saving it as sales.csv on your local computer (or lab VM if applicable). 

5. Return to browser window with Microsoft Fabric Experience. 

6. Select New and then KQL Database. 

    ![](Exercise1images/media/Lab13_Image2.png)

7. Name the database RTDB and click Create. 

    ![](Exercise1images/media/Lab13_Image3.png)

8. Select Get Data and then From Local File. 

    ![](Exercise1images/media/Lab13_Image4.png)

9. On the Ingest Data dialog, name the table Sales. Then click Next: Source 

    ![](Exercise1images/media/Lab13_Image5.png)

10. Select the sales.csv file that you previously downloaded. Then click Next: Schema. 

    ![](Exercise1images/media/Lab13_Image6.png)

11. Use the following settings for the schema settings. Then click Next: Summary.  
- Compression type: Uncompressed
- Data format: CSV
- Ignore the first record: Selected
- Mapping name: sales_mapping

12. Once the file is uploaded, select the Close button. 

    ![](Exercise1images/media/Lab13_Image7.png)


### Task 2: Query the KQL Database

1. Highlight the Sales table in the Data Tree. Then select Query Table > Show any 100 records. 

    ![](Exercise1images/media/Lab13_Image8.png)


2. A new pane will open with the query and its result. Modify the query to be the following:  
```
Sales
| where Item == 'Road-250 Black, 48'
```
3. Run the query. Then review the results

4. Modify the query to be the following: 
```
Sales
| where Item == 'Road-250 Black, 48'
| where datetime_part('year', OrderDate) > 2020
```
5. Run the query and review the results. 

6. Modify the query to be the following: 
```
sales
| where OrderDate between (datetime(2020-01-01 00:00:00) .. datetime(2020-12-31 23:59:59))
| summarize TotalNetRevenue = sum(UnitPrice) by Item
| sort by Item asc
```
7. Run the query and review the results.

8. Select Save as KQL queryset, name the query as Revenue by Product, and click Create.

    ![](Exercise1images/media/Lab13_Image9.png)

### Task 2: Query the KQL Database

1. Select Build Power BI report and wait for the report editor to open.

    ![](Exercise1images/media/Lab13_Image10.png)

2. In the report editor, in the Data pane, expand Kusto Query Result and select the Item and Quantity fields.

    ![](Exercise1images/media/Lab13_Image11.png)


3. On the report design canvas, select the table visualization that has been added and then in the Visualizations pane, select Clustered bar chart.

    ![](Exercise1images/media/Lab13_Image12.png)

4. Resize the visual to take up the entire page. 

5. Select File and then Save. 
    
    ![](Exercise1images/media/Lab13_Image13.png)

6. Name the file Sales Item Quantities and save it in the FabricWS1. 

   ![](Exercise1images/media/Lab13_Image14.png)

7. Close the Power BI window, and in the bar on the left, select the FabricWS1 workspace on the left. 

8. Select the Sales Item Quantities report from the list to view your report. 

   ![](Exercise1images/media/Lab13_Image15.png)

9. Review the report in your browser window. 

   ![](Exercise1images/media/Lab13_Image16.png)


### Summary


In this exercise, you created a KQL database, wrote a KQL query, and created a report that uses a KQL dataset. 