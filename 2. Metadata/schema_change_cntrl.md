# Schema Change Control

This Meta data table has the control of Dynamic schema. Dynamic schema will look for this table and create/recreate the tables.

## Significance of Columns

| Column Name           | Description                                                                                       |
| :---         | :---                                                                                     |
|BusinessName          	| 	Defines Business Area	|
|SourceName          	| 	Source Name                                                                                       |
|ObjectName          	| 	Object Name or Table Name to be kept in ADLS                                                      |
|TblSchemaName          	| 	Indicate the schema in which table should be created                                                      |
|TblCreateInd          	| 	Indicates wheather the table should be created or not N= to be created , Y = Created
|ActiveInd          	| 	Activate or De-Activate the Object Name or Table Name                                             |
|DeltaTableLayer          	| 	Indicates the layer in which it should be indicates                                             |
|LayerSequence          	| 	Indicates the LayerSequence in which it should be indicates                                             |
|IncludeRejected          	| 	Indicates wheather it contains rejected layer                                             |
|Scenario_Identifier          	| 	Indicates which Scenario should get executed                                             |

## Metadata table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].SchemaChangeCntrl
* Configuration Columns : SourceName,ObjectName, TblschemaName, TblCreateInd, ActiveInd, DeltaTablelayer, LayerSequence, IncludeRejected, Scenario_Identifier

### Example :

* DataProduct             : Batch Data Product
* DataProductSchema       : EDNABacth
* ObjectName              : plant_text

```jsonc
select * from EDNABatch.SchemaChangeCntrl where objectname='plant_text'
```

|BusinessName	|SourceName	|ObjectName	|TblSchemaName	|TblCreateInd	|ActiveInd	|DeltaTableLayer	|LayerSequence	|IncludeRejected	|Scenario_Identifier|
|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|
|Batch_DataProduct	|SAP	|plant_text	|batch_curated	|N	|Y	|Curated	|3	|Y	|NewTable|
|Batch_DataProduct	|SAP	|plant_text	|batch_raw	|N	|Y	|Raw	|1	|NA	|NewTable|
|Batch_DataProduct	|SAP	|plant_text	|batch_stage	|N	|Y	|Stage	|2	|Y	|NewTable|
|Batch_DataProduct	|SAP	|plant_text	|EDNABATCH	|N	|Y	|Synapse	|4	|NA	|NewTable|
