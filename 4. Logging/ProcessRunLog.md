# Process Run Log

This is one of the main log tables used in DIDQ for data source which are Event based. It tells all the processes running and gives us Status of Databricks Pipeline run log entry for every object & files. It is for the data when it is from Raw to Curated layer.

## Significance of column

| Column Name           	| 	Description	|
| :---        						| 	:--- 	|
|ProcessRunLogId	   |    It is the ProcessRunLogId associated with the file which is logged from the processrunlog table.	|
|Source Layer          |   Tells us at which layer of our delta storage the data is loaded.	|
|Target Layer           |     It is the layer in which the activity of DIDQ is performed.	|
|ServiceCategory        |	Tells us about the category of the service which the file processing is using.	|
|BusinessName		|		Defines Business Area	|
|ObjectName			|	Object Name or Table Name as per the DIDQ norms	|
|FileName			|	Tells the name of the file processed.	|
|LoadFormat	              |                       Declare your file as Incremental or Full_Load based on the file	|
|RawFileLoadedTimeStamp             |                 This is the time stamp at which it was loaded to the raw layer initially.	|
|ServiceCategory_Cd	  |    Each service name has a code associated with it and this gives us the code of the service used.	|
|Status	         |       Tells us about the status of file processing in relation to service category code.	|
|ProcessFlag	    |        Defines the state of the pipeline.	|
|Comment            |       Comment about pipeline (ex;Run Completed)	|
|ProcessRunLoadTimeStamp	 |   This is the exact timestamp of when the file passed through each layer of processing.	|
|PipelineName        |          This is the name of the pipeline which is running while this process.	|
|PipelineRunId	    |     This is the ID which is generated when a pipeline is run in the ADF while processing the file.	|
|PipelineStartTime	 |	This tells the Pipeline start time.	|
|PipelineEndTime      |     This tells the Pipeline end time.	|

## Logging table configurations

*	Database: ControlOps
*	Configuration Table: [DataProductSchema].[ProcessRunLog]

### Examples

*	DataProduct: Batch Data Product
*	DataProductSchema: EDNABatch
*	Metadata Table : ScheduleCntlMetadata

### ProcessRunLog table Query

```sql
select * from [EDNABatch].[ProcessRunlog]
where BusinessName= 'Batch_DataProduct'
AND CONVERT (date, PipelineStartTime) = CONVERT (date, CURRENT_TIMESTAMP)
ORDER BY PipelineStartTime asc , PipelineEndTime asc;
```
