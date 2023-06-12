# Source File Metadata

Source File Metadata is baseline table to define the source file details and used in pre-sourcing of files.. This table provides input to Azure Data Factory(ADF) pipelines during sourcing the data from different source files and putting into Azure Storage(Raw Zone).

## Significance of Columns

| Column Name | Description |
| :--- | :--- |
| BatchID | Sequential Number |
| BusinessName | Defines Business Area |
| SourceName | Source Name |
| SourceObjectName | Object Name or Table Name coming from source |
| ObjectName | Object Name or Table Name to be kept in ADLS |
| Source | Source from where we want to pull your raw data e.g. ADLS |
| ProcessType | Mechanism of defining the sourcing classified, its defined into categories: **pull**, **push**, **ext** |
| SourcePath | Source Path |
| LandingRawPath | Raw source path which will keep a copy of source data i.e. **Raw/source/** |
| ActiveInd | Activate or De-Activate the Object Name or Table Name |
| LoadFormat | Declare your file as **Incremental** or **Full_Load** based on the file type |
| LoadedTimeStamp | Metadata Column to capture the record inserted Timestamp |

## Process Type – Divided into Four Categories

* **ext** : This refers to Extract sources like RDBMS, API etc.
* **pull**  : This refers to the sources like SFTP path, any file server etc.
* **push**  : Refers to the source which want to push the data into ADLS.
* **event** : This refers to event hub sources.

## Metadata table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].SourceFileMetadata

### Example

* DataProduct             : Batch Data Product
* DataProductSchema       : EDNABatch
* Metadata Table  : SourceFileMetadata
* ObjectName              : plant_text

### Source File Metadata Query

```SQL
SELECT * FROM EDNABatch.SourceFileMetadata where ObjectName='plant_text'
```

|BatchId |BusinessName |SourceName |SourceObjectName |ObjectName |Source |ProcessType |SourcePath |LandingRawPath |ActiveInd |LoadFormat |LoadedTimeStamp |
|:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |:--- |
|1|Batch_DataProduct|	SAP|	Plant_Text|	plant_text|	FS|	pull|	\MD\SC|	Raw/source/plant_text| Y|	Full_Load|	2020-11-02 14:33:19.9866667 |
