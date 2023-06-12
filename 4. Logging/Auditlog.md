# Audit log

Audit_log table will log each step performed with respect to databricks notebook. It will define what are all service being performed in each layer.
The purpose of an audit log is to provide a complete and accurate history of all activities that occur during the ETL process. It allows administrators to track and monitor the ETL process and quickly identify and resolve any issues that arise.

## Significance of Columns

| Column Name           	| 	Description	|
| :---        						| 	:--- 	|
|AuditLogId           |            It is a unique ID generated while executing pipeline with respect to services in each layer.	|
|ProcessRunlogId       |       These are process Id generated in process run log table and mapped in auditlog with respect to each layer.	|
|BusinessName           |        This column will define the business name on which pipeline is executed. These parameters are defined in ADF.	|
|ObjectName    |      We can identify on which object the DIDQ services are being implemented. Basically, it will define the object name on which databricks validation happened.	|
|StorageLayer    |     This column will identify the layer on which file being processed eg: Raw/Stage/Curated.	|
|ServiceCategory  |  The ServiceCategory in an audit log table is a field that categorizes the type of service that performed the action being recorded in the log. The ServiceCategory field can be helpful for grouping and analyzing the performance of different types  services and identifying any trends or issues related to a particular category of services.	|
|ServiceName	|  The ServiceName in an audit log table typically refers to the name or identifier of the specific service or application that performed the action being recorded in the log.  The ServiceName field can be helpful for tracking and analyzing the performance of service and identifying any issues or errors that may be specific to a particular service.	|
|FileName    |    The FileName in an audit log table typically refers to the name of the file that is being processed during an ETL (Extract, Transform, Load) operation.	|
|ServiceCategory_Cd      |     The ServiceCategory_Cd (or ServiceCategory Code) in an audit log table is a code or identifier that represents the category of service or application that performed the action being recorded in the log. The ServiceCategory_Cd field can be helpful for grouping and analyzing the performance of different types of services using standardized codes or identifiers.	|
|Status	|    The Status in an audit log table typically refers to the result or outcome of the action being recorded in the log. In the context of an ETL process, the Status field in the audit log might indicate the success or failure of a specific ETL operation.	|
|Description	|	  The Description field can be helpful for providing additional context and details about the actions that were performed during the ETL process. It can also be useful for troubleshooting and debugging purposes, as it can help identify specific issues or errors that may have occurred during the process.	|
|SourceColCount	|    In an ETL process, data is often extracted from a source system or file, transformed into a format that can be loaded into a target database or system, and then loaded into the target. The  SourceColCount field in the audit log would typically contain the number of columns or fields present in the  source data that was processed during this operation.	|
|ResultRowCount	|  In an ETL process, data is often extracted from a source system or file, transformed into a format that can be loaded into a target database or system, and then loaded into the target. The ResultRowCount field in the audit log would typically contain the number of rows or records that were successfully processed and loaded into the target system.	|
|PipelineRunId	|    The PipelineRunId in an audit log table typically refers to a unique identifier assigned to a specific run.	|
|LoadTimestamp	|    The LoadTimestamp in an audit log table typically refers to the date and time when a specific set of data was loaded into a target system.	|
|Datepart  |  The Datepart in an audit log table typically refers to a specific part or component of a date and time value that is recorded.	|

## Logging table Configurations

*	Database: ControlOps
*	Configuration Table : [DataProductSchema]. AuditLog

### Example

*	DataProduct : Batch Data Product
*	DataProductSchema : EDNABatch
*	Metadata Table: AuditLog

### AuditLog Query

```sql
select * from [EDNABatch].[AuditLog]
where BusinessName='Batch_DataProduct'
AND CONVERT(date, LoadTimestamp) = CONVERT (date, CURRENT_TIMESTAMP)
ORDER BY LoadTimestamp,ServiceCategory_Cd,FileName;
```
