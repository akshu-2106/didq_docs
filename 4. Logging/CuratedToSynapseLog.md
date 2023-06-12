# CuratedToSynapseLog

CuratedToSynapseLog is baseline table which is used to find the logs between curated to synapse layer. Whenever file is landed in curated layer it will be logged into table(It updates only source layer and target layer will be NULL). Once after completion of data process from curated to synapse,Target layer will be updated.

## Significance of Columns

| Column Name           	| 	Description	|
| :---        						| 	:--- 	|
|BusinessName	|	Defines Business Area	|
|Source	|	Source from where we want to pull your raw data e.g. EVENTHUB, ADLS	|
|SourceFile	| 	File name which is coming from Source	|
|SourceLayer	|	From which layer file coming.	|
|SourceStatus	|	Status of Source file. Ex:Whether it is successfully landed in Curated layer or not	|
|CuratedObject	|	Object name defined in curated layer.	|
|TargetLayer	|	Target layer	|
|Target Status	|	Target file status	|
|Comment	|	Comment about pipeline(ex;Run Completed)	|
|CuratedRowCount	|	Rows which are effected in Curated layer	|
|SourcePipelineRunID	|	ID is used to uniquely identify Source pipeline execution	|
|SourceLastUpdatedTime	|	Last updated time stamp for Source object	|
|TargetPipelineRunID	|	ID is used to uniquely identify target pipeline execution	|
|TargetLastUpdatedTime	|	Last updated time stamp for target location	|

## Logging table Configurations

* Database : ControlOps
* Configuration Table : EDNABatch.CuratedToSynapseLog

### Example

* DataProduct : Batch Data Product
* DataProductSchema : EDNABatch
* Metadata Table : CuratedToSynapseLog

### CntlPreMetadataFilelog Query

```sql
select * from EDNABatch.CuratedToSynapseLog
```
