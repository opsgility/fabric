## Exercise 7: Create a dataflow and schedule execution

### Overview

In this exercise, you will create a dataflow then schedule it.

### Time Estimate

- 15 minutes

### Task 1: Create a dataflow

1. Return to the Microsoft Fabric home page and click **Data Factory**.

    ```
    https://app.fabric.microsoft.com/home
    ```

    ![](Exercise7Images/media/Lab8_Image1.png)

2. Click **Workspaces** on the left then select the the **FabricWS1** workspace. 

    ![](Exercise7Images/media/Lab8_Image2.png)

3. Click **+ New** then select **Dataflow Gen2 (Preview)**.
 
    ![](Exercise7Images/media/Lab8_Image3.png)

4. Click **Import from a Text/CSV** file

    ![](Exercise7Images/media/Lab8_Image4.png)

5. Enter the following information then click **Next** then **Create** to create a new data source. 

    - Link to file: **Selected**

    - File path or URL: **https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/orders.csv**

    - Connection: **Create new connection**

    - Data gateway: **(none)**

    - Authentication kind: **Anonymous**

    ![](Exercise7Images/media/DataSource.png)

6. Click the **Add column** tab then select **Custom column**. Enter the following information then click **OK** to create a new column.

    - New column name: **MonthNo**

    - Data type: **Whole number**

    - Custom column formula: **Date.Month([OrderDate])**

    ![](Exercise7Images/media/Lab8_Image5.png)

7. Click **Home** then **Add data destination**, and select **Lakehouse**.

    ![](Exercise7Images/media/Lab8_Image6.png)

8. Click **Next**. Expand **FabricWS1** on the left then select **Lakehouse1**. Click **Next**. 

    ![](Exercise7Images/media/Lab8_Image8.png)

9. Select **Append** then click **Save settings**. Click **Publish**.  

    ![](Exercise7Images/media/Lab8_Image9.png)

### Task 2: Schedule the dataflow

1. Click **Schedule refresh** next to **Dataflow 1**.

    ![](Exercise7Images/media/Lab8_Image10.png)

2. Expand the **Refresh** section of the dataflow settings. Turn on the refresh schedule and configure the dataflow scheduled refresh by entering the below settings. Click **Apply**.

    - Refresh frequency: **Weekly**

    - Time zone: **Coordinated Universal Time**

    - Day of the week: **Saturday**

    - Time: **10:00 AM**   
    
    ![](Exercise7Images/media/Lab8_Image11.png)

### Summary

In this exercise, you created a dataflow that reads data from a URL, adds a custom column to calculate the month number, and lands the data in the lakehouse. Then you created a refresh schedule for the dataflow. 