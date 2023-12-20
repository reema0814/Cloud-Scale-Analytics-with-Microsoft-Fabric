### Create a Fabric workspace



#### Task 1.1: Assign Fabric Administrator Role

1. Start by searching for **Microsoft Entra ID** in the search pane in Azure portal:

   ![Navigate-To-AAD](./Images/ws/entra01.png)

2. Navigate to **Roles and administrators**:

   ![Roles-and-Administrator](./Images/ws/entraa002.png)

3. In the **Roles and administrators** page, search for **Fabric Administrator**, and click on it:

   ![search-fabric-admin](./Images/ws/entra020.png)

4. This will take you to the **Fabric Administrator | Assignments** page where you will have to assign yourself the **Fabric Administrator role**. Now, click on **+ Add Assignments**:

   ![click-add-assignments](./Images/ws/004.png)

5. Make sure to **check the box(1)** next to your username, confirm if it is **Selected(2)** and click on **Add(3)**:

   ![check-and-add-role](./Images/ws/005.png)

6. You can confirm the **Fabric Administrator** role has been added successfully by **refreshing(1)** Fabric Administrators | Assignments page. After **confirming(2)** it has been added successfully, navigate back to **Home(3)**.

   ![check-and-navigate-back-to-home](./Images/ws/006.png)

----

#### Task 1.2: Sign up for Microsoft Fabric Trial

1. Copy the **microsoft fabric homepage link**, and open this link inside the VM in a new tab:

   ```
   https://app.fabric.microsoft.com/
   ```


2. Select **Power BI**.

   ![Account-manager-start](./Images/ws/microsoftpage.png)

#### Task 1.3: Create a workspace

Here, you create a Fabric workspace. The workspace contains all the items needed for this lakehouse tutorial, which includes lakehouse, dataflows, Data Factory pipelines, the notebooks, Power BI datasets, and reports.

1.  Now, select **Workspaces** and click on **+ New workspace**:

    ![New Workspace](./Images/ws/workspace.png)

2. Fill out the **Create a workspace** form with the following details:

   - **Name:** Enter **fabric-<inject key="DeploymentID" enableCopy="false"/>**.
   

   ![name-and-desc-of-workspc](./Images/ws/workspacename.png)

   - **Advanced:** Expand it and Under **License mode**, select **Fabric capacity(1)**.

3. Select on exisitng **Capacity(2)** then click on **Apply(3)** to create and open the workspace.

   ![advanced-and-apply](./Images/ws/fabriccapacity.png)

    **Congratulations!** You have successfully learnt to create a Fabric workspace.

   ## Proceed to next exercise
