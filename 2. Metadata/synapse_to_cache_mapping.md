# Synapse To Cache Mapping

Synapse To Cache Mapping is another baseline table to define the Business Rules of Cache tables destination and their Source Synapse tables.
This table provides input to Azure Data Factory (ADF) Pipelines to copy the data from synapse to the cache layer.

## Significance of Columns

| Column Name |  Description |
| :---  |  :--- |
|ID |  Defines the id |
|BusinessName |  Defines your Business Area |
|TargetLayer |  Defines the layer of Target destination |
|ObjectName |  Object Name or Table Name as per **DIDQ norms** |
|SourceSchemaName |  Defines the Source Schema Name |
|SourceObjectName |  Defines the Synapse Table or View |
|SourceQuery  | Defines the query which will be used to extract data from synapse |
|DestinationSchemaName | Defines the Target Schema Name |
|DestinationObjectName | Defines the Target Cache Table |
|WaterMarkCol | Metadata column shows the last update |
|FilterCols | Indicates the column by which the load takes place |
|LoadType  | Define Load Type either its Insert **I**, Upsert **U**, FullLoad **F**,Delete **D** |
|ActiveInd | Activate or De-Activate the cache load |
|LoadedTimeStamp | Metadata Column to capture the record inserted Timestamp |

## Metadata table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].SynapseToCacheMapping

### Example

* DataProduct             : Batch Data Product

* DataProductSchema       : EDNABatch
* Metadata Table  : SynapseToCacheMapping
* ObjectName              : process_orders
* Source Object Name              : vw_EntityBatch

### Synapse to Cache Mapping Query

```SQL

select * from EDNABatch.[SynapseToCacheMapping] where objectname='process_orders' and sourceobjectname='vw_EntityBatch'

```

|ID |BusinessName |TargetLayer |ObjectName |SourceSchemaName |SourceObjectName |SourceQuery |DestinationSchemaName |DestinationObjectName |WaterMarkCol |FilterCols |LoadType |ActiveInd |LoadedTimeStamp |
|:--- |:--- |:--- |:--- |:---   |:---   |:---   |:---   |:---   |:---   |:---   |:---   |:---   |:--- |  
|3 |Batch_DataProduct |Cache |process_orders |EDNABatch |vw_EntityBatch |Query |EDNABatch |EntityBatch |LastUpdated |Filter Id |F |Y |2021-09-15 15:08:35.2933333 |
