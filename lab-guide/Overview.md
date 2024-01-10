# Cloud scale analytics with Microsoft Fabric

## Overview

Microsoft Fabric serves as a holistic analytics solution designed for enterprises, encompassing everything from data movement to data science, Real-Time Analytics, and business intelligence. This inclusive platform provides a full suite of services, incorporating data lake management, data engineering, and data integration seamlessly.

Microsoft Fabric is an exciting addition to Microsoft’s suite of data analytics solutions. With its all-in-one analytics platform, organizations can leverage the power of data engineering, data integration, real-time analytics, data science, and business intelligence, all in a single unified environment. The seamless integration with other Azure services, robust security features, and extensibility options make this product a compelling choice for enterprises seeking end-to-end data analytics solutions.

### Key features of Microsoft Fabric

**Data Engineering** - Data Engineering experience provides a world class Spark platform with great authoring experiences, enabling data engineers to perform large scale data transformation and democratize data through the lakehouse. Microsoft Fabric Spark's integration with Data Factory enables notebooks and spark jobs to be scheduled and orchestrated. 

**Data Factory** - Azure Data Factory combines the simplicity of Power Query with the scale and power of Azure Data Factory. You can use more than 200 native connectors to connect to data sources on-premises and in the cloud. For more information, see What is Data Factory in Microsoft Fabric?

**Data Science** - Data Science experience enables you to build, deploy, and operationalize machine learning models seamlessly within your Fabric experience. It integrates with Azure Machine Learning to provide built-in experiment tracking and model registry. Data scientists are empowered to enrich organizational data with predictions and allow business analysts to integrate those predictions into their BI reports. This way it shifts from descriptive to predictive insights.

**Data Warehouse** - Data Warehouse experience provides industry leading SQL performance and scale. It fully separates compute from storage, enabling independent scaling of both the components. Additionally, it natively stores data in the open Delta Lake format. 
Real-Time Analytics - Observational data, which is collected from various sources such as apps, IoT devices, human interactions, and so many more. It's currently the fastest growing data category. This data is often semi-structured in formats like JSON or Text. It comes in at high volume, with shifting schemas. These characteristics make it hard for traditional data warehousing platforms to work with. Real-Time Analytics is best in class engine for observational data analytics.

**Power BI** - Power BI is the world's leading Business Intelligence platform. It ensures that business owners can access all the data in Fabric quickly and intuitively to make better decisions with data.

## Sandbox Scenario

Contoso Corporation, a large enterprise operating in diverse industries, recognizes the critical importance of leveraging data for strategic decision-making. Facing challenges with disparate data services and an increasingly complex analytics landscape, Contoso has decided to renovate its approach by adopting Microsoft Fabric. This decision stems from the company's vision to streamline and consolidate all data-related processes, encompassing data movement, data engineering, real-time analytics, and business intelligence, into a unified and integrated platform.


## About the Sandbox

Using this environment, you'll be able to explore complete features and offerings offered by Microsoft Sentinel. Please find the detailed overview of the sandbox environment below.

### Pre-provisioned resources

#### Virtual Machine: 

- 1 *Windows Server 2022 Datacenter* Virtual machines. As part of the automation, resources linked to virtual machines, including virtual networks, network security groups, managed disks, network interface cards, and IP addresses, are deployed.

  These virtual machines are tailored and configured to the sandbox's specifications. Files, applications, packages, and OS configurations are all pre-configured. It is 
  recommended that you use the same virtual machine throughout the lab for the best experience.

#### License and subscription: 

- You'll have access to a pre-configured Microsoft user account with an active Azure subscription and a tenant. 
   
  User account has assigned as Owner at subscription and Global administrator at the tenant level. You need to use the same user account throughout the lab to get the most out of the lab. 

#### Azure Credits: 

- You have been given a quota of **$180** which includes the running cost of pre-deployed resources, license cost, and other resources deployed while running through the lab.

  You will receive **cost alerts** to your registered email address at **50%/75%/90%/95%/100%** of the allotted Azure Credit is spent.

  You can visit the Azure Subscription page to check the current Azure credit spend and Analysis on **Cost analysis** tab under the Cost Management option.

  ![Picture 1](./media/o1.jpg)

#### Duration and Deletion of sandbox:  

- The sandbox environment will be active for **14 days/336** hours from the time of registration. 
- The maximum allowed virtual machine uptime is only **40 hours**. It is recommended to deallocate the virtual machine when not in use.
- The virtual machine is set up with a custom feature called Idle start/stop. This custom package will check the virtual machine's idleness every **2 hours/120 minutes**. If the 
  virtual machine is left idle for over 2 hours, a pop-up window will appear, prompting you to respond. If you do not take action within 10 minutes, the virtual machine will 
  shutdown automatically. This feature is enabled in virtual machines to optimize Azure costs.
- When 100% of Azure credits are spent, the sandbox environment will get automatically deleted without any prior notification. To retain the environment for a longer period and to get the most out of the environment, please follow the best practices mentioned below.

#### Best practices: 

- **Resources usage**: Please stop the virtual machines and other resources when not in use to minimize the Azure spend.

- **Azure Cost Analysis**: Maintain a practice of checking the Cost Analysis report of the assigned Azure subscription often in check the Azure spending so that the environment 
  can be retained for a longer duration of time.

- **Alert notifications**: Make sure to check your registered email's inbox for any alert-related mails. Alerts give you can head start to keep your Azure spending in control and to plan out the remaining credits in the best way possible.

## Lab guide Content

You will have access to a lab guide which is a reference material to assist you in getting started with the exploration.

Based on your interests, you can use this lab guide as a reference to learn and test any Microsoft Fabric feature. You are also encouraged to explore additional features of Microsoft Fabric based on your interests and preferences.

- Lab 01 - Getting Started with Microsoft Fabric
- Lab 02 - Cloud-Scale-Analytics-with-Microsoft-Fabric
- Lab 03 - Cloud-Scale-Analytics-with-Microsoft-Fabric
- Lab 04 - Use Delta tables in Apache Spark
- Lab 05 - Cloud-Scale-Analytics-with-Microsoft-Fabric
- Lab 06 - Create a Dataflow (Gen2) in Microsoft Fabric
- Lab 07 - Analyze data in a data warehouse
- Lab 08 - Get started with Real-Time Analytics in Microsoft Fabric
- Lab 09 - Use notebooks to train a model in Microsoft Fabric

### Azure services and related products:

- Microsoft Entra ID


