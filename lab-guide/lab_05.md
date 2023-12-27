# Lab 05: Cloud-Scale-Analytics-with-Microsoft-Fabric

## Lab Overview

In this lab, you will immerse yourself in the world of cloud-scale analytics, leveraging Microsoft Fabric to orchestrate data pipelines and analyze information seamlessly.

## Lab Objectives

Task 1 : Create a pipeline.<br>
Task 2 : Create a notebook.<br>
Task 3 : Modify and Monitor the pipeline.<br>

  
### Estimated timing: 40 minutes

## Architecture Diagram

![03](./Images/ws/lab_5.1.png)

## Task 1 :  Create a pipeline

A simple way to ingest data is to use a **Copy Data** activity in a pipeline to extract the data from a source and copy it to a file in the lakehouse.

1. At the bottom left of the Power BI portal, select the **Power BI** icon and switch to the **Data Engineering** experience.

1. In the **Synapse Data Engineering** home page, create a new **Lakehouse**.

   - **Name:** Enter **fabric2_<inject key="DeploymentID" enableCopy="false"/>**

1. On the **Home** page for your lakehouse, select **New Data pipeline**.

     ![03](./Images/01/datapipeline.png)

1. Create a new data pipeline named **Ingest Sales Data Pipeline**. 
   
     ![03](./Images/01/Pg3-TCreatePipeline-S1.1.png)
   
1. If the **Copy Data** wizard doesn't open automatically, select **Copy Data** in the pipeline editor page.

     ![03](./Images/01/03.png)

1. In the **Copy Data** wizard, on the **Choose a data source** page, in the **data sources** section, select the **Generic protocol (1)** tab and then select **HTTP (2)**, click on **Next (3)**.

     ![Screenshot of the Choose data source page.](./Images/01/Pg3-TCreatePipeline-S3.png)

1. Select **Next** and then select **Create new connection** and enter the following settings for the connection to your data source:
    - **URL**: `https://raw.githubusercontent.com/MicrosoftLearning/dp-data/main/sales.csv`
    - **Connection**: Create new connection
    - **Connection name**: *Specify a unique name*
    - **Authentication kind**: Basic (*Leave the username and password blank*)
  
     ![04](./Images/01/04.png)
    
1. Select **Next**. Then ensure the following settings are selected:
    - **Relative URL**: *Leave blank*
    - **Request method**: GET
    - **Additional headers**: *Leave blank*
    - **Binary copy**: <u>Un</u>selected
    - **Request timeout**: *Leave blank*
    - **Max concurrent connections**: *Leave blank*
  
     ![05](./Images/01/05.png)
   
1. Select **Next**, and wait for the data to be sampled and then ensure that the following settings are selected:
    - **File format**: DelimitedText
    - **Column delimiter**: Comma (,)
    - **Row delimiter**: Line feed (\n)
    - **First row as header**: Selected
    - **Compression type**: Leave default
1. Select **Preview data** to see a sample of the data that will be ingested. Then close the data preview and select **Next**.

     ![06](./Images/01/06.png)

1. On the **Choose data destination** page, select your existing lakehouse. Then select **Next**.

     ![07](./Images/01/07.png)

     ![07](./Images/01/connectdest02.png)

1. Set the following data destination options, and then select **Next**:
    - **Root folder**: Files
    - **Folder path name**: new_data
    - **File name**: sales.csv
    - **Copy behavior**: Leave default
   
     ![08](./Images/01/08.png)

1. Set the following file format options and then select **Next**:
    - **File format**: DelimitedText
    - **Column delimiter**: Comma (,)
    - **Row delimiter**: Line feed (\n)
    - **Add header to file**: Selected
    - **Compression type**: Leave default
   
     ![09](./Images/01/09.png)

1. On the **Copy summary** page, review the details of your copy operation and then select **Review + Run**.

    A new pipeline containing a **Copy Data** activity is created, as shown here:

     ![Screenshot of a pipeline with a Copy Data activity.](./Images/copy-data-pipeline.png)

1. When the pipeline starts to run, you can monitor its status in the **Output** pane under the pipeline designer. Use the **&#8635;** (*Refresh*) icon to refresh the status, and wait until it has succeeded.

     ![Screenshot of a pipeline with a Copy Data activity.](./Images/01/Pg3-CpyOutput.png)

1. In the menu bar on the left, select your lakehouse.

1. On the **Home** page, in the **Lakehouse explorer** pane, expand **Files** and select the **new_data** folder to verify that the **sales.csv** file has been copied.

     ![10](./Images/01/10.png)

#### Task 2 : Create a notebook

1. On the **Home** page for your lakehouse, in the **Open notebook** menu, select **New notebook**.

      ![11](./Images/01/11.png)

    After a few seconds, a new notebook containing a single *cell* will open. Notebooks are made up of one or more cells that can contain *code* or *markdown* (formatted text).

2. Select the existing cell in the notebook, which contains some simple code, and then replace the default code with the following variable declaration.

    ```python
   table_name = "sales"
    ```

   ![11](./Images/01/Pg3-Notebook-S2.png) 

3. In the **...** menu for the cell (at its top-right) select **Toggle parameter cell**. This configures the cell so that the variables declared in it are treated as parameters when running the notebook from a pipeline.

     ![12](./Images/01/12.png)

4. Under the parameters cell, use the **+ Code** button to add a new code cell. Then add the following code to it:

   >**Note:** Wait untill the previous code completes execution
   
    ```python
   from pyspark.sql.functions import *

   # Read the new sales data
   df = spark.read.format("csv").option("header","true").option("inferSchema","true").load("Files/new_data/*.csv")

   ## Add month and year columns
   df = df.withColumn("Year", year(col("OrderDate"))).withColumn("Month", month(col("OrderDate")))

   # Derive FirstName and LastName columns
   df = df.withColumn("FirstName", split(col("CustomerName"), " ").getItem(0)).withColumn("LastName", split(col("CustomerName"), " ").getItem(1))

   # Filter and reorder columns
   df = df["SalesOrderNumber", "SalesOrderLineNumber", "OrderDate", "Year", "Month", "FirstName", "LastName", "EmailAddress", "Item", "Quantity", "UnitPrice", "TaxAmount"]

   # Load the data into a managed table
   #Managed tables are tables for which both the schema metadata and the data files are managed by Fabric. The data files for the table are created in the Tables folder.
   df.write.format("delta").mode("append").saveAsTable(table_name)
    ```

    This code loads the data from the sales.csv file that was ingested by the **Copy Data** activity, applies some transformation logic, and saves the transformed data as a **managed table** - appending the data if the table already exists.

5. Verify that your notebooks looks similar to this, and then use the **&#9655; Run all** button on the toolbar to run all of the cells it contains.

     ![Screenshot of a notebook with a parameters cell and code to transform data.](./Images/notebook.png)

    > **Note**: Since this is the first time you've run any Spark code in this session, the Spark pool must be started. This means that the first cell can take a minute or so to complete.

6. (Optional) You can also create **external tables** for which the schema metadata is defined in the metastore for the lakehouse, but the data files are stored in an external location.

    ```python
    df.write.format("delta").saveAsTable("external_sales", path="<abfs_path>/external_sales")

    #In the Lakehouse explorer pane, in the ... menu for the Files folder, select Copy ABFS path.

    #The ABFS path is the fully qualified path to the Files folder in the OneLake storage for your lakehouse - similar to this:

    #abfss://workspace@tenant-onelake.dfs.fabric.microsoft.com/lakehousename.Lakehouse/Files
    ```
    > **Note**: To run the above code, you need to replace the <abfs_path> with your abfs path


7. When the notebook run has completed, in the **Lakehouse explorer** pane on the left, in the **...** menu for **Tables** select **Refresh** and verify that a **sales** table has been created.

8. In the notebook menu bar, use the ⚙️ **Settings** icon to view the notebook settings. Then set the **Name** of the notebook to **Load Sales Notebook** and close the settings pane.

    ![.](./Images/01/Pg3-Notebook-S10.png)
 
9. In the hub menu bar on the left, select your lakehouse.

10. In the **Explorer** pane, refresh the view. Then expand **Tables**, and select the **sales** table to see a preview of the data it contains.

#### Task 3 :  Modify and Monitor the pipeline

1. To monitor your data pipeline runs, hover over your pipeline in your workspace. Doing so will bring up three dots to the right of your pipeline name.

    ![.](./Images/ws/modify_runs.png)
   
1. Select the three dots to find a list of options. Then select View run history. This action opens a fly-out on the right side of your screen with all your recent runs and run statuses.

1. Select Go to monitoring hub from the prior screenshot to view more details and filter results. Use the filter to find specific data pipeline runs based on several criteria.

    ![.](./Images/ws/monitorinf_tab.png)

1. Select one of your pipeline runs to view detailed information. You’ll be able to view what your pipeline looks like and view more properties like Run ID or errors if your pipeline run failed.

    ![.](./Images/ws/monitoring1.png)

1. You can select Update pipeline to make changes to your pipeline from this screen. This selection will take you back in the pipeline canvas.

1. You can also Rerun your data pipeline. You can choose to rerun the entire pipeline or only rerun the pipeline from the failed activity.

1. A Gantt chart is a view that lets you see the run history over a time range. If you switch to a Gantt view, all pipeline runs will be grouped by name, displayed as bars relative to 
  how long the run took.

    ![.](./Images/ws/listgrant.png)

## Review

In this exercise, the completion of these tasks involved the creation of a pipeline  for orchestrating data workflows. A notebook was created to execute specific tasks within the pipeline. Furthermore, the pipeline was modified and monitored  to ensure adaptability and to track its performance over time. The tasks collectively contributed to the development and management of an effective data processing infrastructure.

## Proceed to next exercise

