# Configuration Properties Metadata

Properties metadata table defines the DIDQ Service Codes as Property Value and its respective descriptions.
This table provides the input to L3 Team and Maintenance Team during debugging of DIDQ processes.

## Significance of Columns

| Column Name           | Description                                                                                       |
| :---         | :---                                                                                     |
| PropertyId          | Defines Property Id                                                                              |
| PropertyValue            | Defines Property Value which will be used in DIDQ                                                                                       |
| Description      | Description of the Property values in DIDQ                                                |
| ValidFrom            | When the property is created      									|
| ValidFrom            | Till what time it will be valid, **NULL**  represents no expiry								|
| DataDomain            | Data Product Name     									|

## Metadata table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].ConfPropertiesMetadata

### Example

* DataProduct	: Batch Data Product
* DataProductSchema	: EDNABatch
* Metadata Table		: ConfPropertiesMetadata

### Source Control Metadata Query

```jsonc
SELECT * FROM EDNABatch.ConfPropertiesMetadata
```

|	PropertyId	|PropertyName	|PropertyValue	|Description	|ValidFrom	|ValidTo	|DataDomain	|
|	:---	|:---	|:---	|:---	|:---	|:---	|:---	|
|	1	|OverideRestart	|1	|For Re-Processing the same processed step but it should not failed step, Update ProcessFlag to -> 1 = Start New or 0 -> Restart	|2020-09-06 10:53:32.920	|NULL	|Batch_DataProduct	|
|	2	|IgnoreFailed	|-1	|To Ignore the failed step for next run, Update ProcessFlag to -> -1	|2020-09-06 10:54:35.823	|NULL	|Batch_DataProduct	|
|	3	|EmailAlerting	|1	|To Enable Pipeline email alerts via the database, 1 = Yes, 0 = No.	|2020-09-06 10:56:30.867	|NULL	|Batch_DataProduct	|
|	4	|Data_Quality_Datatype	|3	|Service Code for Data_Quality_Datatype	|2020-09-06 10:56:30.867	|NULL	|Batch_DataProduct	|
|	5	|Data_Quality_PrimaryKey	|4	|Service Code for Data_Quality_PrimaryKey	|2020-09-06 10:56:30.867	|NULL	|Batch_DataProduct	|
|	6	|Data_Cleansing_Trim	|2	|Service Code for Data_Cleansing_Trim	|2020-09-06 10:56:30.867	|NULL	|Batch_DataProduct	|
|	7	|Data_Cleansing_Dedup	|6	|Service Code for Data_Cleansing_Dedup	|2020-09-06 10:56:30.867	|NULL	|Batch_DataProduct	|
|	8	|Data_Cleansing_NotNull	|5	|Service Code for Data_Cleansing_NotNull	|2020-09-06 10:56:30.867	|NULL	|Batch_DataProduct	|
|	9	|Data_Ingestion_ColValidation	|1	|Service Code for Data_Ingestion_Column_Validation	|2020-09-06 10:56:30.867	|NULL	|Batch_DataProduct	|
|	10	|Data_CDC	|7	|Service Code for ChangeDataCapture_SCD2	|2020-12-18 07:22:16.953	|NULL	|Batch_DataProduct	|
