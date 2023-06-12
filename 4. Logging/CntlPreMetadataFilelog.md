# CntlPreMetadataFilelog

CntlPreMetadataFilelog is baseline table which is mainly used for handling the multiple files(File Handling) for single object. Initially all the file records w.r.t each object will be updated into this table after that will apply sorting mechanism. Based on sorting results, Old file will be an input for CntlMetadataFileLog to complete further process. This process will be applied for remaining files as well which are updated as file records in CntlPreMetadataFilelog.

## Significance of Columns

| Column Name           	| 	Description	|
| :---        						| 	:--- 	|
|ExecutionId	|	Key is used to uniquely identify one execution	|
|ProcessLayer	|	In which stage it's running(Ex:Raw/Stage/…etc)	|
|BusinessName	|	Defines Business Area	|
|SourceName	|	Source Name	|
|ObjectName	|	Object Name or Table Name to be kept in ADLS	|
|Source	|	Source from where we want to pull your raw data e.g. EVENTHUB, ADLS	|
|ProcessType	|	Mechanism of defining the sourcing classified, its defined into categories: pull, push, ext, event	|
|LandingRawPath	|	Raw source path which will keep a copy of source data i.e. Raw/source/	|
|FileName	|	File Name	|
|SchemaFileName	|	Defines the Source Schema Name	|
|FileFormat	|	In which format you are/want to keep your file e.g. csv,json	|
|FileLandingTime	|	File copied time stamp to stage	|
|LoadedTimeStamp	|	Metadata Column to capture the record inserted Timestamp	|
|ProcessFlag	|	Defines the state of the pipeline	|
|Status	|	Status of pipeline(ex:Success/Failure)	|
|Comment	|	Comment about pipeline(ex;Run Completed)	|
|LoadFormat	|	Declare your file as Incremental or Full_Load based on the file type	|
|PipelineRunId	|	ID of the pipeline that triggers the pipeline run	|
|PipelineName	|	Pipeline name which is defined in ADF	|
|PipelineStartTime	|	Pipeline start time	|
|PipelineEndTime	|	pipeline end time	|

## Logging table Configurations

* Database : ControlOps
* Configuration Table : [DataProductSchema].[CntlPreMetadataFilelog]

### Example

* DataProduct : Batch Data Product
* DataProductSchema : EDNABatch
* Metadata Table : ScheduleCntlMetadata

### CntlPreMetadataFilelog Query

```sql
select * from EDNABatch.CntlPreMetadataFilelog
```
