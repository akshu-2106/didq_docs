
# Scenario 1 - New Table

This Scenario will create Raw, Stage and Stage_rejected delta tables and place the synapse create table scripts under the innovation folder of the data product container

## Key Features

* Creates a new delta table for Raw, Stage, and Curated layers with help of SchemaChangeCntrl metadata table.
* For Synapse it auto creates a script in the corresponding data product container under the innovation folder.
* Reduces the manual effort by automation.

## Metadata Table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].SchemaChangeCntrl
* Configuration Columns : SourceName,ObjectName, TblschemaName, TblCreateInd, ActiveInd, DeltaTablelayer, LayerSequence, IncludeRejected, Scenario_Identifier

## Scenario_Identifier

|Value	|Description|
|:---	|:---	|
|NewTable	|Creates the table by referring to the control table|

### Example :

* DataProduct             : Batch Data Product
* DataProductSchema       : EDNABacth
* ObjectName              : plant_text

```md
select * from EDNABatch.SchemaChangeCntrl where objectname='plant_text'
```

|BusinessName	|SourceName	|ObjectName	|TblSchemaName	|TblCreateInd	|ActiveInd	|DeltaTableLayer	|LayerSequence	|IncludeRejected	|Scenario_Identifier|
|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|
|Batch_DataProduct	|SAP	|plant_text	|batch_curated	|N	|Y	|Curated	|3	|Y	|NewTable|
|Batch_DataProduct	|SAP	|plant_text	|batch_raw	|N	|Y	|Raw	|1	|NA	|NewTable|
|Batch_DataProduct	|SAP	|plant_text	|batch_stage	|N	|Y	|Stage	|2	|Y	|NewTable|
|Batch_DataProduct	|SAP	|plant_text	|EDNABATCH	|N	|Y	|Synapse	|4	|NA	|NewTable|

We need to trigger the pipeline PL_BTDD_MASTER_DYNAMIC_SCHEMA.

Service **dynamicTables_SchemaService** will be triggered.

Now Dynamic Schema will check for the TblCreateInd =N and ActiveInd=Y and then it creates the table for the respective layer.
Then SchemaChangeCntrl table will be updated with the TblcreateInd to **Y**

|BusinessName	|SourceName	|ObjectName	|TblSchemaName	|TblCreateInd	|ActiveInd	|DeltaTableLayer	|LayerSequence	|IncludeRejected	|Scenario_Identifier|
|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|
|Batch_DataProduct	|SAP	|plant_text	|batch_curated	|Y	|Y	|Curated	|3	|Y	|NewTable|
|Batch_DataProduct	|SAP	|plant_text	|batch_raw	|Y	|Y	|Raw	|1	|NA	|NewTable|
|Batch_DataProduct	|SAP	|plant_text	|batch_stage	|Y	|Y	|Stage	|2	|Y	|NewTable|
|Batch_DataProduct	|SAP	|plant_text	|EDNABATCH	|Y	|Y	|Synapse	|4	|NA	|NewTable|
