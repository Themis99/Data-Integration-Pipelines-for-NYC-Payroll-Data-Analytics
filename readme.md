# Data Integration Pipelines for NYC Payroll Data Analytics
## project overview
The City of New York would like to develop a Data Analytics platform on Azure Synapse Analytics to accomplish two primary objectives:

Analyze how the City's financial resources are allocated and how much of the City's budget is being devoted to overtime.
Make the data available to the interested public to show how the City’s budget is being spent on salary and overtime pay for all municipal employees.

In this project a high-quality data pipelines that are dynamic, can be automated, and monitored for efficient operation will be created. The pipelines will also be tested by the city’s quality assurance experts who are part of the project team to identify any errors and improve overall data quality.

## Dataset
The source data resides in Azure Data Lake and needs to be processed in a NYC data warehouse in Azure Synapse Analytics. The source datasets consist of CSV files with Employee master data and monthly payroll data entered by various City agencies.

![db-schema](https://user-images.githubusercontent.com/46052843/217810408-44cca1a0-0e3f-47df-8d77-0aca632ab6fe.jpeg)

## Azure rescources:
Four Microsoft Azure resources have been created 
- Azure Data Lake Gen2
- Azure SQL DataBase
- Azure Data Factory
- Azure Synapse Analytics

The Data lake will be used to store the raw data but also as staging container when the pipelines will be deployed
The data will be stored in three distinct directories:
- dirpayrollfiles
- dirhistoryfiles
- dirstaging

The dirpayrollfiles will be used to store the payroll data for the year 2021 along with the Employee, Title, Agency data. The dirhistoryfiles will be used for storing the payroll data for the year 2020. The dirstaging will be used to store staging data during the execution of the Pipelines.

The SQL Database will be used to store the payroll data of the 2021 year 

In the Data factory the workflows and the pipelines will be created.




## Link services


