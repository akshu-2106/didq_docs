# Configuration Email Recipients

Email Recipient metadata table to declare the recipient mail id in case of any Azure Data Factory(ADF) failure. We have one generic Logic App defined in the
Development and Quality DataOps environment to send the mail in case of ADF pipelines or activity failures.
This table provides input to Azure Data Factory(ADF) pipelines.

## Significance of Columns

| Column Name           | Description                                                                                       |
| :---         | :---                                                                                     |
| RecipientId          | Defines Recipient Id                                                                              |
| Batch_DataProduct            | Defines Business Name                                                                                       |
| ToEmailAddress      | Receipt Mail id or id's seperated with comma \(\,\)                                                      |
| Enabled            | Value **1** to enable and **0** to Disable                                                        |

## Metadata table Configurations

* Database              : ControlOps
* Configuration Table   : [DataProductSchema].ConfEmailRecipients

### Example

* DataProduct	: Batch Data Product
* DataProductSchema	: EDNABatch
* Metadata Table		: ConfEmailRecipients

### Source Control Metadata Query

```jsonc
SELECT * FROM EDNABatch.ConfEmailRecipients
```

|RecipientId	|BusinessName	|ToEmailAddress	|Enabled |
|:---	|:---	|:---	|:---
|1	|Batch_DataProduct	|sneh_kumar.gaur@elancoah.com,MOHAMMAD.SHAHBAZ@elancoah.com,DASARI_RAVINDRANATH.REDDY@elancoah.com,mahima.sharma@elancoah.com,rajavigneswarran.jayaram@elancoah.com,jayamadhuri.neelam@network.elancoah.com,yashwanth.raj_n@network.elancoah.com	|1	|
