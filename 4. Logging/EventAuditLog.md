# EventAuditLog

This is one of the main log tables used in DIDQ for data source which are Event based . It logs all data services and changes a file goes through starting from source layer to curated layer. Whenever, there is a failure, we can directly look at the Status column and description column to see the error message.

## Significance of column

| Column Name           	| 	Description	|
| :---        						| 	:--- 	|
|AuditLogId	|	Sequential ID is generated to log the changes ,a file goes through in every step of processing.	|
|ProcessRunLogId	|	It is the ProcessRunLogId associated with the file which is logged from the processrunlog table.	|
|BusinessName	|			Defines Business Area	|
|ObjectName		|		Object Name or Table Name as per the DIDQ norms	|
|StorageLayer	|	Tells us at which layer of our delta storage the data is loaded.	|
|ServiceCategory	|	Tells us about the category of the service which the file processing is using.	|
|ServiceName	|	Each service Category have different services under it Service Name tells us about the name of the particular service used.	|
|FileName		|		Tells the name of the file processed.	|
|ServiceCategory_Cd	|	Each service name has a code associated with it and this gives us the code of the service used	|
|Status	|	Tells us about the status of file processing in relation to service category code.	|
|Description	|	Tells us the brief detail of the process the file is going through.	|
|SourceColCount	|	Gives us the count of column present in the source file being processed.	|
|ResultRowCount	|	Gives us the count of the new or updated row in the current file which was processed.	|
|PipelineRunId	|	This is the ID which is generated when a pipeline is run in the ADF while processing the file, this ID is then logged in The EventPipelineRunlog table which we are also using in EventAuditlog.	|
|LoadTimeStamp	|	This is the exact timestamp of when the file passed through each layer of processing.	|
|Datepart		|		This is the date when the file was processed.	|

## Logging table configurations

*	Database: ControlOps
*	Event Log Table: [DataProductSchema].EventAuditLog

### Examples

*	DataProduct: Consumer Data Product
*	DataProductSchema: EDNAConsumer
*	Event Log Table: EventAuditLog
*	ObjectName: reminders

### EventAuditLog table Query

```sql
select * from [EDNAConsumer].[EventAuditLog]
where BusinessName='Consumer_DataProduct' AND ObjectName in ('pets','reminders')
```
