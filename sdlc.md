 PBI REPORTS:
Commercial -> 
	Reckitt Core Workspace:
		RGM: Dedicated Resource Group:
			-> Azure Data factory
				-> Triggers
					-> Main Pipeline
						-> Activity
							-> /Repos/trinity-rgm-core/trinity-uc-rgm-databricks_new/RGM/pat/PAT Refresh_POS
							-> create sheet woth below fields:
								Trigger, Main Pipeline, Activity, Notebook, read (files/tables), write(files,tables,json outuput)

							-> /Repos/trinity-rgm-core/trinity-uc-rgm-databricks_new/RGM/pat/master


			-> Storage Accounts
			Dedicated Resource Groups for Databricks:
			-> ADB Repo
-------------------------------------------------------------------------------------------------------------------------------------
Azure Data factory - Pipelines : Raw Data -> Bronze Table -> Silver -> Gold /Gold Plus

Analysis:
Table names - Source and Target
Source: Silver / Bronze / Master Data Tables (Gold)

Capture:
 1. all the tables needed from silver layer till the final pipeline

	https://rbcom.sharepoint.com/:x:/s/EHTrinitySplit/EcLvGQvm0gZOk5bJ7My1a1cBQBjCEWImebrcL8CxTtf8FQ?e=kovNzk&wdOrigin=TEAMS-WEB.p2p_ns.rwc&wdExp=TEAMS-TREATMENT&wdhostclicktime=1764668475171&web=1
 2. Files : config files, static data



Delta shared tables will be used for:
	1. History Load
	2. Incremental Loading Silver / Bronze tables
	3. Actual pipelines

	Connect with:
		1. DV team (get the details of POC): Get all the table and sharpeoint details
		2. Followup with Devops/Platform Team

-------------------------------------------------------------------------------------------------------------------------------------
	EH WORKSPACE:
		RGM: Dedicated Resource Group:
		-> Azure Data factory
			-> Triggers
		-> Storage Accounts
		Dedicated Resource Groups for Databricks:
		-> ADB Repo
		-> ADO Repo

Connect with:
		1. Followup with Devops/Platform Team: Fix the bugs

		2. DV team (get the details of POC): To provide the details for all the datasets

-------------------------------------------------------------------------------------------------------------------------------------
Delta share:
	1. Silver: az_trinity_non_gxp_dev_silver_eh
	2. Gold: az_trinity_non_gxp_dev_gold_eh
ADB repo changes:
	1. create branch, clone it
	1. Parameterise: Catalog and storage accounts (Update the values)
	2. Table Type: If it is UC or HMS
		-> HMS: Create similar table in UC
	3. Un-necessary for our development: Sharepoint/Snowflake
	3. Historical Load: Add a new notebook and table details for load (All tables)
	4. Incremental Load: Add a notebook and table details (Silver/bronze tables)

	5. Update the ADF pipeline notebook activity paths

old path: /Repos/trinity-rgm-core/trinity-uc-rgm-databricks_new/RGM/pat/master

new path: /Commerical/trinity-rgm-core/trinity-uc-rgm-databricks_new/RGM/pat/master

In dev:
adb_repo_base: /Workspace/Repos/rakesh.choudhary@reckitt.com/trinity-uc-rgm-databricks_new

Verify the data in RC (Reckitt core) and EH (Essential Home)

rc - az_trinity_non_gxp_dev_silver_eh.table1
eh - eh_catalog.table1


After dev:
adb_repo_base: /Commerical/trinity-rgm-core/trinity-uc-rgm-databricks_new

@{pipeline().globalParameters.adb_repo_base}/RGM/pat/core_plus_trigger_file_creation

-------------------------------------------------------------------------------------------------------------------------------------
ADF changes:
 - create branch
 - modify/ update the pipelines (notebook paths, global parameters)

SDLC:
	1. Analysis
	2. Share the dependencies with Platform team (Tables, Files)
	3. Clone the ADB repo - make changes and run it using you rlocal changes in ADF
	4. update the ADF pipelines and test them - Test all the changes in dev
	5. Push the code to develop branch for both ADB and ADF
	6. Test all the changes in dev
	7. Push the changes to Main branch
	8. Test all the changes in prod

-------------------------------------------------------------------------------------------------------------------------------------	