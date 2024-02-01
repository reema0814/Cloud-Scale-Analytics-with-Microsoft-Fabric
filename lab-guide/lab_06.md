# Lab 06: Create a Dataflow (Gen2) in Microsoft Fabric

## Lab Overview

In Microsoft Fabric, Dataflows (Gen2) connect to various data sources and perform transformations in Power Query Online. They can then be used in Data Pipelines to ingest data into a lakehouse or other analytical store, or to define a dataset for a Power BI report.

In this lab, we will delve into the realm of data transformation and ingestion using Microsoft Fabric! In this practical session, you will navigate the process of creating a Dataflow (Gen2), a powerful tool for orchestrating extract, transform, and load (ETL) processes seamlessly.

## Lab Objectives

Task 1 :  Create a Dataflow (Gen2) to ingest data<br>
Task 2 : Add data destination for Dataflow<br>
Task 3 :  Add a dataflow to a pipeline<br>

  
### Estimated timing: 30 minutes

## Architecture Diagram

![Navigate-To-AAD](./Images/ws/lab_04.png)

## Task 1:  Create a Dataflow (Gen2) to ingest data

 Now that you have a lakehouse, you need to ingest some data into it. One way to do this is to define a dataflow that encapsulates an *extract, transform, and load* (ETL) process.

1. In the home page of your workspace (1), click on **+New**(2) and then select **More options**(3).

   >**Note**: Ensure that the data warehouse is selected from the bottom left-hand corner.

   ![More-Options](./Images/more-options.png)

1. Search for Data Factory and then select **Dataflow Gen2**.

   ![Dataflow-Gen2](./Images/dataflow-gen2.png)

1. After a few seconds, the Power Query editor for your new dataflow opens as shown here. Select **Import from a Text/CSV file**, and create a new data source with the following settings:
   - **Link to file**: *Selected*
   - **File path or URL**: `https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/orders.csv`
   - **Connection**: Create new connection
   - **data gateway**: (none)
   - **Authentication kind**: Anonymous

   ![New dataflow.](./Images/new-dataflow1.png)

3. Select **Next** to preview the file data, and then **Create** the data source. The Power Query editor shows the data source and an initial set of query steps to format the data, as shown here:

    ![Query in the Power Query editor.](./Images/power-query1.png)

4. On the toolbar ribbon, select the **Add column** tab. Then select **Custom column** and create a new column named **MonthNo** that contains a number based on the formula `Date.Month([OrderDate])` - as shown here:

    ![Custom column in Power Query editor.](./Images/custom-column1.png)
   
    ![Query with a custom column step.](./Images/custom-column-added1.png)

     **The step to add the custom column is added to the query and the resulting column is displayed in the data pane**


   > **Tip:** In the Query Settings pane on the right side, notice the **Applied Steps** include each transformation step. At the bottom, you can also toggle the **Diagram flow** button to turn on the Visual Diagram of the steps.
   >
   > Steps can be moved up or down, edited by selecting the gear icon, and you can select each step to see the transformations apply in the preview pane.

## Task 2 : Add data destination for Dataflow

1. On the toolbar ribbon, select the **Home** tab. Then in the **Add data destination** drop-down menu, select **Lakehouse**.

   > **Note:** If this option is grayed out, you may already have a data destination set. Check the data destination at the bottom of the Query settings pane on the right side of the Power Query editor. If a destination is already set, you can change it using the gear.

2. In the **Connect to data destination** dialog box, verify that you're signed and then click on **Next**.

   ![Data destination configuration page.](./Images/lakehuse_31-1.png)

3. Select **Next** and in the list of available workspaces, find your workspace and select the lakehouse you created in it at the start of this exercise. Then specify a new table named **orders**:

    ![Data destination configuration page.](./Images/lakehouse.png)

   > **Note:** On the **Destination settings** page, notice how OrderDate and MonthNo are not selected in the Column mapping and there is an informational message: *Change to date/time*.

4.  On the **Destination settings** page, select **Append**, then go  to OrderDate and MonthNo columns . Click on the down Arrow and **Change Type** and then save the settings

    - OrderDate = Date/Time
    - MonthNo = Whole number

    ![Data destination settings page.](./Images/save_settings.png)

5. On the **Destination settings** page, select **Append**, and then save the settings.  The **Lakehouse** destination is indicated as an icon in the query in the Power Query editor.

 
    ![Query with a lakehouse destination.](./Images/publish.png)

6. Select **Publish** to publish the dataflow. Then wait for the **Dataflow 1** dataflow to be created in your workspace.

7. Once published, you can right-click on the dataflow in your workspace, select **Properties**, and rename your dataflow as **Transform Orders Dataflow**.


## Task 3:  Add a dataflow to a pipeline

You can include a dataflow as an activity in a pipeline. Pipelines are used to orchestrate data ingestion and processing activities, enabling you to combine dataflows with other kinds of operation in a single, scheduled process. Pipelines can be created in a few different experiences, including Data Factory experience.

1. From your Fabric-enabled workspace, make sure you're still in the **Data Engineering** experience. Select **New**, **Data pipeline**, then when prompted, create a new pipeline named **Load Orders pipeline**.

   The pipeline editor opens.

    ![Empty data pipeline.](./Images/new-pipeline1.png)

   > **Tip**: If the Copy Data wizard opens automatically, close it!

2. Select **Add pipeline activity**, and add a **Dataflow** activity to the pipeline.

3. With the new **Dataflow1** activity selected, on the **Settings** tab, in the **Dataflow** drop-down list, select **Transform Orders Dataflow** (the data flow you created previously)

    ![Pipeline with a dataflow activity.](./Images/dataflow-activity1.png)

4. On the **Home** tab, save the pipeline using the **&#128427;** (*Save*) icon.
5. Use the **&#9655; Run** button to run the pipeline, and wait for it to complete. It may take a few minutes.

    ![Pipeline with a dataflow that has completed successfully.](./Images/dataflow-pipeline-succeeded1.png)

6. In the menu bar on the left edge, select your lakehouse.
7. In the menu select **ellipse** icon for **Tables**, select **refresh**. Then expand **Tables** and select the **orders** table, which has been created by your dataflow.

    ![Table loaded by a dataflow.](./Images/loaded-table1.png)

   > **Tip**: Use the Power BI Desktop *Dataflows connector* to connect directly to the data transformations done with your dataflow<br>
  You can also make additional transformations, publish as a new dataset, and distribute with intended audience for specialized datasets.<br>
   ![Power BI data source connectors](Images/pbid-dataflow-connectors1.png)

## Review
In this execrise, the completion of these tasks involved the creation of a Dataflow (Gen2) to efficiently ingest data. A designated data destination was added to the Dataflow, ensuring organized storage for the ingested data. Additionally, a seamless integration was achieved by adding the Dataflow to a pipeline, allowing for coordinated data processing. The tasks collectively contributed to establishing an efficient and organized data ingestion and processing workflow.
 
## Proceed to next lab 
