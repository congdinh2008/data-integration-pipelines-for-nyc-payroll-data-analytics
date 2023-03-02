# Data Integration Pipelines for NYC Payroll Data Analytics
Project Introduction
The City of New York would like to develop a Data Analytics platform on Azure Synapse Analytics to accomplish two primary objectives:

1. Analyze how the City's financial resources are allocated and how much of the City's budget is being devoted to overtime.
2. Make the data available to the interested public to show how the City’s budget is being spent on salary and overtime pay for all municipal employees.

You have been hired as a Data Engineer to create high-quality data pipelines that are dynamic, can be automated, and monitored for efficient operation. The project team also includes the city’s quality assurance experts who will test the pipelines to find any errors and improve overall data quality.

The source data resides in Azure Data Lake and needs to be processed in a NYC data warehouse in Azure Synapse Analytics. The source datasets consist of CSV files with Employee master data and monthly payroll data entered by various City agencies.

<img src="./images/db-schema.jpeg" title="Database Schema">
NYC Payroll DB Schema

For this project, you'll do your work in the Azure Portal, using several Azure resources including:

- Azure Data Lake Gen2
- Azure SQL DB
- Azure Data Factory
- Azure Synapse Analytics

You'll take screenshots as proof of work for this project, so remember to collect these screenshots throughout the project steps. A checklist is provided at the end of each step so you can double-check you've collected all of the screenshot deliverables.

## Step 1: Prepare the Data Infrastructure
Setup Data and Resources in Azure

<img src="./images/step_1/create_all_resources.png" title="Create the data lake and upload data">

### 1. Create the data lake and upload data

<img src="./images/step_1/upload_file_to_data_lake_gen2_list_folder.png" title="Create the data lake and upload data">

<img src="./images/step_1/upload_file_to_data_lake_gen2_payroll_folder.png" title="Create the data lake and upload data">


<img src="./images/step_1/upload_file_to_data_lake_gen2_history_folder.png" title="Create the data lake and upload data">

### 2. Create an Azure Data Factory Resource

<img src="./images/step_1/create_all_resources.png" title="Create the data lake and upload data">

### 3. Create a SQL Database to store the current year of the payroll data

<img src="./images/step_1/create_sql_database.png" title="Create the data lake and upload data">
<img src="./images/step_1/Config_sql_networking.png" title="Create the data lake and upload data">
<img src="./images/step_1/Create_NYC_Payroll_Data_table_Sql.png" title="Create the data lake and upload data">


4. Create A Synapse Analytics workspace, or use one you already have created.

<img src="./images/step_1/Create_Synapse_Workspace.png" title="Create synapse tables">
<img src="./images/step_1/script_create_synapse_tables.png" title="Create synapse tables">


- All script in synapse branch git: synapse/sqlscript
- Create Emplyee Master Data table:

<img src="./images/step_1/create_synapse_NYC_Payroll_EMP_MD.png" title="Create synapse tables">

- Create Job Title Table:

<img src="./images/step_1/create_synapse_NYC_Payroll_TITLE_MD.png" title="Create synapse tables">

- Create Agency Master table:

<img src="./images/step_1/create_synapse_NYC_Payroll_Agency_MD.png" title="Create synapse tables">

- Create Payroll transaction data table:

<img src="./images/step_1/script_create_synapse_tables.png" title="Create synapse tables">


## Step 2: Create Linked Services

### 1.Create a Linked Service for Azure Data Lake

### 2.Create a Linked Service to SQL Database that has the current (2021) data

### 3. Create a Linked Service for Synapse Analytics


<img src="./images/step_2/linked_services_adf.png" title="Create all linked services">

## Step 3: Create Datasets in Azure Data Factory

### 1.Create the datasets for the 2021 Payroll file on Azure Data Lake Gen2

<img src="./images/step_3/ds_DelimitedText_nycpayroll_2021.png" title="Create all linked services">

### 2. Repeat the same process to create datasets for the rest of the data files in the Data Lake

- EmpMaster.csv

<img src="./images/step_3/ds_DelimitedText_EmpMaster.png" title="Create all linked services">

- TitleMaster.csv

<img src="./images/step_3/ds_DelimitedText_TitleMaster.png" title="Create all linked services">

- AgencyMaster.csv

<img src="./images/step_3/ds_DelimitedText_AgencyMaster.png" title="Create all linked services">

### 3. Create the dataset for transaction data table that should contain current (2021) data in SQL DB

<img src="./images/step_3/ds_AzureSqlTable_NYC_Payroll_Data.png" title="Data set file on Azure Data Lake Gen 2">

### 4. Create the datasets for destination (target) tables in Synapse Analytics

<img src="./images/step_3/ds_syn_NYC_Payroll_AGENCY_MD.png" title="Data set file on Azure Data Lake Gen 2">
<img src="./images/step_3/ds_syn_NYC_Payroll_Data.png" title="Data set file on Azure Data Lake Gen 2">
<img src="./images/step_3/ds_syn_NYC_Payroll_EMP_MD.png" title="Data set file on Azure Data Lake Gen 2">
<img src="./images/step_3/ds_syn_NYC_Payroll_TITLE_MD.png" title="Data set file on Azure Data Lake Gen 2">

## Step 4: Create Data Flows

### 1.In Azure Data Factory, create the data flow to load 2021 Payroll Data to SQL DB transaction table (in the future NYC will load all the transaction data into this table).

<img src="./images/step_4/df_loadFileNYCPayroll2021ToSqlDb.png" title="Data flow payroll to sql db">

### 2.Create Pipeline to load 2021 Payroll data into transaction table in the SQL DB

<img src="./images/step_4/pl_load2021PayrollDataintoSQLDb.png" title="Data flow payroll to sql db">
<img src="./images/step_4/pl_load2021PayrollDataintoSQLDb_success.png" title="Data flow payroll to sql db">
<img src="./images/step_4/pl_load2021PayrollDataintoSQLDb_check_query.png" title="Data flow payroll to sql db">

### 3. Create data flows to load the data from the data lake files into the Synapse Analytics data tables

<img src="./images/step_4/df_loadFileEmpMasterToSynTables.png" title="Data flow payroll to sql db">

<img src="./images/step_4/df_loadFileAgencyMasterToSynTables.png" title="Data flow payroll to sql db">

<img src="./images/step_4/df_loadFileTitleMasterToSynTables.png" title="Data flow payroll to sql db">


### 4. Create a data flow to load 2021 data from SQL DB to Synapse Analytics
<img src="./images/step_4/df_loadNYCPayroll2021ToSynTables.png" title="Data flow payroll to sql db">

### 5. Create pipelines for Employee, Title, Agency, and year 2021 Payroll transaction data to Synapse Analytics containing the data flows.

<img src="./images/step_4/pipeline_loadDataToSynapse_employee.png" title="Data flow payroll to sql db">

<img src="./images/step_4/pipeline_loadDataToSynapse_agency.png" title="Data flow payroll to sql db">

<img src="./images/step_4/pipeline_loadDataToSynapse_title.png" title="Data flow payroll to sql db">

<img src="./images/step_4/pipeline_loadDataToSynapse_Payroll2021.png" title="Data flow payroll to sql db">

### 6. Trigger and monitor the Pipelines

<img src="./images/step_4/pipeline_loadDataToSynapse_success.png" title="Data flow payroll to sql db">
<img src="./images/step_4/pipeline_loadDataToSynapse_check_query.png" title="Data flow payroll to sql db">


## Step 5: Data Aggregation and Parameterization

<img src="./images/step_5/data_flows_aggregate_data.png">


### 1.Create a Summary table in Synapse with the following SQL script and create a dataset named table_synapse_nycpayroll_summary

<img src="./images/step_5/">

### 2.Create a new dataset for the Azure Data Lake Gen2 folder that contains the historical files.

<img src="./images/step_5/filter_by_fiscal_year_payroll_aggregate_data.png">

### 3.Create new data flow and name it Dataflow Aggregate Data

<img src="./images/step_5/df_payroll_sql_aggregate_data.png">
<img src="./images/step_5/df_payroll_file_aggregate_data.png">

### 4.Create a new Union activity in the data flow and Union with history files

<img src="./images/step_5/union_payroll_aggregate_data.png">

### 5.Add a Filter activity after Union

<img src="./images/step_5/filter_by_fiscal_year_payroll_aggregate_data.png">

### 6.Derive a new TotalPaid column

<img src="./images/step_5/derived_TotalPaid_column_aggregate_data.png">

### 7.Add an Aggregate activity to the data flow next to the TotalPaid activity

<img src="./images/step_5/group_by_and_sum_payroll_aggregate_data.png">

### 8.Add a Sink activity to the Data Flow

<img src="./images/step_5/sink_to_synapse_table_aggregate_data.png">

### 9.Create a new Pipeline and add the Aggregate data flow

<img src="./images/step_5/pipeline_aggregate_data_create_global_parameter.png">

### 10.Validate, Publish and Trigger the pipeline. Enter the desired value for the parameter.

<img src="./images/step_5/pipeline_aggregate_data_using_global_parameter.png">
<img src="./images/step_5/pipeline_aggregate_data_trigger_global_parameter.png">

All Success
<img src="./images/step_5/all_pipelines_success.png">

Check pipeline aggregate data in synapse table
<img src="./images/step_5/pipeline_AggregateData_param_2020_check_query.png">
<img src="./images/step_5/pipeline_AggregateData_param_2021_check_query.png">

### 11.Monitor the Pipeline run and take a screenshot of the finished pipeline run.


## Step 6: Connect your Project to Github
<img src="./images/step_6/github_config.png">
