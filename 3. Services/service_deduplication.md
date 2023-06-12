# Deduplication Service

Data deduplication service will remove the duplicate from a table.

## Key Features

* Responsible to perform a Data Cleansing on top of the incoming data from variety of source systems.
* This is a way to detect and remove the duplicates from the table.
* Process that eliminates excessive copies of data and significantly decreases storage capacity requirements.

## Metadata Table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].ServiceCntrlMetadata
* Configuration Columns : ObjectName, ColumnName, DeDupCol, DeDupOrderFlag, DeDupOrderRank

Metadata Table has below three columns for Deduplication

1. **DeDupCol** - Value should be marked **Y** corresponding to the columns based on which deduplication is required.
2. **DeDupOrderFlag** (Asc/Desc) - Deduplication Order by column which can be set to **Asc** or **Desc** based on order arrangement.
3. **DeDupOrderRank** (1/2/3) - 	Decides the arrangement order of the Order By clause, value should be **1/2/3** based the corresponding order by column or columns, **1 been the highest**.\
\
*DeDupOrderRank need to be updated for the Columns (Id, Sal) for the same Object (EmpDetail) present in ObjectName column. This decides the order of the Order By operation. For Example: Order By operation will follow the order mentioned in DeDupOrderRank (Id 1, Sal 2).*

### Example

* DataProduct             : Batch Data Product
* DataProductSchema       : EDNABatch
* ObjectName              : plant_text

## Service Control Metadata Query

```jsonc
SELECT BusinessName, ObjectName, ColumnName, DeDupCol, DeDupOrderFlag, DeDupOrderRank FROM EDNABatch.ServiceCntrlMetadata where ObjectName='plant_text'
```

|BusinessName	|ObjectName	|ColumnName	|DeDupCol	|DeDupOrderFlag |DeDupOrderRank |
|:---	|:---	|:---	|:---	|:---	|:---	|
|Batch_DataProduct	|plant_text	|recordmode	|NULL	|NULL	|NULL	|
|Batch_DataProduct	|plant_text	|plant	|Y	|Desc	|1	|
|Batch_DataProduct	|plant_text	|txtmd	|NULL	|NULL	|NULL	|

## Databricks Configurations

### Databricks Master Package : raw2stage_master_package_RowNo

#### Data Cleansing DeDup Service Call

```jsonc
 dbutils.notebook.run(s"$root_path/Services/dataCleansing_dedupService_RowNo/", 0, Map("process_runlogId" -> s"$process_runlogId","business_name" -> s"$business_name", "object_name" -> s"$object_name", "control_table" -> s"$srvc_control_table", "adls_storage_account_name" -> s"$adls_storage_account_name", "adls_container_name" -> s"$adls_container_name", "rawtablename" -> s"$rawtablename", "stagetablename" -> s"$stagetablename", "rejectedtablename" -> s"$rejectedtablename", "audit_log" -> s"$audit_log", "src_control_table" -> s"$src_control_table","srvc_control_table" -> s"$srvc_control_table","process_runlog" -> s"$process_runlog","raw_filter" -> s"$loaded_timeStamp","raw_filter_filename" -> s"$filename","df_scope" -> s"$df_scope", "df_secret" -> s"$df_secret", "df_clintid" -> s"$df_clintid","df_tenantid" -> s"$df_tenantid", "df_raw" -> s"$df_raw", "df_jdbcUsername" -> s"$df_jdbcUsername","df_jdbcPassword" -> s"$df_jdbcPassword","df_jdbcHostname" -> s"$df_jdbcHostname","df_jdbcDatabase" -> s"$df_jdbcDatabase","scratchpad_source_path" -> s"$scratchpad_dcnn_obj_path","scratchpad_target_path" -> s"$scratchpad_dcdd_obj_path","rej_scratchpad_target_path" -> s"$rej_scratchpad_dcdd_obj_path","pipeline_runid" -> s"$pipeline_runid"))
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
select * from EDNABatch.AuditLog where ObjectName='plant_text' and ServiceCategory='Data_Cleansing' and ServiceName='Data_Cleansing_Dedup'
```

|AuditLogId	|ProcessRunlogId	|BusinessName	|ObjectName	|StorageLayer	|ServiceCategory	|ServiceName	|FileName	|ServiceCategory_Cd	|Status	|Description	|SourceColCount	|ResultRowCount	|PipelineRunId	|LoadTimestamp	|Datepart|
|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---|
|107	|7266F63D-EB53-483C-9571-5E3D7CE106F2	|Batch_DataProduct	|plant_text	|Stage	|Data_Cleansing	|Data_Cleansing_Dedup 	|Plant_Text_09-07-2022_12_36_53.csv	|6	|Pass 	|Pass in Data Cleansing Dedup for plant_text 	|3	|203	|f8b51ebb-4f55-4e07-af6e-0d109b288fb5	|2022-09-07 12:47:06.183	|2022-09-07 |

## SAP ans Non-SAP sources

For SAP sources, notebook with 'RowNo' suffix has to be used, as these notebooks are designed to handle multiple transactions reflected in same source file. For reference, see [Column validation for SAP sources](https://github.com/elanco/DataOps_DIDQFramework/blob/master/ADB_Spark3.x/notebooks/EDNA%20-%20DataOps%20Framework%20(EDNA)/DIDQ_Spark3x/Services/dataCleansing_dedupService_RowNo.scala)

For Non-SAP sources, notebook without 'RowNo' suffix has to be used. For reference, see [Column validation for Non-SAP sources](https://github.com/elanco/DataOps_DIDQFramework/blob/master/ADB_Spark3.x/notebooks/EDNA%20-%20DataOps%20Framework%20(EDNA)/DIDQ_Spark3x/Services/dataCleansing_dedupService.scala)
