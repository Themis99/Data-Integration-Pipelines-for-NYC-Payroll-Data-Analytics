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

In the sypapse analytics a dedicated SQL pool will be created. Inside the pool four tables will be created and used to store the data for the Employees, Title and Agency and 2021 payroll data.

## link services and Dataset creation
Inside the Data factory 
The Azure synapse, SQL Database and Data lake will be linked. For every table or csv file inside the linked services a Dataset is created.

![linked servises](https://user-images.githubusercontent.com/46052843/217815038-39d8892f-6add-4350-ae5b-cf7aa7358ced.png)



## Workflows and Pipelines creation 

We create five workflows

- One workflow for storing the payroll data for year 2021 to the SQL DB

- One workflow for storing the payroll data for year 2021 to the synapse dedicated pool

- One workflow for storing the Agency Master data to the synapse dedicated pool

- One workflow for storing the Employee Master data to the synapse dedicated pool

- One workflow for storing the Title Master data to the synapse dedicated pool

For every workflow we also create a pipeline:

- A pipeline for storing the payroll data for year 2021 to the SQL DB:

![Pipeline load 2021 payroll into SQLDB](https://user-images.githubusercontent.com/46052843/217819093-75d6e4b3-76a5-4403-a924-e17ba439533a.png)

- A pipeline for storing the payroll data for year 2021 to the synapse dedicated pool:

![Pipeline Load Year 2021 to Synapse](https://user-images.githubusercontent.com/46052843/217819103-5e830e72-7b95-4d75-8fe5-61aa889e6d08.png)

- A pipeline for storing the Agency Master data to the synapse dedicated pool:

![Pipeline Load Agency Master to Synapse](https://user-images.githubusercontent.com/46052843/217819096-f11dafe4-bde2-4449-98d9-2e5e1ad995b5.png)

- A pipeline for storing the Employee Master data to the synapse dedicated pool:

![Pipeline Employee Master to Synapse](https://user-images.githubusercontent.com/46052843/217819087-46e4a676-4836-4b86-b631-921d64288c6b.png)

- A pipeline for storing the Title Master data to the synapse dedicated pool:

![Pipeline load Title Master to Synapse](https://user-images.githubusercontent.com/46052843/217819099-4cc13d2b-bede-456e-891b-73627c526234.png)

## Data aggregation 
In this step, the 2021 and 2020 payroll year data will be extracted and then merged. Afterwards, aggregation will be performed on the Agency Name, Fiscal Year, and TotalPaid, and the result will be stored in the dedicated synapse pool.

Firstly a new dataset containing the 2020 payroll dataset is created. Also a Table that will store the aggregation results is created in the dedicated SQL pool

A new workflow is created that will aggregate the data. In the first step of the workflow the 2021 and 2020 payroll datasets are loaded and then the union of this datasets is created. Then the fiscal year is filtered based on a parameter (the parameter could be 2020 or 2021). A TotalPaid column is created (derived column) that is equal to RegularGrossPaid + TotalOTPaid + TotalOtherPay. Finally, the TotalPaid is grouped by the AgencyName column and Fiscal Year column.




