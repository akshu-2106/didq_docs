# Service Control Metadata

Service Control Metadata is another baseline table to define the Business Rules of Source Object Name / Table Name at Column Level.
This table provides input to Azure Data Factory(ADF) Pipelines & Databricks Service Notebook to apply the given rules at each Object Name Level.

## Significance of Columns

| Column Name           	| 	Description	|
| :---        						| 	:--- 	|
| BusinessName          	| 	Defines Business Area	|
| SourceObjectName      | 	Object Name or Table Name coming from source	|
|SourceColumnName     	| 	Object Column Name or Table Column Name coming from source	|
|ObjectName                 | 	Object Name or Table Name as per **DIDQ norms**	|
|ColumnName               	| 	Object Column Name or Table Column Name as per **DIDQ norms**	|
|DeDupCol                    	|	Value should be mark as **Y** corresponding to the columns based on which deduplication is required	else **NULL** |
|DeDupOrderFlag          	|	Deduplication Order by column which can be set to **Asc** or **Desc** based on order arrangement else **NULL**  |
|DeDupOrderRank         	|	This decides the arrangement order of the Order By clause else **NULL**	|
|DataType                     |	Datatype of **Stage Delta** Table	|
|Trim                           	|	**Y** value indicates Trim Function should be applied on the specified column else **NULL**	|
|NotNullCheck              	|	**Y** value indicates Not Null Check should be applied on the specified column else **NULL**		|
|RemoveCommaInd      	|	**Y** value indicates Remove Comma Ind Function should be applied on the specified column else **NULL**	|
|DQPrimaryKey            	|	**Y** value indicates Primary Key Function should be applied on the specified column else **NULL**	|
|DQDataTypeCategory   	|	Service will pick the Data Type defined as **Integral** (Integer, Big Integer, Long), **Fractional**(Decimal, Double), **Timestamp**, **Date**, **Boolean**	else NULL|
|DQColLength                |	For **String** and **Integral** Datatype define the Maximum length/upper bound for respective column	else **NULL** |
|DQPrecisionLength      	|	For **Decimal** Datatype, you can define precision length else **NULL** |
|DQScaleLength           	|	For **Decimal** Datatype, you can define scale length else **NULL** 	|
|DQNotNullCheckFlag   	|	Value should be **R**(Restrictive Flag) or **P**(Permissive Flag) corresponding to any column if user wants to enable **Not Null** Check for the respective column|
|DQDateFormat           	|	Valid **Date** or **Timestamp** format, should be ‘Accepted Date Format’ corresponding to any date/timestamp column if user wants to enable **Date Format** check for respective column	else NULL|
|DQPatternMatch         	|	Specify the **Pattern Match**, similar to **Regex Function** like Columns Phone Number starting with [+91] can be defined in this column	|
|CDCKey                     	|	**Y** value indicates Key Column on which Change Data Capture/SCD Type 2 will perform the operation else **Null**	|
|ColSequenceNo          	|	Sequence Number of the column starting from **1 to N** value	|
|LoadedTimeStamp      	|	Metadata Column to capture the record inserted Timestamp  	|

More details of each columns usage is explained in the respective services

## Metadata table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].ServiceCntrlMetadata

### Example

* DataProduct             : Batch Data Product
* DataProductSchema       : EDNABatch
* Metadata Table : ServiceCntrlMetadata
* ObjectName              : plant_text

### Service Control Metadata Query

```jsonc
SELECT * FROM EDNABatch.ServiceCntrlMetadata where ObjectName='plant_text'
```

|BusinessName	|SourceObjectName	|SourceColumnName	|ObjectName	|ColumnName	|DeDupCol	|DeDupOrderFlag	|DeDupOrderRank	|DataType	|Trim	|NotNullCheck	|RemoveCommaInd	|DQPrimaryKey	|DQDataTypeCategory	|DQColLength	|DQPrecisionLength	|DQScaleLength	|DQNotNullCheckFlag	|DQDateFormat	|DQPatternMatch	|CDCKey	|ColSequenceNo	|LoadedTimeStamp|
|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---		|:---	|
|Batch_DataProduct	|Plant_Text	|RECORDMODE	|plant_text	|recordmode	|NULL	|NULL	|NULL	|string	|Y	|NULL	|NULL	|NULL	|string	|1	|NULL	|NULL	|P	|NULL	|NULL	|NULL	|1	|2020-12-16 17:45:07.1466667|
