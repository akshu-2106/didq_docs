# Data Ingestion & Data Quality Framework(DIDQ)

Data Ingestion and Quality Framework (DIDQ): I saw an opportunity to streamline and automate the processing of data that is being ingested into the enterprise Azure data platform. I went from the identification of the need/opportunity to the production delivery of a reusable Data Ingestion-Data Quality framework that was utilized on key programs supporting Stallion migrations and continues to be implemented in support of new data products. DIDQ enables automation for standard schema validation checks, data quality checks, and cleansing operations to support the data ingestion design pattern into our enterprise data lake and data warehouse environment. With this reusable, common component, teams across Elanco will be able to reuse the code - driving down costs, increasing speed of delivery by up to 70% for data products, and bringing down the risk of accumulating technical debt. The DIDQ framework is currently being deployed on projects in the M&Q, Commercial, and Marketing domains, other verticals with the expectation that this use continue to grow - broadening the impact and value of this delivery across Elanco. In addition to the technical delivery, this was an excellent example of collaboration amongst the data engineering team in the development, testing, and documentation of the solution across Internal and vendors partners. Partnered across IT to share progress, gather feedback, and incorporate new functionality - increasing the level of partnership and influence for the Elanco IAC (India office) teams across the broader IT organization.

## Data Ingestion & Data Quality Framework(DIDQ) Architecture Design

![Data Ingestion & Data Quality Framework(DIDQ)](./images/didq_architecture_design.png)

## Data Ingestion & Data Quality Framework(DIDQ) High Level Design

![Data Ingestion & Data Quality Framework(DIDQ)](./images/didq_high_level_design.png)

# Features 

* DIDQ is an Azure Driven Capability with Scala Code Base Framework
* Accelerator Path for Teams to Onboard Data into our Azure Platforms
* Leverages Delta Lake on Azure Data Lake Gen2
* Quick Refresh of Data on Azure Synapse and Cache (API) Layer

## Importance of Data Ingestion & Data Quality Framework(DIDQ)

* Giving Quality Controls to the Business or Project Owners
* Business Rules are easy to use
* Minimize manual work and redoing of same work
* Timespan of the Projects is reduced to ~80% - 90%
* Maximize reusability of the codes/projects and can be shared across domains/vertical teams very easily

# Technical Stack

The Data Ingestion and Data Quality (DIDQ) Azure Driven Capability is created using the whole Azure Stack, including: 
* Azure Data Factory
* Data Lake Storage in Azure Gen2 Databricks
* Azure SQL Database
* Analytics in Azure Synapse
* Azure Event Hub
* Stream Analytics with Spark

#### Contributions and Role: 
* I created the complete flow, including the implementation plan and high-level design(attached).

#### Metadata 
* Utilising the metadata methodology, all orchestration processes in Azure Data Factory were designed and created.

#### Databricks Scala Scripts 
* The Quality & Cleansing process uses written Scala scripts in Databricks, including Not Null Check, Deduplication, Column Validation, Datatype Check, Primary Key Check, Trim Service, and Incremental Processes.

#### SQL Database Logging
* The log table will record each action taken in relation to the databricks notebook. It will outline the services that are provided at each layer. A log serves as a comprehensive and accurate record of all activities that take place throughout the ETL process. It enables administrators to keep tabs on the ETL process and swiftly find and fix any problems that may crop up.

#### Azure Data Factory
* Information about configuring and transmitting metadata values through any Azure Data Factory (ADF) is contained in a table.

## Additional Features 
* Job Clusters
* Dynamic Schema
* SCIM provisioning
* Gib Hub integration
* Internal portal for sharing.

## Running Pilots: The last step is to design and launch a pilot using
* Unity Catalog
* Hybrid cloud (Azure & GCP)
* Databricks ML, and AI space.

## Results and Achievements: 
* Best of Tech Award winner for Global Elanco.

## Posted few more Databricks features that I am reading on Linkedin
* Linkedin : https://www.linkedin.com/in/sneh-gaur/

