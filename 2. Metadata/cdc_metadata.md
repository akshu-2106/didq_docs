# Change Data Capture(CDC) Control Metadata

Change Data Capture(CDC) control metadata table is used to declare the properties of Databricks CDC service.
This table provides input to Databricks services through Azure Data Factory (ADF) pipelines.

## Significance of Columns

| Column Name           | Description                                                                                       |
| :---         | :---                                                                                     |
| BusinessName            | Defines Business Area                                                                                       |
| ObjectName      | Object Name or Table Name as per **DIDQ norms**                                                |
| CdcDate            | **Start date** in CDC logic      									|
| PartitionCol            | **Partition Column** for Rank Number Function 								|
| OrderCol            | Column based on which we will perform **Rank function**      									|
| OrderFlag            | Rank Order by column which can be set to **Asc** or **Desc** based on order arrangement.     									|
| OrderRank            | Decides the arrangement order of the Order By clause, value should be **1/2/3** based the corresponding order by column or columns, **1 been the highest**   									|
| SoftDeleteCol            | **Soft Delete** Column     									|
| LoadedTimeStamp            | Metadata Column to capture the record inserted Timestamp     									|

Read More About Change Data Capture(CDC): <https://mungingdata.com/delta-lake/type-2-scd-upserts/>

Read More About Rank Function:  <https://spark.apache.org/docs/latest/sql-ref-syntax-qry-select-window.html>

## Change Data Capture(CDC) Date can be derived in three ways:

| Values           | Description                                                                                       |
| :---         | :---                                                                                     |
| Filename | Value **filename** will extract the Start Date from Filename and provided to Databricks CDC service  |
| Metadata Column | Value **fileloaded_timestamp** will declared **fileloaded_timestamp** metadata column as Start Date from Stage table and provided to Databricks CDC service  |
| Table Column |  Any respetive column from Stage table can be declared as **Start Date** and provided to **Databricks CDC service**  |

## Metadata table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].CdcCntlMetadata

### Example

* DataProduct	: Batch Data Product
* DataProductSchema	: EDNABatch
* Metadata Table		: CdcCntlMetadata
* ObjectName        : plant_text

### Source Control Metadata Query

```jsonc
SELECT * FROM EDNABatch.CdcCntlMetadata where ObjectName='plant_text' 
```

|BusinessName	|ObjectName	|CdcDate	|PartitionCol	|OrderCol	|OrderFlag	|OrderRank	|SoftDeleteCol	|LoadedTimeStamp	|
|:---  	|:---  	|:---  	|:---  	|:---  	|:---  	|:---  	|:---  	|:---  	|
|Batch_DataProduct	|plant_text	|filename	|plant	|plant	|Desc	|1	|NULL	|2021-08-17 14:05:43.8933333	|
