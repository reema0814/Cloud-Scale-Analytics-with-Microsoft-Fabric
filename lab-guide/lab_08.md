## Lab 08: Get started with Real-Time Analytics in Microsoft Fabric

## Lab Overview

In this lab, you will explore the exciting realm of real-time analytics using Microsoft Fabric. This lab is designed to introduce you to the powerful Kusto Query Language (KQL) and guide you through the process of creating a KQL database, querying data, and creating compelling Power BI reports.

## Lab Objectives
 Task 1 : Create a KQL database.<br>
 Task 2 : Use KQL to query the sales table.<br>
 Task 3 : Create a Power BI report from a KQL Queryset.<br>
 
  
### Estimated timing: 30 minutes

## Architecture Diagram 

![Navigate-To-AAD](./Images/ws/lab_06.png)

## Task 1 : Create a KQL database

Kusto query language (KQL) is used to query static or streaming data in a table that is defined in a KQL database. To analyze the sales data, you must create a table in a KQL database and ingest the data from the file.

1. In the **Microsoft Fabric** https://app.fabric.microsoft.com/ experience portal, select the **Synapse Real-Time Analytics** experience image as shown here:
    
     ![00](./Images/03/synpase.png)

3. On the **Home** page for the **Real-Time Analytics** experience, select **KQL database** and create a new database.
   
     ![00](./Images/03/kql.png)

   >**Note:** Make the fabric workspace is selected before Creating KQL database
   
   - **Name:** Enter **KQL-Database-<inject key="DeploymentID" enableCopy="false"/>**

    ![00](./Images/03/createkql.png)
   
   
5. When the new database has been created, select the option to get data from **Local File**.

    ![01](./Images/03/01.png)

6. Use the wizard to import the data into a new table by selecting the following options:
    - **Destination**:
        - **Database**: *The database you created is already selected*
        - **Table**: *Create a new table named* **sales**.
    - **Source**:
        - **Source type**: File
        - **Upload files**: Drag or Browse for the file from **C:\LabFiles\Files\sales.csv**
    - **Schema**:
        - **Compression type**: Uncompressed
        - **Data format**: CSV
        - **Ignore the first record**: *Selected*
        - **Mapping name**: sales_mapping
    - **Summary**:
        - *Review the preview of the table and close the wizard.*

> **Note**: In this example, you imported a very small amount of static data from a file, which is fine for the purposes of this exercise. In reality, you can use Kusto to analyze much larger volumes of data; including real-time data from a streaming source such as Azure Event Hubs.

## Task 2 : Use KQL to query the sales table

Now that you have a table of data in your database, you can use KQL code to query it.

1. Make sure you have the **sales** table highlighted. From the menu bar, select the **Query table** drop-down, and from there select **Show any 100 records** .

2. A new pane will open with the query and its result. 

3. Modify the query as follows:

    ```kusto
   sales
   | where Item == 'Road-250 Black, 48'
    ```

4. Run the query. Then review the results, which should contain only the rows for sales orders for the *Road-250 Black, 48* product.

5. Modify the query as follows:

    ```kusto
   sales
   | where Item == 'Road-250 Black, 48'
   | where datetime_part('year', OrderDate) > 2020
    ```

6. Run the query and review the results, which should contain only sales orders for *Road-250 Black, 48* made after 2020.

7. Modify the query as follows:

    ```kusto
   sales
   | where OrderDate between (datetime(2020-01-01 00:00:00) .. datetime(2020-12-31 23:59:59))
   | summarize TotalNetRevenue = sum(UnitPrice) by Item
   | sort by Item asc
    ```

8. Run the query and review the results, which should contain the total net revenue for each product between January 1st and December 31st 2020 in ascending order of product name.

9. Select **Save as KQL queryset** and save the query as **Revenue by Product**.

## Task 3 : Create a Power BI report from a KQL Queryset

You can use your KQL Queryset as the basis for a Power BI report.

1. In the query workbench editor for your query set, run the query and wait for the results.

2. Select **Build Power BI report** and wait for the report editor to open.

3. In the report editor, in the **Data** pane, expand **Kusto Query Result** and select the **Item** and **TotalRevenue** fields.

4. On the report design canvas, select the table visualization that has been added and then in the **Visualizations** pane, select **Clustered bar chart**.

    ![Screenshot of a report from a KQL query.](./Images/kql-report.png)

5. In the **Power BI** window, in the **File** menu, select **Save**. Then save the report as **Revenue by Item.pbix** in the workspace where your lakehouse and KQL database are defined using a **Non-Business** sensitivity label.

6. Close the **Power BI** window, and in the bar on the left, select the icon for your workspace.

    Refresh the Workspace page if necessary to view all of the items it contains.

7. In the list of items in your workspace, note that the **Revenue by Item** report is listed.

## Review

In this exercise, In summary, these tasks led to the creation of a KQL database , the utilization of KQL to query the sales table , and the successful generation of a Power BI report from a KQL Queryset . The specific implementations and details varied based on the nature of the dataset and the analytical requirements.


## Proceed to next exercise
