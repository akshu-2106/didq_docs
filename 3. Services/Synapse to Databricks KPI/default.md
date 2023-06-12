# Synapse to Databricks KPI

The intention of Synapse to Databricks KPI is to reduce the time taken and cost incurred while loading Synapse tables.
Currently, we have stored procedures defined in Synapse layer which are responsible for performing transformations and analytical operations by taking data from one/more Synapse tables and finally loading into a target syanpse table. As we have millions of records in Synapse each operation becomes time taking and costly.

To overcome this issue, we have come up with an approach where the transformation and analytics part can be shifted to Databricks which wpuld save time. Final result set can then be loaded to Synapse table directly from the databricks delta table(s). Below steps can be followed:

-	Setting Synapse Configuration

![Synapse_Configuration](./images/Syanpse_Config.png)

-	Reading Synapse table - It will take very minimal time to read data from Syanpse irrespective of the amount of data.

![Read_from_Synapse_table](./images/Read_from_synapse.png)

-	Perform analytics operations - Rewrite the transformation/analytics logic in databricks and write final result in one dataset.

![Analytics_Databricks](./images/Databricks_analytics.png)

-	Write it as delta table

![Write_to_Detla_Databricks](./images/WritetoDelta.png)

-	Write into Synapse - Write the final dataset in Synapse.

![Write_to_Syanpse](./images/Write_to_Syanpse.png)

-	Drop temp view & delta table (optional)

![Drop_view_table](./images/Optional_step.png)

Here is an example notebook for reference - [Synapse to Databricks KPI](https://adb-8516392274079895.15.azuredatabricks.net/?o=8516392274079895#notebook/4311880607761340/command/4311880607761342)
