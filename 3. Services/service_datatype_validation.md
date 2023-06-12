# Datatype Service

Datatype service will check the Data type if a categorization of data belong to the respective datatype category.
A data type is an attribute associated with a piece of data that tells a computer system how to interpret its value.
Understanding data types ensures that data is collected in the preferred format and the value of each property is as expected.

This service can be done in two ways

* [Row wise quality validation](https://github.com/elanco/DataOps_DIDQFramework/blob/master/ADB_Spark3.x/notebooks/EDNA%20-%20DataOps%20Framework%20(EDNA)/DIDQ_Spark3x/Services/dataQuality_datatypeCheck.scala)
* [Column wise quality validation](https://github.com/elanco/DataOps_DIDQFramework/blob/master/ADB_Spark3.x/notebooks/EDNA%20-%20DataOps%20Framework%20(EDNA)/DIDQ_Spark3x/Services/DataQuality_DataType_Column_wise.scala)

## Key Features

* Responsible to perform a Data Quality on top of the incoming data from variety of source systems.
* This is a way to detect and reject the incompatible data to be send to Stage Delta tables.
* The data type will also determine what logical, mathematical or relational operations and actions can be performed on it.

## Metadata Table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].ServiceCntrlMetadata
* Configuration Columns : ObjectName, ColumnName, DQDataTypeCategory,	DQColLength,	DQPrecisionLength,	DQScaleLength,	DQNotNullCheckFlag,	DQDateFormat, DQPatternMatch

## Data Type Classification

* **DQDataTypeCategory** are grouped into the following classes
  * **integral** value for numeric types which represent whole numbers
    * TINYINT
    * SMALLINT
    * INT
    * BIGINT

  * **fractional** value for numeric types which represent floating point types use exponents and a binary representation to cover a large range of numbers
    * FLOAT
    * DOUBLE
    * DECIMAL(p,s)

  * **date** value to represent date components
    * DATE
  
  * **timestamp** value to represent date and time components
    * TIMESTAMP

  * **string** value to represent string components
    * STRING

  * **boolean** value to represent boolean components
    * BOOLEAN

* **DQColLength** - Defines the maximum length/upper boundaies based on SQL/HQL.

* **DQPrecisionLength** -  Defines the precision (p) length for Decimal datatype.

* **DQScaleLength** -   Defines the scale (s) length for Decimal datatype.

* **DQ_NotNullCheck** - Defines the rule where value should be **R** or **P** corresponding to any column if user wants to enable Not Null Check for that column.
  * **P**: Permissive Flag, even if Row fails the condition, it will not go to Error Table.
  * **R**: Restrictive Flag, Row which fails the condition will go to Error Table.

* **DQ_DateFormatCheck** - Defines the rule to valid date time format, should be ‘Accepted Date Format’ corresponding to any date column if user wants to enable Date Format check for that column.

* **DQPatternMatch** -   Defines the rule to specify the Pattern Match, similar to Regex function.

### Example

* DataProduct             : Batch Data Product
* DataProductSchema       : EDNABatch
* ObjectName              : plant_text

## Service Control Metadata Query

```jsonc
SELECT BusinessName, ObjectName, ColumnName, DQDataTypeCategory, DQColLength, DQPrecisionLength, DQScaleLength, DQNotNullCheckFlag, DQDateFormat, DQPatternMatch FROM EDNABatch.ServiceCntrlMetadata where ObjectName='plant_text'
```

|BusinessName	|ObjectName	|ColumnName	|DQDataTypeCategory	|DQColLength	|DQPrecisionLength	|DQScaleLength	|DQNotNullCheckFlag	|DQDateFormat	|DQPatternMatch	|
|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|
|Batch_DataProduct	|plant_text	|recordmode	|string	|1	|NULL	|NULL	|P	|NULL	|NULL	|
|Batch_DataProduct	|plant_text	|plant	|string	|4	|NULL	|NULL	|R	|NULL	|NULL	|
|Batch_DataProduct	|plant_text	|txtmd	|string	|40	|NULL	|NULL	|P	|NULL	|NULL	|

## Databricks Configurations

### Databricks Master Package : raw2stage_master_package_RowNo

#### Data Quality Datatype Service Call

```jsonc
dbutils.notebook.run(s"$root_path/Services/dataQuality_datatypeCheck_RowNo/", 0, Map("process_runlogId" -> s"$process_runlogId","business_name" -> s"$business_name", "object_name" -> s"$object_name", "control_table" -> s"$srvc_control_table", "adls_storage_account_name" -> s"$adls_storage_account_name", "adls_container_name" -> s"$adls_container_name", "rawtablename" -> s"$rawtablename", "stagetablename" -> s"$stagetablename", "rejectedtablename" -> s"$rejectedtablename", "audit_log" -> s"$audit_log", "src_control_table" -> s"$src_control_table","srvc_control_table" -> s"$srvc_control_table","process_runlog" -> s"$process_runlog","raw_filter" -> s"$loaded_timeStamp","raw_filter_filename" -> s"$filename","df_scope" -> s"$df_scope", "df_secret" -> s"$df_secret", "df_clintid" -> s"$df_clintid","df_tenantid" -> s"$df_tenantid", "df_raw" -> s"$df_raw", "df_jdbcUsername" -> s"$df_jdbcUsername","df_jdbcPassword" -> s"$df_jdbcPassword","df_jdbcHostname" -> s"$df_jdbcHostname","df_jdbcDatabase" -> s"$df_jdbcDatabase","scratchpad_source_path" -> s"$scratchpad_dccm_obj_path","scratchpad_target_path" -> s"$scratchpad_dqdt_obj_path","rej_scratchpad_target_path" -> s"$rej_scratchpad_dqdt_obj_path","pipeline_runid" -> s"$pipeline_runid","df_srvc_constant" -> s"$df_srvc_constant"))
```

## Logs

### ProcessRunlog Query

```jsonc
select * from EDNABatch.ProcessRunlog where ObjectName='plant_text' and ServiceCategory='Data_Quality'
```

|ProcessRunlogId	|SourceLayer	|TargetLayer	|ServiceCategory	|BusinessName	|ObjectName	|FileName	|LoadFormat	|RawFileLoadedTimeStamp	|Status	|ProcessFlag	|Comment	|ProcessRunLoadTimestamp	|PipelineName	|PipelineRunId	|PipelineStartTime	|PipelineEndTime|
|:-----		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---	|
|7266F63D-EB53-483C-9571-5E3D7CE106F2	|Raw	|Stage	|Data_Quality	|Batch_DataProduct	|plant_text	|Plant_Text_09-07-2022_12_36_53.csv	|Full_Load	|2022-09-07 12:39:34.980	|Success	|1	|Data Quality : Completed Successfully	|2022-09-07 12:48:35.307	|PL_BDD_CHILD_DI_DQ_DC_SRV_SRS_ROWNO_LEVEL2	|f8b51ebb-4f55-4e07-af6e-0d109b288fb5	|2022-09-07 12:42:11.593	|2022-09-07 12:48:35.307|

### AuditLog Query

```jsonc
select * from EDNABatch.AuditLog where ObjectName='plant_text' and ServiceCategory='Data_Quality' and ServiceName='Data_Quality_Datatype'
```

|AuditLogId	|ProcessRunlogId	|BusinessName	|ObjectName	|StorageLayer	|ServiceCategory	|ServiceName	|FileName	|ServiceCategory_Cd	|Status	|Description	|SourceColCount	|ResultRowCount	|PipelineRunId	|LoadTimestamp	|Datepart|
|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---	|:---|
|104	|7266F63D-EB53-483C-9571-5E3D7CE106F2	|Batch_DataProduct	|plant_text	|Stage	|Data_Quality	|Data_Quality_Datatype 	|Plant_Text_09-07-2022_12_36_53.csv	|3	|Pass 	|Pass in Data Quality Datatype for plant_text 	|3	|203	|f8b51ebb-4f55-4e07-af6e-0d109b288fb5	|2022-09-07 12:47:06.183	|2022-09-07 |

## SAP ans Non-SAP sources

For SAP sources, notebook with 'RowNo' suffix has to be used, as these notebooks are designed to handle multiple transactions reflected in same source file. For reference, see [Datatype validation for SAP sources](https://github.com/elanco/DataOps_DIDQFramework/blob/master/ADB_Spark3.x/notebooks/EDNA%20-%20DataOps%20Framework%20(EDNA)/DIDQ_Spark3x/Services/dataQuality_datatypeCheck_RowNo.scala)

For Non-SAP sources, notebook without 'RowNo' suffix has to be used. For reference, see [Datatype validation for Non-SAP sources](https://github.com/elanco/DataOps_DIDQFramework/blob/master/ADB_Spark3.x/notebooks/EDNA%20-%20DataOps%20Framework%20(EDNA)/DIDQ_Spark3x/Services/dataQuality_datatypeCheck.scala)

Note: Column wise quality validation is the recommended type of validation from May 2023.
