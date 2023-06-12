# Schedule Control Metadata

Schedule Control Metadata is a static baseline table to define the schedule of all objects in a data product for each source. This table provides input to Azure Data Factory(ADF) pipelines during each layer processing to ensure that object is running at the scheduled time.

## Significance of Columns

| Column Name           | Description                                                                                       |
| :---        			| :---                                                                                     |
| BatchID      		    |   Sequential Number                                                                            |
| BusinessName          | Defines Business Area                                                                            |
| SourceName            | Source Name                                                                                       |
| ObjectName            | Object Name or Table Name to be kept in ADLS                                                      |
| Source                | Source from where we want to pull your raw data e.g. EVENTHUB, ADLS                               |
| ProcessType 	       | Mechanism of defining the sourcing classified, its defined into categories: **pull**, **push**, **ext**, **event**|
| ADFName         	   | Azure Data Factory Name                                                                                       |
| Schdeule	     		| Define the schedule and frequency (e.g. Daily-2/Weekly-1)                           |
| Timings	            | Scheduled time for pipeline runs with comma separated                                            |
| LoadedTimeStamp       | Metadata Column to capture the record inserted Timestamp                                          |

### Process Type – Divided into Four Categories

* **ext** : This refers to Extract sources like RDBMS, API etc.
* **pull**  : This refers to the sources like SFTP path, any file server etc.
* **push**  : Refers to the source which want to push the data into ADLS.
* **event** : This refers to event hub sources.

## Metadata table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].[ScheduleCntlMetadata]

### Example

* DataProduct             : Batch Data Product
* DataProductSchema       : EDNABatch
* Metadata Table			: ScheduleCntlMetadata
* ObjectName              : plant_text

### Schedule Control Metadata Query

```jsonc
SELECT * FROM EDNABatch.ScheduleCntlMetadata where ObjectName='plant_text'
```

|BatchId  |BusinessName |SourceName |ObjectName |Source |ProcessType  |ADFName |Schdeule |Timings |LoadedTimeStamp  |
|:---     |:---         |:---       |:---       |:---   |:---		|:---		|:---    |:---    |:---       		|
|1		|Batch_DataProduct|	SAP		|plant_text	|	FS	|	pull	|	BPAZE1IBTDDDF01|	Daily-2|	03:30,15:30|	2021-10-19 12:44:14.7766667 |
