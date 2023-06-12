# Trim Service

Trim service will omit the leading and trailing spaces in the stated column or columns in a table.

## Key Features

* Responsible to perform a Data Cleansing on top of the incoming data from variety of source systems.
* Trim all string columns or columns.

## Metadata Table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].ServiceCntrlMetadata
* Configuration Columns : ObjectName, ColumnName, Trim

### Example

* DataProduct             : Batch Data Product
* DataProductSchema       : EDNABatch
* ObjectName              : plant_text

## Service Control Metadata Query

```jsonc
SELECT BusinessName, ObjectName, ColumnName, Trim FROM EDNABatch.ServiceCntrlMetadata where ObjectName='plant_text'
```

|BusinessName	|ObjectName	|ColumnName	|Trim	|
|:---	|:---	|:---	|:---	|
|Batch_DataProduct	|plant_text	|recordmode	|Y	|
|Batch_DataProduct	|plant_text	|plant	|Y	|
|Batch_DataProduct	|plant_text	|txtmd	|Y	|

## Databricks Configurations

### Databricks Master Package : raw2stage_master_package_RowNo

#### Data Cleaning Trim Service Call

```jsonc
dbutils.notebook.run(s"$root_path/Services/dataCleansing_trimService_RowNo/", 0, Map("process_runlogId" -> s"$process_runlogId","business_name" -> s"$business_name", "object_name" -> s"$object_name", "control_table" -> s"$srvc_control_table", "adls_storage_account_name" -> s"$adls_storage_account_name", "adls_container_name" -> s"$adls_container_name", "rawtablename" -> s"$rawtablename", "stagetablename" -> s"$stagetablename", "rejectedtablename" -> s"$rejectedtablename", "audit_log" -> s"$audit_log", "src_control_table" -> s"$src_control_table","srvc_control_table" -> s"$srvc_control_table","process_runlog" -> s"$process_runlog","raw_filter" -> s"$loaded_timeStamp","raw_filter_filename" -> s"$filename","df_scope" -> s"$df_scope", "df_secret" -> s"$df_secret", "df_clintid" -> s"$df_clintid","df_tenantid" -> s"$df_tenantid", "df_raw" -> s"$df_raw", "df_jdbcUsername" -> s"$df_jdbcUsername","df_jdbcPassword" -> s"$df_jdbcPassword","df_jdbcHostname" -> s"$df_jdbcHostname","df_jdbcDatabase" -> s"$df_jdbcDatabase","scratchpad_target_path" -> s"$scratchpad_dctm_obj_path","pipeline_runid" -> s"$pipeline_runid"))
```

## Logs

### ProcessRunlog Query

```jsonc
select * from EDNABatch.ProcessRunlog where ObjectName='plant_text' and ServiceCategory='Data_Cleansing'
```

|ProcessRunlogId	|SourceLayer	|TargetLayer	|ServiceCategory	|BusinessName	|ObjectName	|FileName	|LoadFormat	|RawFileLoadedTimeStamp	|Status	|ProcessFlag	|Comment	|ProcessRunLoadTimestamp	|PipelineName	|PipelineRunId	|PipelineStartTime	|PipelineEndTime|
|:-----		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---	|
|7266F63D-EB53-483C-9571-5E3D7CE106F2	|Raw	|Stage	|Data_Cleansing	|Batch_DataProduct	|plant_text	|Plant_Text_09-07-2022_12_36_53.csv	|Full_Load	|2022-09-07 12:39:34.980	|Success	|1	|Data Cleansing : Completed Successfully	|2022-09-07 12:48:35.307	|PL_BDD_CHILD_DI_DQ_DC_SRV_SRS_ROWNO_LEVEL2	|f8b51ebb-4f55-4e07-af6e-0d109b288fb5	|2022-09-07 12:42:11.593	|2022-09-07 12:48:35.307|

### AuditLog Query

```jsonc
select * from EDNABatch.AuditLog where ObjectName='plant_text' and ServiceCategory='Data_Cleansing' and ServiceName='Data_Cleansing_Trim'
```

|AuditLogId	|ProcessRunlogId	|BusinessName	|ObjectName	|StorageLayer	|ServiceCategory	|ServiceName	|FileName	|ServiceCategory_Cd	|Status	|Description	|SourceColCount	|ResultRowCount	|PipelineRunId	|LoadTimestamp	|Datepart|
|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---|
|103	|7266F63D-EB53-483C-9571-5E3D7CE106F2	|Batch_DataProduct	|plant_text	|Stage	|Data_Cleansing	|Data_Cleansing_Trim 	|Plant_Text_09-07-2022_12_36_53.csv	|2	|Pass 	|Pass in Data Cleansing Trim for plant_text 	|3	|203	|f8b51ebb-4f55-4e07-af6e-0d109b288fb5	|2022-09-07 12:47:06.183	|2022-09-07 |

## SAP ans Non-SAP sources

For SAP sources, notebook with 'RowNo' suffix has to be used, as these notebooks are designed to handle multiple transactions reflected in same source file. For reference, see [Trim validation for SAP sources](https://github.com/elanco/DataOps_DIDQFramework/blob/master/ADB_Spark3.x/notebooks/EDNA%20-%20DataOps%20Framework%20(EDNA)/DIDQ_Spark3x/Services/dataCleansing_trimService_RowNo.scala)

For Non-SAP sources, notebook without 'RowNo' suffix has to be used. For reference, see [Trim validation for Non-SAP sources](https://github.com/elanco/DataOps_DIDQFramework/blob/master/ADB_Spark3.x/notebooks/EDNA%20-%20DataOps%20Framework%20(EDNA)/DIDQ_Spark3x/Services/dataCleansing_trimService.scala)
