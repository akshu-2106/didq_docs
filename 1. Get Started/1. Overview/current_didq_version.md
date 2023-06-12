# Current Version of DIDQ

Please find the below-mentioned enhancements/upgrades done on DIDQ, which added more levels of security without disturbing any existing/current code base. We are expecting all the Data Products to be on the same versions.
As a learning curve, we are moving towards the process of releases, where we will club all the releases/upgrades on a Quarterly basis and all these releases will be available in the developer portal with detailed information's and logs.

-	Dedicated Azure Resource Group for each Data Product and migrating the current resources from the EDNA Resources Group to its individual Resource Group. For more details, refer: [Infrastructure Request Template](https://developer.elanco.com/dataops/data-product/development/infrastructure-request-template)

-	Earlier we were having centralized DIDQ tables, views inside ControlOps, DataOps database. Now, we are securing the Data Product at each level, we have separate Data Product schema in ControlOps, DataOps database same as Synapse. Only authorized users can access any ControlOps, DataOps tables, or views in the database. For more details, refer: [Database Data Product](https://github.com/elanco/DataOps_DIDQFramework/tree/master/Database/Database_dataProduct)

-	Concept of Dynamic Schema, which will fasten the implementation in case of any additional changes in schema/table definition or in case of onboarding any new table in any Data Product. For more details, refer: [Dynamic Schema](https://developer.elanco.com/dataops/data-ingestion-and-data-quality/3-services/dynamic-schema)

-	Concept to Databricks Job Cluster and moving away from centralized Databricks Cluster which is acting as a blocker in current running Production because each Product is using the same compute power and ending up deadlocking the resources and affecting each Data Product. Databricks Job Cluster will have it's own dedicated compute power for each Data Product level and based on each Data Product we choose its own compute power. Easy to upgrade, easy to do cost analysis at Data Product level, no deadlock, high performance. For more details, refer: [Job Cluster](https://developer.elanco.com/dataops/data-ingestion-and-data-quality/3-services/job-cluster)

-	Using Git Hub Action in all the Data Products. For more details, refer: [GitHub](https://developer.elanco.com/dataops/github)

-	Enabling the SCIM access policy in Databricks which will sync with Azure Security Groups (Currently in Dev- will be taken care by Andrew Melwin Raj D).
