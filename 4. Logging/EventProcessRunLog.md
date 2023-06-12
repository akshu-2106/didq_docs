# Event Process Run Log

Event Process Run Log is another table provides input to Event process about the data transformations in different layers (Source -Raw-Stage-Curated). This table will describe detailed description of the Event process run logs.

## Significance of Columns

| Column Name           	| 	Description	|
| :---        						| 	:--- 	|
|ProcessRunlogId 	|		Defines Process Run log Id of ADF pipeline.	|
|SourceLayer		|	From where data needs to be fetched	|
|TargetLayer 		|	To where data needs to be stored	|
|ServiceCategory	|		Different data transformations in Source and Target Layer	|
|BusinessName		 |          Defines Business Area	|
|Object Name		  |  Object Name or Table Name as per DIDQ norms.  |
|FileName		|		File name of the object which contains the data.	|
|LoadFormat		|	What type of load(Full load/Incremental)	|
|RawFileLoadedTimeStamp	|     When the raw file loaded into the ADLS	|
|Status			|	Status of the raw file load whether Success or Fail.	|
|ProcessFlag 	|		ProcessFlag will be 1 if status is success, 0 if Fail.	|
|Comment 		|	Comments whether data transformations completed or not	|
|ProcessRunLoadTimeStamp	|    Entire Process run load timings	|
|PipelineName		|	Name of the pipeline which runs the process		.	|
|PipelineRunId		|	Run Id of the ADF pipeline.	|
|PipelineStartTime	|	Start time of the pipeline run.	|
|PipelineEndTime	|	End time of the pipeline run.	|

## Logging table Configurations

*	Database: ControlOps
*	Configuration Table: [EDNAWorkforce].[EventProcessRunlog]

### Example

*	DataProduct : Workforce Data Product
*	DataProductSchema : EDNA Workforce
*	Event Process Run Log Table: EventProcessRunlog
*	ObjectName : plant text

### Event Process Run Log Query

```sql
select * from [EDNABatch].[EventProcessRunlog]
where BusinessName= 'Batch_DataProduct'
AND CONVERT (date, PipelineStartTime) = CONVERT (date, CURRENT_TIMESTAMP)
ORDER BY PipelineStartTime asc , PipelineEndTime asc;
```
