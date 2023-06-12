# Scenario 2 - New/Rename/Delete Column

The New Column scenario will take a backup of existing tables, recreate the table with the column list from service/curated control tables, and load the existing data into the recreated table leaving the newly created column.
Rename Column scenario will take a backup of existing tables, recreate the table with the column list from service/curated control tables, and load the existing data into the recreated table.
Delete Column scenario will take a backup of existing tables, recreate the table with the column list from service/curated control tables, and load the existing data into the recreated table without the deleted column.

## Key Features

* Creates delta table with required scenarios for Raw, Stage, and Curated layers with help of SchemaChangeCntrl metadata table column Scenario_identifier.
* For Synapse auto creates a script in the corresponding data product container under the innovation folder.
* Reduces the manual effort by automation.

## Metadata Table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].SchemaChangeCntrl
* Configuration Columns : SourceName,ObjectName, TblschemaName, TblCreateInd, ActiveInd, DeltaTablelayer, LayerSequence, IncludeRejected, Scenario_Identifier

## Scenario_Identifier

|Value	|Description|
|:---	|:---	|
|NewColumn	|Recreates the table with the new column listed in the control table|
|RenameColumn	|Recreates the table by renaming the specific column by referring to the control table|
|DeleteColumn	|Recreates the table by removing the column and by referring to the control table|

### Example :

* DataProduct             : Batch Data Product
* DataProductSchema       : EDNABatch
* ObjectName              : plant_text
* Scenario_Identifier     : RenameColumn

```jsonc
select * from EDNABatch.SchemaChangeCntrl where objectname='plant_text' where Scenario_Identifier='RenameColumn'
```

|BusinessName	|SourceName	|ObjectName	|TblSchemaName	|TblCreateInd	|ActiveInd	|DeltaTableLayer	|LayerSequence	|IncludeRejected	|Scenario_Identifier|
|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|
|Batch_DataProduct	|SAP	|plant_text	|batch_curated	|N	|Y	|Curated	|3	|Y	|RenameColumn|
|Batch_DataProduct	|SAP	|plant_text	|batch_raw	|N	|Y	|Raw	|1	|NA	|RenameColumn|
|Batch_DataProduct	|SAP	|plant_text	|batch_stage	|N	|Y	|Stage	|2	|Y	|RenameColumn|
|Batch_DataProduct	|SAP	|plant_text	|EDNABATCH	|N	|Y	|Synapse	|4	|NA	|RenameColumn|

We need to trigger the pipeline PL_EDCD_MASTER_DYNAMIC_SCHEMA.

Service **dynamicTables_Schema_Recreate** will be triggered.

Now Dynamic Schema will check for the TblCreateInd =N and ActiveInd=Y and then it Recreates the table for the respective layer and loads the exisitng data.
Then SchemaChangeCntrl table will be updated with the TblcreateInd to **Y**

|BusinessName	|SourceName	|ObjectName	|TblSchemaName	|TblCreateInd	|ActiveInd	|DeltaTableLayer	|LayerSequence	|IncludeRejected	|Scenario_Identifier|
|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|
|Batch_DataProduct	|SAP	|plant_text	|batch_curated	|Y	|Y	|Curated	|3	|Y	|RenameColumn|
|Batch_DataProduct	|SAP	|plant_text	|batch_raw	|Y	|Y	|Raw	|1	|NA	|RenameColumn|
|Batch_DataProduct	|SAP	|plant_text	|batch_stage	|Y	|Y	|Stage	|2	|Y	|RenameColumn|
|Batch_DataProduct	|SAP	|plant_text	|EDNABATCH	|Y	|Y	|Synapse	|4	|NA	|RenameColumn|
