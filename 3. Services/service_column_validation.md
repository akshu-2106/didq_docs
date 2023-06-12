# Column Validation Service

This service will validate the column name along with number of columns present in source & target dataset and log the result in Audit log table which will state if the result is pass or fail along with process description.

## Key Features

* Responsible to perform a Data Ingestion and Quality check on top of the incoming data from variety of source systems.
* Validate the source column with control metadata column list.
* Validate the number of columns in sequence using Col Sequence Number column in control metadata table.

## Metadata Table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].ServiceCntrlMetadata
* Configuration Columns : SourceObjectName, SourceColumnName, ObjectName, ColumnName, ColSequenceNo

### Example

* DataProduct             : Batch Data Product
* DataProductSchema       : EDNABatch
* ObjectName              : plant_text

## Service Control Metadata Query

```jsonc
SELECT BusinessName, SourceObjectName, SourceColumnName, ObjectName, ColumnName, ColSequenceNo FROM EDNABatch.ServiceCntrlMetadata where ObjectName='plant_text'
```

|BusinessName	|SourceObjectName	|SourceColumnName	|ObjectName	|ColumnName	|ColSequenceNo	|
|:---	|:---	|:---	|:---	|:---	|:---	|
|Batch_DataProduct	|Plant_Text	|RECORDMODE	|plant_text	|recordmode	|1	|
|Batch_DataProduct	|Plant_Text	|PLANT	|plant_text	|plant	|2	|
|Batch_DataProduct	|Plant_Text	|TXTMD	|plant_text	|txtmd	|3	|

## Databricks Configurations

### Databricks Master Package : source2raw_master_package_RowNo

#### Column Validation Service Call

```jsonc
dbutils.notebook.run(s"$root_path/Services/dataIngestion_columnValidation_RowNo/", 0, Map("process_runlogId" -> s"$process_runlogId","business_name" -> s"$business_name", "object_name" -> s"$object_name", "control_table" -> s"$srvc_control_table", "adls_storage_account_name" -> s"$adls_storage_account_name", "adls_container_name" -> s"$adls_container_name", "landingrawpath" -> s"$landingrawpath", "file_format" -> s"$file_format", "rawtablename" -> s"$rawtablename", "filename" -> s"$filename","audit_log" -> s"$audit_log","delimiter" -> s"$delimiter","headerInd" -> s"$headerInd","schemaFileInd" -> s"$schemaFileInd","schema_filename" -> s"$schema_filename","source_name" -> s"$source_name","df_scope" -> s"$df_scope", "df_secret" -> s"$df_secret", "df_clintid" -> s"$df_clintid","df_tenantid" -> s"$df_tenantid", "df_raw" -> s"$df_raw", "df_jdbcUsername" -> s"$df_jdbcUsername","df_jdbcPassword" -> s"$df_jdbcPassword","df_jdbcHostname" -> s"$df_jdbcHostname","df_jdbcDatabase" -> s"$df_jdbcDatabase","pipeline_runid" -> s"$pipeline_runid"))
```

## Logs

### ProcessRunlog Query

```jsonc
select * from EDNABatch.ProcessRunlog where ObjectName='plant_text' and ServiceCategory='Data_Ingestion'
```

|ProcessRunlogId	|SourceLayer	|TargetLayer	|ServiceCategory	|BusinessName	|ObjectName	|FileName	|LoadFormat	|RawFileLoadedTimeStamp	|Status	|ProcessFlag	|Comment	|ProcessRunLoadTimestamp	|PipelineName	|PipelineRunId	|PipelineStartTime	|PipelineEndTime|
|:-----		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---	|
|7266F63D-EB53-483C-9571-5E3D7CE106F2	|Source	|Raw	|Data_Ingestion	|Batch_DataProduct	|plant_text	|Plant_Text_09-07-2022_12_36_53.csv	|Full_Load	|2022-09-07 12:39:34.980	|Success	|1	|Column Validation : Completed Successfully	|2022-09-07 12:48:35.307	|PL_BDD_CHILD_DI_DQ_DC_SRV_SRS_ROWNO_LEVEL2	|f8b51ebb-4f55-4e07-af6e-0d109b288fb5	|2022-09-07 12:42:11.593	|2022-09-07 12:48:35.307|

### AuditLog Query

```jsonc
select * from EDNABatch.AuditLog where ObjectName='plant_text' and ServiceCategory='Data_Ingestion'
```

|AuditLogId	|ProcessRunlogId	|BusinessName	|ObjectName	|StorageLayer	|ServiceCategory	|ServiceName	|FileName	|ServiceCategory_Cd	|Status	|Description	|SourceColCount	|ResultRowCount	|PipelineRunId	|LoadTimestamp	|Datepart|
|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---|
|101	|7266F63D-EB53-483C-9571-5E3D7CE106F2	|Batch_DataProduct	|plant_text	|Raw	|Data_Ingestion	|ColumnNameValidation 	|Plant_Text_09-07-2022_12_36_53.csv	|1	|Pass 	|Source File: Plant_Text_09-07-2022_12_36_53.csv and Target Object: plant_text Columns are RECORDMODE,PLANT,TXTMD	|3	|203	|f8b51ebb-4f55-4e07-af6e-0d109b288fb5	|2022-09-07 12:47:06.183	|2022-09-07|
|102	|7266F63D-EB53-483C-9571-5E3D7CE106F2	|Batch_DataProduct	|plant_text	|Raw	|Data_Ingestion	|NoOfColumnValidation 	|Plant_Text_09-07-2022_12_36_53.csv	|1	|Pass 	|#Column is same in Source File: Plant_Text_09-07-2022_12_36_53.csv and Target Object: plant_text	|3	|203	|f8b51ebb-4f55-4e07-af6e-0d109b288fb5	|2022-09-07 12:47:06.183	|2022-09-07|

## SAP ans Non-SAP sources

For SAP sources, notebook with 'RowNo' suffix has to be used, as these notebooks are designed to handle multiple transactions reflected in same source file. For reference, see [Column validation for SAP sources](https://github.com/elanco/DataOps_DIDQFramework/blob/master/ADB_Spark3.x/notebooks/EDNA%20-%20DataOps%20Framework%20(EDNA)/DIDQ_Spark3x/Services/dataIngestion_columnValidation_RowNo.scala)

For Non-SAP sources, notebook without 'RowNo' suffix has to be used. For reference, see [Column validation for Non-SAP sources](https://github.com/elanco/DataOps_DIDQFramework/blob/master/ADB_Spark3.x/notebooks/EDNA%20-%20DataOps%20Framework%20(EDNA)/DIDQ_Spark3x/Services/dataIngestion_columnValidation.scala)
