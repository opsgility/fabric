## Exercise 5: Copy data into a lakehouse with the Copy Data Tool

### Overview

In this exercise, you will copy data into a lakehouse using the copy tool.

### Time Estimate

- 15 minutes

### Task 1: Download and install OneLake File Explorer

1. Return to the Microsoft Fabric home page and click **Data Factory**.

    ```
    https://app.fabric.microsoft.com/home
    ```

    ![](Exercise5Images/media/Lab6_Image1.png)

2. Click **Workspaces** on the left then select the the **FabricWS1** workspace.

    ![](Exercise5Images/media/Lab6_Image2.png)

3. Click **+ New** then **Data pipeline (Preview)**. 

    ![](Exercise5Images/media/Lab6_Image3.png)

4. Enter **Ingest Sales Data** for the name then click **Create**. 
    
    ![](Exercise5Images/media/Lab6_Image4.png)

5. Click **Copy data**.
    
    ![](Exercise5Images/media/Lab6_Image5.png)

6. In the **Copy Data** wizard, on the **Choose data source** page, scroll down and click the **Generic protocol** tab then select **HTTP**. Click **Next**. 

    ![](Exercise5Images/media/Lab6_Image6.png)

7. Select **Create new connection** and enter the following settings for the connection to your data source then click **Next** and click **Next** again.

    - URL: **https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/sales.csv**

    - Connection: **Create new connection**

    - Connection name: **Specify a unique name**

    - Authentication kind: **Basic**

    ![](Exercise5Images/media/Lab6_Image7.png)

8. Wait for the data to be sampled and then ensure that the below settings are selected. Click **Next**. 

    - File format: **DelimitedText**

    - Column delimiter: **Comma (,)**

    - Row delimiter: **Line feed (\n)**

    - First row as header: **Selected**

    ![](Exercise5Images/media/Lab6_Image9.png)

9. On the **Choose data destination** page, select **Lakehouse** then click **Next**.

    ![](Exercise5Images/media/SelectLakehouse.png)

10. Select **Existing Lakehouse** then select **Lakehouse1** then click **Next**. 

    ![](Exercise5Images/media/Lab6_Image10.png)

11. Enter the below data destination information, then click **Next**.

    - Root folder: **Files**

    - Folder path: **new_data**

    - File name: **sales2.csv**

    ![](Exercise5Images/media/Lab6_Image11.png)

12. Enter the below file format options then click **Next**. Click **Save +Run**. 

    - File format: **DelimitedText**

    - Column delimiter: **Comma (,)**

    - Row delimiter: **Line feed (\n)**

    - Add header to file: **Selected**

    ![](Exercise5Images/media/Lab6_Image12.png)

13. A new pipeline containing a Copy Data activity is created. The pipeline is executed immediately. Review the information on the Output tab to confirm the pipeline run succeeded. 

    ![](Exercise5Images/media/Lab6_Image13.png)


### Task 2: Review the copied data

1. Click the **Lakehouse1** icon depicted in the below image. Expand **Files** on the left then select the **new_data** folder. Verify that you see the **sales2.csv** file.   

    ![](Exercise5Images/media/Lab6_Image14.png)

    ![](Exercise5Images/media/Lab6_Image15.png)


### Summary

In this exercise, you used the Copy Data tool to copy data from an HTTP source to a lakehouse and then verified the new data using the Lakehouse Explorer. 