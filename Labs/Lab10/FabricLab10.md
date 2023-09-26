# Lab Guide

## Design a dimensional model from AdventureWorks OLTP data

### Overview

In this lab you will work to take the data from a transactional database and denormalize it into a star schema.  

### More Information

Source files have been provided for you with this Lab. You will need to download them to your local machine if you are not working in a lab VM. 
 
This lab requires the use of OneLake File Explorer, which was installed in a previous lab. 

### Time Estimate

- 35 minutes


## Exercise 1: Ingest the data

### Overview

In this exercise, you will upload data from the AdentureWorks OLTP database to a lakehouse, then you will design a fact table and a dimension table using dataflows. Your goal is to create a product dimension and a sales fact. 

### Task 1: Get the source data

1. Locate the 5 files provided for this lab: 
- Product.csv
- ProductCategory.csv
- ProductModel.csv
- SalesOrderDetail.csv
- SalesOrderHeader.csv


2. Locate the OneLake app in your start menu. Select it to open the app. If the app is already running, locate the OneLake icon in the system tray and double-click to open it. A Windows Explorer window should open.

3. You should see two folders named after the two workspaces you created in Lab 1. Navigate into the FabricWS2 folder. You should see a folder named Lakehouse2.Lakehouse. Navigate into that folder and then into the Files folder.
    
    ![](Exercise1images/media/Lab10_Image2.png) 

4. Copy the five files to the FabricWS2\Lakehouse2.Lakehouse\Files folder. The files will sync to Lakehouse2.
    
     ![](Exercise1images/media/Lab10_Image3.png) 

### Task 2: Create the product dimension

1. In a web browser, navigate to the Fabric home page at https://app.fabric.microsoft.com/home. 

2. Select the Synapse Data Engineering experience. 

3.  In the menu on the left, select Workspaces and then choose the FabricWS2 workspace. 

4. Select the Lakehouse2 lakehouse item from the workspace. Then select Get Data > New Dataflow Gen2.  

    ![](Exercise1images/media/Lab10_Image4.png) 

5. Select Get Data and choose the Lakehouse data source. 
 
    ![](Exercise1images/media/Lab10_Image5.png) 

6. Select the 3 product related files in the Files folder under FabricWS2 >  Lakehouse2. Then click Create. 
- Products.csv
- ProductCategory.csv
- ProductModel.csv

   ![](Exercise1images/media/Lab10_Image6.png) 

7. Select the Product query. Then select Use first row as headers. 
   
   ![](Exercise1images/media/Lab10_Image7.png) 

8. Select the ProductCategory query. Then select Use first row as headers. 

   ![](Exercise1images/media/Lab10_Image8.png) 

9. Select the ProductModel query. Then select Use first row as headers. 

10. Select the Product query. Then choose Merge queries. 

   ![](Exercise1images/media/Lab10_Image9.png) 

11. Merge the Product query with the ProductCategory query based upon the ProductCategoryID column in each table. Set the join kind to Inner. Then click OK. 

   ![](Exercise1images/media/Lab10_Image10.png) 

12. Expand the ProductCategory column. Select only the Name column and then click OK. 

   ![](Exercise1images/media/Lab10_Image11.png) 

 13. Select the Product query again. Then choose Merge queries. 

 14. Merge the Product query with the ProductModel query based upon the ProductModelID column in each table. Set the join kind to Inner. Then click OK.   

   ![](Exercise1images/media/Lab10_Image12.png) 

15. Expand the ProductModel column. Select only the Name column and then click OK. 

   ![](Exercise1images/media/Lab10_Image13.png) 

16. Select the Product query. On the Add column tab, choose Index column. 

   ![](Exercise1images/media/Lab10_Image14.png) 

17. Rename the following columns in the Product query: 
- Change Name.1 to ProductCategory. 
- Change Name.2 to ProductModel.
- Change Index to ProductKey.
- Change Name to ProductName.

   ![](Exercise1images/media/Lab10_Image15.png) 

18. In the lower right corner, add a data destination to a Lakehouse.

   ![](Exercise1images/media/Lab10_Image16.png) 

19. Click Next on the data destination page. Then choose Lakehouse2 as the destination. Name the table Product. Click Next and then click Save Settings. 

20. Click the Publish button. 

### Task 2: Create the sales fact

1. Select New and then Dataflow Gen2. 

   ![](Exercise1images/media/Lab10_Image17.png) 

2. Select Get Data and choose the Lakehouse data source. 

3. Select the the SalesOrderHeader.csv and SalesOrderDetail.csv files in the Files folder under FabricWS2 >  Lakehouse2. Then click Create. 

   ![](Exercise1images/media/Lab10_Image18.png) 

4. Select the SalesOrderHeader query and choose Use first row as header. 

5. Select the SalesOrderDetail query and choose Use first row as header. 

6. Select the SalesOrderDetail query and choose Merge queries. 

7. Merge the SalesOrderDetail query with the SalesOrderHeader query based upon the SalesOrderID column in each table. Set the join kind to Inner. Then click OK. 

   ![](Exercise1images/media/Lab10_Image19.png) 

8. Select the SalesOrderDetail query and expand the SalesOrderHeader column. Select the following columns and then click OK: 
- OrderDate
- ShipDate
- SalesOrderNumber
- PurchaseOrderNumber

   ![](Exercise1images/media/Lab10_Image20.png) 


9. Select Get Data and choose the Lakehouse data source. 

10. Select the Product table. 

11. Select the SalesOrderDetail query. Then choose Merge queries.

12. Merge the SalesOrderDetail query with the Product query based upon the ProductID column in each table. Set the join kind to Inner. Then click OK. 

   ![](Exercise1images/media/Lab10_Image21.png) 


13. Expand the Product column. Choose only the ProductKey column and click Ok. 

   ![](Exercise1images/media/Lab10_Image22.png) 


14. In the lower right corner, add a data destination to a Lakehouse.

15. Click Next on the data destination page. Then choose Lakehouse2 as the destination. Name the table Sales. Click Next and then click Save Settings. 

16. Click the Publish button near the lower right corner. 

### Summary

In this exercise, you uploaded files from a transactional system to a lakehouse. Then you used dataflows to create a product dimension and sales fact that are part of a star schema. 
