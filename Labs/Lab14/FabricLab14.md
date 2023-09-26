# Lab Guide

## Implement a data science scenario

### Overview

In this lab you will ingest and cleanse data, train and register machine learning models, perform batch scoring, and create a Power BI report to visualize your predictions. 
 
### Time Estimate

- 45 minutes

## Exercise 1: Ingest and cleanse the data

### Overview

In this exercise, you will ingest and cleanse data, train and register machine learning models, perform batch scoring, and create a Power BI report. 
 

### Time Estimate

- 45 minutes

### Task 1: Ingest the Data

1. Go to https://github.com/microsoft/fabric-samples/tree/main/docs-samples/data-science/data-science-tutorial and download the raw files for the 5 notebooks in that folder. 

2. In a web browser, navigate to the Fabric home page at https://app.fabric.microsoft.com/home. 

3. Choose the Synapse Data Science experience. 

    ![](Exercise1images/media/Lab14_Image1.png)

4. In the menu on the left, select Workspaces and then choose the FabricWS1 workspace. 

6. Select the Home icon on the left. 

5. Select Import notebook and upload the notebook files that you downloaded in step 1. 

    ![](Exercise1images/media/Lab14_Image2.png)

6. Go to the FabricWS1 workspace and open the 01-ingest-data-into-fabric-lakehouse-using-apache-spark notebook. 

    ![](Exercise1images/media/Lab14_Image3.png)

7. Select Add Lakehouse. Choose Existing Lakehouse and select Lakehouse1. 

8. Run the first cell in the notebook. When the run is complete, expand the Spark jobs detail and review the information. 

    ![](Exercise1images/media/Lab14_Image4.png)

9. Execute cells 2 and 3. 

10. In the Lakehouse Explorer, refresh the Tables folder. 

  ![](Exercise1images/media/Lab14_Image5.png)

11. Confirm that the nyctaxi_raw table is present. 

  ![](Exercise1images/media/Lab14_Image6.png)


### Task 2: Explore the Data

1.  Navigate to the FabricWS1 workspace and open the 02-explore-and-visualize-data-using-notebooks notebook.

  ![](Exercise1images/media/Lab14_Image7.png)


2. Select Add Lakehouse. Choose Existing Lakehouse and select Lakehouse1.

3. Run cells 1 - 3. 

4. Review the visuals created as output of cell 3. 

  ![](Exercise1images/media/Lab14_Image8.png)

5. Run cell 4 and review the visual created in the output. 

  ![](Exercise1images/media/Lab14_Image9.png)

6. Run cell 5 and review the visual created in the output. 

  ![](Exercise1images/media/Lab14_Image10.png)

7. Run cell 6 and review the visual created in the output.

  ![](Exercise1images/media/Lab14_Image11.png)

8. Run cell 7 and compare the two visuals created in the output.

  ![](Exercise1images/media/Lab14_Image12.png)

9. Run cell 8 and review the two visuals created in the output. 

  ![](Exercise1images/media/Lab14_Image13.png)

10. Run cell 9 and review the visual created in the output.

  ![](Exercise1images/media/Lab14_Image14.png)

11. Run cell 10 and review the resulting heatmap visual. 

  ![](Exercise1images/media/Lab14_Image15.png)

12. Run cell 11 and review the visual created in the output. 

  ![](Exercise1images/media/Lab14_Image16.png)

13. Read the observations noted at the end of the notebook. 

  ![](Exercise1images/media/Lab14_Image17.png)


### Task 3: Cleanse and Prepare the Data

1.  Navigate to the FabricWS1 workspace and open the 03-perform-data-cleansing-and-preparation-using-apache-spark notebook. 

  ![](Exercise1images/media/Lab14_Image18.png)

2. Select Add Lakehouse. Choose Existing Lakehouse and select Lakehouse1.

3. Select Run All on the Home tab. Executing this notebook may take a few minutes. 

  ![](Exercise1images/media/Lab14_Image19.png)

4. Review the summary statistics shown in the output of cell 2. 

  ![](Exercise1images/media/Lab14_Image20.png)

5. Review the text and code in cell 3. 

  ![](Exercise1images/media/Lab14_Image21.png)

6. In the Lakehouse Explorer, confirm that you see a table named nyctaxi_prep. 

  ![](Exercise1images/media/Lab14_Image22.png)

### Task 4: Train and Register Machine Learning Models

1. Navigate to the FabricWS1 workspace and open the 04-train-and-track-machine-learning-models notebook. 

2. Select Add Lakehouse. Choose Existing Lakehouse and select Lakehouse1.

3. Run cell 1 and review the output. Confirm that the output indicates a new experiment has been created. 

  ![](Exercise1images/media/Lab14_Image23.png)

4. Run cells 2 and 3. Review the counts in the output of cell 3. 

  ![](Exercise1images/media/Lab14_Image24.png)

5. Review the text and code in cell 4. Then run the cell. 

  ![](Exercise1images/media/Lab14_Image25.png)

6. Review the text and code in cell 5. Then run the cell. 

7. Review the code in cell 6. Then run the cell. 

8. Review the code in cell 7. Then run the cell and review the output. 

  ![](Exercise1images/media/Lab14_Image26.png)

9. Review the code in cell 9. Then run the cell and review the output. 

10. Review the code in cell 10. Then run the cell and review the output. 

11. Review the code in cell 11. Then run the cell and review the output. 

  ![](Exercise1images/media/Lab14_Image27.png)

12. Review the code in cell 12. Then run the cell and review the output. 

13. Run cell 13 and copy the output.

  ![](Exercise1images/media/Lab14_Image28.png)

14. Navigate to the FabricWS1 workspace and select the model item named nyctaxi_tripduration_lightgbm to open the model UI.

  ![](Exercise1images/media/Lab14_Image29.png)

15. Review the model properties, metrics, and parameters. 

  ![](Exercise1images/media/Lab14_Image30.png)

### Task 5: Perform batch scoring and save predictions to a lakehouse

1. Navigate to the FabricWS1 workspace and open the 05-perform-batch-scoring-and-save-predictions-to-lakehouse notebook. 

  ![](Exercise1images/media/Lab14_Image31.png)


2. Select Add Lakehouse. Choose Existing Lakehouse and select Lakehouse1.

3. In cell 3, replace "<Enter the run_uri from module 04 here>" in line 8 with the value you copied from the output in the previous notebook. 

  ![](Exercise1images/media/Lab14_Image32.png)

3. Select Run All on the Home tab. Executing this notebook may take a few minutes. 

4. Review the inal predicted data in the output of cell 9. 

  ![](Exercise1images/media/Lab14_Image33.png)

5. In the Lakehouse Explorer, refresh the Tables folder.

6. In the Lakehouse Explorer, confirm that you see a table named nyctaxi_pred. 

  ![](Exercise1images/media/Lab14_Image34.png)

### Task 6: Create a Power BI report to visualize predictions

1. In the left menu, select OneLake data hub. 

  ![](Exercise1images/media/Lab14_Image35.png)

2. Select Lakehouse1. 

  ![](Exercise1images/media/Lab14_Image36.png)

3. Under Open this lakehouse, select Open. 

 ![](Exercise1images/media/Lab14_Image37.png)

4. Select New Power BI dataset in the top ribbon. 

 ![](Exercise1images/media/Lab14_Image38.png)

5. In the New dataset dialog, choose nyctaxi_pred.

 ![](Exercise1images/media/Lab14_Image39.png)

6. Once the page for the new dataset loads, rename the dataset by selecting the dropdown at top left corner of the dataset page and entering the more user-friendly name nyctaxi_predictions. Click outside the drop-down to apply the name change.

 ![](Exercise1images/media/Lab14_Image40.png)

7. On the Home tab at the top of the dataset page, select New report to open the Power BI report authoring page.

8. Select the slicer option from the visualizations pane and select pickupDate from the data pane and drop it on the created slicer visualization field of the date slider visual.

9. Add a clustered column chart, add timeBins to the X-axis, tripDuration and predictedTripDuration to the Y-axis and change the aggregation method to Average.

 ![](Exercise1images/media/Lab14_Image41.png)

10. Add an area chart visual and add weekDayName onto X-axis, tripDuration to Y-axis and predictedTripDuration to secondary Y-axis. Switch aggregation method to Average for both Y-axes.

 ![](Exercise1images/media/Lab14_Image42.png)

11. Add a Card Visual and add predictedTripDuration to the fields and switch aggregation method to Average.

12. Add a Card Visual and add TripDuration to the fields and switch aggregation method to Average.

 ![](Exercise1images/media/Lab14_Image43.png)

13. Select File and Save. Name the report Trip Duration Predictions. Save the report in FabricWS1.

### Summary

In this exercise, you used notebooks to ingest and cleanse data, train and register machine learning models, perform perform batch scoring, and save the predictions to a lakehouse. Then you created a Power BI report to visualize your predictions. 