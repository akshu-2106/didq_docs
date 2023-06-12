# Pipeline Run Log

Pipeline Run Log is another table provides input to Azure Data Factory (ADF) Pipelines. This table will describe detailed description of the ADF pipeline runs.

## Significance of Columns

| Column Name           	| 	Description	|
| :---        						| 	:--- 	|
|ProcessRunlogId 			| Defines Process Run log Id of ADF pipeline.	|
|TargetLayer 			| To where data needs to be stored	|
|BusinessName		          | Defines Business Area	|
|Object Name		         |  Object Name or Table Name as per DIDQ norms.	|
|FileName			|	File name of the object which contains the data.	|
|ServiceCategory		|	-------	|
|Status			|	Status of the pipeline run whether **Success** or **Fail.**	|
|ProcessFlag 		|	ProcessFlag will be 1 if status is success, 0 if Fail.	|
|Comment 		|	comments whether pipeline completed successfully or not.	|
|PipelineName		|	Name of the ADF pipeline.	|
|PipelineRunId		|	Run Id of the ADF pipeline.	|
|PipelineStartTime	|	Start time of the pipeline run.	|
|PipelineEndTime	|	End time of the pipeline run.	|

More details of each column’s usage is explained in the respective services.

## Logging table Configurations

*	Database: ControlOps
*	Configuration Table: [EDNAWorkforce].[PipelineRunlog]

### Example

*	DataProduct : Workforce Data Product
*	DataProductSchema : EDNA Workforce
*	Metadata Table: PipelineRunlog
*	ObjectName : plant text
