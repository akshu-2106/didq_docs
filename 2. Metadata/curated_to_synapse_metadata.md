# Curated To Synapse Metadata

Curated to Synapse Metadata is another baseline table to define the Business Rules of Curated Object Name and Synapse Table Name at Column Level.
This table provides input to Azure Data Factory(ADF) Pipelines, Databricks Service Notebook for Curated Layer and Stored Procedure in Synapse to apply the given rules at each Object Name Level.

## Significance of Columns

| Column Name           	| 	Description	|
| :---        						| 	:--- 	|
|CuratedObject          	| 	Object Name or Table Name of **Curated Layer** and **Synapse Table**	|
|PrimaryKey      			| 	**Y** value defines the Primary Key in **Synapse Table** else **NULL**	|
|ForeignKey     				| 	**Y** value defines the Foreign Key in **Synapse Table** else **NULL**	|
|DataType		                | 	Datatype of **Synapse Table**		|
|NullFlag		               	| 	**Y** value defines the Not Nullable column in **Synapse Table** else **NULL**	|
|Length	                    	|	Datatype Length of **Synapse Table**	|
|Precision          			|	Precision value only for Decimal Datatype on the specified column of **Synapse Table**	|
|Scale         					|	Scale value only for Decimal Datatype on the specified column of **Synapse Table**	|
|DefaultValue                	|	Any Default Value on the specified column of **Synapse Table**	|
|SynapseSchema          	|	Schema Name of **Synapse Table**	|
|DataTypeExternalTables	|	Datatype of **Curated Delta Table**		|
|LoadType      	|	Define Load Type either its Insert **I**, Upsert **U**, FullLoad **F**,Delete **D**	|
|FilterCol            	|	Based on which column the **Incremental** process will run between Curated to Synpase in case of LoadType in **I**, **U**, **D** (Set value as **1**)	else **0** |
|BusinessName   	|	Defines your Business Area	|
|ColSequenceNo                |	Sequence Number of the column starting from **1 to N** value	|

## Metadata table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].CuratedToSynapseSchema

### Example

* DataProduct             : Batch Data Product
* DataProductSchema       : EDNABatch
* Metadata Table : CuratedToSynapseSchema
* ObjectName              : plant_text

### Service Control Metadata Query

```jsonc
SELECT * FROM EDNABatch.CuratedToSynapseSchema where CuratedObject='plant_text'
```

|CuratedObject	|ColumnName	|PrimaryKey	|ForeignKey	|DataType	|NullFlag	|Length	|Precision	|Scale	|DefaultValue	|SynapseSchema	|DataTypeExternalTables	|LoadType	|FilterCol	|BusinessName	|ColSequenceNo|
|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---|
|plant_text	|recordmode	|NULL	|NULL	|char	|NULL	|1	|NULL	|NULL	|NULL	|EDNABatch	|string	|U	|0	|Batch_DataProduct	|1	|
|plant_text	|plant	|NULL	|NULL	|char	|NULL	|4	|NULL	|NULL	|NULL	|EDNABatch	|string	|U	|1	|Batch_DataProduct	|2	|
|plant_text	|txtmd	|NULL	|NULL	|nvarchar	|NULL	|40	|NULL	|NULL	|NULL	|EDNABatch	|string	|U	|0	|Batch_DataProduct	|3	|
