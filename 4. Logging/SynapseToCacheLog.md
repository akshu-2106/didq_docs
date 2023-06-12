# SynapseToCache Log

SynapseToCacheLog is a baseline table which logs the Synapse to Cache Log entry for every object files. For all the object names it tells us the load type and the timing as well.

## Significance of column

| Column Name           	| 	Description	|
| :---        						| 	:--- 	|
|DestinationObjectName	|	Destination Object Name as per the DIDQ norms for different object types.	|
|LoadType                 |                                   Tells us the type of load if its loaded fully, deleted and then got loaded or got updated.	|
|Row count                   |                              Gives us the count of the new or updated row in the current file which was processed.	|
|Last updated time	|	Time when the load is completed, and all the files are loaded.	|

## Logging table configurations

*	Database: ControlOps
*	Configuration Table: [DataProductSchema].[ SynapseToCacheLog]

## Examples

*	DataProduct: Batch Data Product
*	DataProductSchema: EDNABatch
*	Metadata Table : ScheduleCntlMetadata

### SynapseToCacheLog table Query

```sql
select DestinationObjectName,LoadType, Row_Count, LastUpdatedTime from [EDNABatch].[SynapseToCacheLog]
Where BusinessName = 'Batch_DataProduct'
AND CONVERT (date, LastUpdatedTime) = CONVERT (date, CURRENT_TIMESTAMP)
Order by ObjectName
```
