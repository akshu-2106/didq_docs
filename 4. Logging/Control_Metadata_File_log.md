# Control Metadata File log

Control Metadata File_log is log mechanism table, whenever data processed from source to ADLS(Raw-source) it will be logged in  Control Metadata File log. Source – Raw pipeline in ADF will log files in CntlMetadataFilelog

## Significance of Columns

| Column Name           	| 	Description	|
| :---        						| 	:--- 	|
|ExecutionId       |      It’s a unique ID generated while executing pipeline. These values are generated from system variables through ADF.	|
|ProcessLayer      |       In this column we can find to which layer the file have been processed.	|
|BusinessName   |     On which Data product its referring to.	|
|SourceName      |     It will tells from which source data coming from example: SAP , Veevanetwork	|
|ObjectName    |    This column will refer in Data product what is the object we are processing.	|
|Source          |    Source from which source_data being received can be identified in this column.	|
|ProcessType    |   It will define how data retrieved from source either push, pull or extract.	|
|LandingRawPath	|  Landing path from source to ADLS can be identified from this column.	|
|FileName     |     Source file name can be identified in this column.	|
|SchemaFileName	|  In this column we can identify the schema file name which are mapped with Source filename.	|
|FileFormat    |   Format of file can be identified in this column example: CSV,Excel, Json.	|
|FileLandingTime	|  It will define timestamp of file landed from source.	|
|LoadedTimeStamp	|  When we load data from source - Raw(source) its being captured in this column.	|
|ProcessFlag	|  It will define the status of the layer whether it is success(1) or failure(0).Processflag -1 will ignore those file and process to next step.	|
|Status	| Status of pipeline is defined in this column.	|
|Comment	|  Pipeline status are commented in this column.	|
|LoadFormat	|  We can find the type of load from this column either it’s full load or Incremental.	|
|PipelineRunId | Its metadata column which has unique ID while executing pipeline. These values are generated from system variables through ADF.	|
|PipelineName	|  It’s a metadata column which has pipeline name that has been executed.	|
|PipelineStartTime	| It’s a metadata column which has pipeline start time these values are generated from ADF	|
|PipelineEndTime	|  It’s a metadata column which has pipeline end time these values are generated from ADF	|

## Logging table Configurations

*	Database: ControlOps
*	Configuration Table : [DataProductSchema].CntrIMetadataFilelog

### Example

*	DataProduct : Batch Data Product
*	DataProductSchema : EDNABatch
*	Metadata Table: CntrIMetadataFilelog
*	ObjectName : batch_charateristics

### Service Control Metadata Query

```sql
select * from EDNABatch.CntlMetadataFilelog where ObjectName = 'batch_charachterstics'
```
