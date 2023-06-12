# Source Control Metadata

Source driven baseline table to define the below mentioned metadata columns of Source, Object, Azure Storage Mapping like Source Name, Source Object Name/Table Name for the Business Name that you want to enable in DIDQ.
This table provides input to Azure Data Factory(ADF) pipelines during sourcing the data from different sources and putting into Azure Storage(Raw Zone).

## Significance of Columns

| Column Name           | Description                                                                                       |
| :---         | :---                                                                                     |
| BusinessName          | Defines Business Area                                                                             |
| SourceName            | Source Name                                                                                       |
| SourceObjectName      | Object Name or Table Name coming from source                                                      |
| ObjectName            | Object Name or Table Name to be kept in ADLS                                                      |
| Source                | Source from where we want to pull your raw data e.g. EVENTHUB, ADLS                               |
| Format                | In which format you are/want to keep your file e.g. csv,json                                      |
| Process Type          | Mechanism of defining the sourcing classified, its defined into categories: **pull**, **push**, **ext**, **event**|
| SourcePath            | Source Path                                                                                       |
| LandingRawPath        | Raw source path which will keep a copy of source data i.e. **Raw/source/**                            |
| RawObjectName         | Raw Object Name or Table Name                                                                     |
| RawPath               | Raw Object Path for Delta Tables                                                                  |
| StageObjectName       | Stage Object Name or Table Name                                                                   |
| StagePath             | Stage Object Path for Delta Tables                                                                |
| RejectedObjectName    | Stage Rejected Object Name or Table Name                                                          |
| RejectedPath          | Stage Rejected Object Path for Delta Tables                                                       |
| CuratedObjectName     | Curated Object Name or Table Name                                                                 |
| CuratedPath           | Curated Object Path for Delta Tables                                                              |
| ActiveInd             | Activate or De-Activate the Object Name or Table Name                                             |
| HeaderInd             | Define **Y** if file is having Header, **N** if file is not having Header                             |
| SchemaFileInd         | Defined for SAP sources which generates Schema File, make it **Y** else **N**                             |
| DelimiterInd          | Define File delimiter                                                                             |
| CDCInd                | Activate Change Data Capture as a service make it **Y** else **N**                                        |
| SynapseRefreshInd     | Refresh the Synapse Layer using Curated Data make it **Y** else **N**                                    |
| LoadFormat            | Declare your file as **Incremental** or **Full_Load** based on the file type                              |
| LoadedTimeStamp       | Metadata Column to capture the record inserted Timestamp                                          |

### Process Type – Divided into Four Categories

* **ext** : This refers to Extract sources like RDBMS, API etc.
* **pull**  : This refers to the sources like SFTP path, any file server etc.
* **push**  : Refers to the source which want to push the data into ADLS.
* **event** : This refers to event hub sources.

## Metadata table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].SourceCntlMetadata

### Example

* DataProduct             : Batch Data Product
* DataProductSchema       : EDNABatch
* Metadata Table  : SourceCntlMetadata
* ObjectName              : plant_text

### Source Control Metadata Query

```jsonc
SELECT * FROM EDNABatch.SourceCntlMetadata where ObjectName='plant_text'
```

|BatchId  |BusinessName |SourceName |SourceObjectName |ObjectName |Source |Format |ProcessType  |SourcePath |LandingRawPath |RawObjectName  |RawPath  |StageObjectName  |StagePath  |RejectedObjectName |RejectedPath |CuratedObjectName  |CuratedPath  |ActiveInd  |HeaderInd  |SchemaFileInd  |DelimiterInd |CDCInd |SynapseRefreshInd  |LoadFormat |LoadedTimeStamp  |
|:---   |:---  |:---  |:---  |:---  |:---  |:---  |:---   |:---  |:---  |:---   |:---   |:---   |:---   |:---  |:---  |:---   |:---   |:---   |:---   |:---   |:---  |:---  |:---   |:---  |:---  |
1|	Batch_DataProduct|	SAP|	Plant_Text|	plant_text|	FS|	csv|	pull|	\MD\SC|	Raw/source/plant_text|	plant_text|	Raw/plant_text|	plant_text|	Stage/plant_text|	plant_text|	Stage/rejected/plant_text|	plant_text|	Curated/plant_text|	Y|	N|	Y|	\|         |	Y|	Y|	Full_Load|	2020-11-02 14:33:19.9866667 |
