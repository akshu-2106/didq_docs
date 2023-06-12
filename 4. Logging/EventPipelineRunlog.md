# EventPipeline Run log

This is one of the main log tables used in DIDQ for data source which are Event based. It logs all the ADF pipeline runs when a files starts its loading process. We have different pipelines for handling different process and all those pipeline execution will be logged in this table. Whenever, there is a pipeline  failure, we can directly look at this table get the pipeline details and then search it in the ADF.

## Significance of column

| Column Name           	| 	Description	|
| :---        						| 	:--- 	|
|ProcessRunLogId	|	It is the ProcessRunLogId associated with the file which is logged from the processrunlog table.	|
|Target Layer	|	This indicates the layer to which the file will be loaded once the current pipeline finishes execution.	|
|BusinessName	|			Defines Business Area	|
|ObjectName		|		Object Name or Table Name as per the DIDQ norms	|
|FileName		|		Tells the name of the file processed.	|
|ServiceCategory	|	---	|
|Status	|	Tells us about the run status of pipeline is it failed or successful.	|
|ProcessFlag	|	Tells us the status of the pipeline run. 1 = success, 0 = failed.	|
|Comment		|	It gives current status like completed, started new, ignore.	|
|PipelineName	|	Name of the ADF pipeline.	|
|PipelineRunId	|	This is the ID which is generated when a pipeline is run in the ADF while processing the file, this ID is then logged in The EventPipelineRunlog table.	|
|PipelineStartTime	|	This gives us the timestamp of when the pipeline started the execution.	|
|PipelineEndTime	|	This gives us the timestamp of when the pipeline completed the execution.	|

## Event Log table configurations

*	Database: ControlOps
*	Event Log Table: [DataProductSchema]. [EventPipelineRunlog]

### Examples

*	DataProduct: Consumer Data Product
*	DataProductSchema: EDNAConsumer
*	Event Log Table: [EventPipelineRunlog]
*	ObjectName: reminders

### EventAuditLog table Query:

```sql
select * from [EDNAConsumer].[EventPipelineRunlog]
where BusinessName='Consumer_DataProduct' AND ObjectName in ('pets','reminders')
```
