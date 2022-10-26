<img src="etc/images/sbd_logo.png" alt="drawing" width="200"/>

# GIT OneSource DataMart Sustainability (GODS)

## Table Of Contents
- [Versions](#versions-)
    - [Revision History](#project_revisionhistory)
    - [dbt Project Version](#dbt_project_version_info)
- [Overview](#dbt_project_overview)
- [Application Functional Overview](#dbt_project_components)
    - [Project Input](#dbt_project_input)
        - [Source Data from Raw Layer](#dbt_project_input_source_tables)
        - [Static/Seeds](#dbt_project_input_static_or_seeds)
    - [Cleansing/Transformation](#dbt_project_cleansing_and_transformation)
    - [Project Output](#dbt_project_output)
    - [Data Lineage](#dbt_project_data_lineage)
    - [Functional Context](#dbt_project_functional_context)
- [Using This dbt Project](#dbt_project_using_this_one)
    - [Project Structure](#dbt_project_structure)
    - [Permissions](#dbt_project_permissions)
    - [Project Settings](#dbt_project_settings)
    - [Project Packages/Dependencies](#dbt_project_packages_dependencies)
    - [Development Environment Setup](#dbt_project_development_environnment)
        - [Local Development: VSCode/Atom etc](#dbt_project_input_local_development)
        - [Developing in the Cloud IDE](#dbt_project_input_cloud_ide_development)
- [dbt Commands: How to Run](#dbt_project_howtorun)
    - [To get dependencies](#dbt_howtorun_deps)
    - [To compile the dbt project](#dbt_howtorun_compile)
    - [To get the documentation](#dbt_howtorun_docsgenerate)
    - [Loading static/seed files](#dbt_howtorun_seed)
    - [Mart build](#dbt_howtorun_martbuild)
    - [List Project resources](#dbt_howtorun_ls)
- [Control/Audit Framework/Monitoring](#dbt_project_audit_control_framework)
- [Testing](#dbt_project_testing)
    - [Continuos Integration: Bitbucket Pipelines](#dbt_project_ci)
        - [Credentials](#dbt_project_ci_credentials)
        - [Pipe Setup](#dbt_project_ci_pipe_setup)
    - [dbt Tests](#dbt_ci_dbt_tests)
- [Deployment](#dbt_project_deployment)
    - [Continuous Deployment: dbt_runner](#dbt_cd_dbt_runner)
        - [Credentials](#dbt_project_cd_credentials)
        - [Alerts](#dbt_project_cd_alerts)
        - [Job Names](#dbt_project_cd_job_names)
        - [Adhoc Runs](#dbt_project_adhoc_runs)
        - [(Re-)Loading seeded files](#dbt_project_adhoc_runs_seeds)
        - [(Re-)Loading static S3 files](#dbt_project_adhoc_runs_s3_files)
        - [Orchestration](#dbt_project_cd_orchestration)
- [Support Team Structure](#dbt_project_support_team_structure)
- [Service Level Agreements (SLA)](#dbt_project_sla)
- [Troubleshoot/ F.A.Q](#dbt_troubleshoot)
    - [known Issues](#dbt_troubleshoot_known_issues)
    - [Debugging](#dbt_troubleshoot_debugging)
- [Migration Notes](#dbt_project_migration_notes)
- [Resources](#resources-)
- [Cutover Plan](#cutover_plan)

# Versions <a name="versions-"></a>

## Revision History <a name="project_revisionhistory"></a>

|**Version** | **Revision Date** |
| :-------: | :-------: |
|v1.0   | October 10, 2022

## dbt Project Version <a name="dbt_project_version_info"></a>

|**Version** | **Latest Version used for testing** | 
| :-------: | :-------: | 
|1.0.0   | 1.0.3 | 


# Overview <a name="dbt_project_overview"></a>

# Application Functional Overview <a name="dbt_project_components"></a>

## Project Input <a name="dbt_project_input"></a>

###  Source Data from Raw Layer  <a name="dbt_project_input_source_tables"></a>

The following raw tables are consumed by this project

| **Database** | **Source System/Schema** | **Views** |
| :------------: | :--------------: | :-----------------: |
|	PROD_RAW	|	PPM	|	VW_BIZ_COM_PERIODS	|
|	PROD_RAW	|	PPM	|	VW_CMN_CAPTIONS_NLS	|
|	PROD_RAW	|	PPM	|	VW_CMN_LOOKUPS	|
|	PROD_RAW	|	PPM	|	VW_CMN_LOOKUPS_V	|
|	PROD_RAW	|	PPM	|	VW_DEPARTMENTS	|
|	PROD_RAW	|	PPM	|	VW_FIN_COST_PLAN_DETAILS	|
|	PROD_RAW	|	PPM	|	VW_FIN_PLANS	|
|	PROD_RAW	|	PPM	|	VW_INV_APPLICATIONS	|
|	PROD_RAW	|	PPM	|	VW_INV_FLAT_HIERARCHIES	|
|	PROD_RAW	|	PPM	|	VW_INV_HIERARCHIES	|
|	PROD_RAW	|	PPM	|	VW_INV_IDEAS	|
|	PROD_RAW	|	PPM	|	VW_INV_INVESTMENTS	|
|	PROD_RAW	|	PPM	|	VW_INV_OTHERS	|
|	PROD_RAW	|	PPM	|	VW_INV_PROJECTS	|
|	PROD_RAW	|	PPM	|	VW_NBI_DIM_CALENDAR_TIME	|
|	PROD_RAW	|	PPM	|	VW_NBI_DIM_OBS	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_COP_PRJ_STATUSRPT	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_COSTPLAN	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_COSTPLANDETAIL	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_DEPARTMENT	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_IDEA	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_INV	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_PROJECT	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_RESOURCE	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_SBD_ALLOCATION_METH	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_SBD_BUSI_CAPABILITY	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_SBD_CAPITAL	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_SBD_CAPITAL_DETAILS	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_SBD_COST_CENTER	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_SBD_PFL_FORECAST	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_SBD_SOW	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_SBD_WRK_ORDR	|
|	PROD_RAW	|	PPM	|	VW_ODF_CA_TEAM	|
|	PROD_RAW	|	PPM	|	VW_ODF_MULTI_VALUED_LOOKUPS	|
|	PROD_RAW	|	PPM	|	VW_ODF_OBJECTS	|
|	PROD_RAW	|	PPM	|	VW_ODF_SSL_CST_DTL_COST	|
|	PROD_RAW	|	PPM	|	VW_ODF_SSL_CST_DTL_UNITS	|
|	PROD_RAW	|	PPM	|	VW_PAC_MNT_PROJECTS	|
|	PROD_RAW	|	PPM	|	VW_PAC_MNT_RESOURCES	|
|	PROD_RAW	|	PPM	|	VW_PPA_WIP	|
|	PROD_RAW	|	PPM	|	VW_PPA_WIP_VALUES	|
|	PROD_RAW	|	PPM	|	VW_PPM_PHASE_DATA	|
|	PROD_RAW	|	PPM	|	VW_PRASSIGNMENT	|
|	PROD_RAW	|	PPM	|	VW_PRCALENDAR	|
|	PROD_RAW	|	PPM	|	VW_PRJ_BASELINE_DETAILS	|
|	PROD_RAW	|	PPM	|	VW_PRJ_BASELINES	|
|	PROD_RAW	|	PPM	|	VW_PRJ_BLB_SLICEREQUESTS	|
|	PROD_RAW	|	PPM	|	VW_PRJ_BLB_SLICES	|
|	PROD_RAW	|	PPM	|	VW_PRJ_OBS_ASSOCIATIONS	|
|	PROD_RAW	|	PPM	|	VW_PRJ_OBS_TYPES	|
|	PROD_RAW	|	PPM	|	VW_PRJ_OBS_UNITS	|
|	PROD_RAW	|	PPM	|	VW_PRJ_RESOURCES	|
|	PROD_RAW	|	PPM	|	VW_PRNOTE	|
|	PROD_RAW	|	PPM	|	VW_PRTASK	|
|	PROD_RAW	|	PPM	|	VW_PRTEAM	|
|	PROD_RAW	|	PPM	|	VW_PRTIMEENTRY	|
|	PROD_RAW	|	PPM	|	VW_PRTIMEPERIOD	|
|	PROD_RAW	|	PPM	|	VW_PRTIMESHEET	|
|	PROD_RAW	|	PPM	|	VW_RIM_RISKS_AND_ISSUES	|
|	PROD_RAW	|	PPM	|	VW_SRM_COMPANIES	|
|	PROD_RAW	|	PPM	|	VW_SRM_RESOURCES	|
|	PROD_RAW	|	PPM	|	VW_TRANSCLASS	|
|	PROD_RAW	|	SERVICENOW	|	VW_PROBLEM	|
|	PROD_RAW	|	SERVICENOW	|	VW_INCIDENT	|
|	PROD_RAW	|	SERVICENOW	|	VW_CHANGE_REQUEST	|
|	PROD_RAW	|	SERVICENOW	|	VW_RM_ENHANCEMENT	|
|	PROD_RAW	|	SERVICENOW	|	VW_U_SDLC_LITE	|
|	PROD_RAW	|	SERVICENOW	|	VW_CMDB_CI_SERVICE	|
|	PROD_RAW	|	SERVICENOW	|	VW_ITEM_OPTION_NEW	|
|	PROD_RAW	|	SERVICENOW	|	VW_SC_ITEM_OPTION	|
|	PROD_RAW	|	SERVICENOW	|	VW_SC_ITEM_OPTION_MTOM	|
|	PROD_RAW	|	SERVICENOW	|	VW_SC_REQ_ITEM	|
|	PROD_RAW	|	SERVICENOW	|	VW_SYS_USER	|
|	PROD_RAW	|	SERVICENOW	|	VW_SYSAPPROVAL_APPROVER	|
|	PROD_RAW	|	SERVICENOW	|	VW_TASK	|
|	PROD_RAW	|	SERVICENOW	|	VW_SC_REQUEST	|
|	PROD_RAW	|	SERVICENOW	|	VW_METRIC_INSTANCE	|
|	PROD_RAW	|	SERVICENOW	|	VW_U_PORTFOLIO_SEGMENT_LOOKUP	|
|	PROD_RAW	|	SERVICENOW	|	VW_U_MODULES	|
|	PROD_RAW	|	SERVICENOW	|	VW_SYS_USER_GROUP	|
|	PROD_RAW	|	SERVICENOW	|	VW_TBL_HCLENHANCEMENTS_SNAPSHOTS	|
|	

###  Static/Seeds <a name="dbt_project_input_static_or_seeds"></a>

The following static tables are used by this project

| **FILE_NAME** | **TABLE_NAME** |
| :--------: | :------------: |
|	dbo_forecast_6.csv	|	dbo_forecast_6	|
|	metric_instance_from_sys_history.csv	|	metric_instance_from_sys_history	|
|	dbo_es_bi_report_classifications.csv	|	dbo_es_bi_report_classifications	|
|	dbo_msp_project_list.csv	|	dbo_msp_project_list	|
|	dbo_mws_exceptions_list.csv	|	dbo_mws_exceptions_list	|
|	dbo_tbl_dw_cappm_cost_centers.csv	|	dbo_tbl_dw_cappm_cost_centers	|
|	ppm_tbl_mspdomaintowermapping.csv	|	ppm_tbl_mspdomaintowermapping	|
|	ppm_tbl_resourcehoursmodeled.csv	|	ppm_tbl_resourcehoursmodeled	|
|	dbo_tbl_dw_cappm_pde_projects_snapshot.csv	|	dbo_tbl_dw_cappm_pde_projects_snapshot	|
|	dbo_tbl_dw_cappm_rate_matrix.csv	|	dbo_tbl_dw_cappm_rate_matrix	|
|	ppm_phase_data_by_phase.csv	|	ppm_phase_data_by_phase	|
|	ppm_phase_data_by_phase_archive.csv	|	ppm_phase_data_by_phase_archive	|
|	tbl_hclenhancements.csv	|	tbl_hclenhancements	|
|	tbl_hclenhancements_snapshots.csv	|	tbl_hclenhancements_snapshots	|
|	tbl_hclenhancements_stage.csv	|	tbl_hclenhancements_stage	|

## Cleansing/Transformation <a name="dbt_project_cleansing_and_transformation"></a>

This project handles the following transformations/cleansing or curation details during its execution.

| **SCHEMA** | **TABLE_NAME** | **TRANSFORMATION/CLEANSING/CURATION NOTES** |
| :--------: | :------------: | :------------------------: |
|            |                |                            |

## Project Output <a name="dbt_project_output"></a>

This project produces the following tables in snowflake

| **SCHEMA** | **TABLE_NAME** | **TARGET STRUCTURE NOTES** |
| :--------: | :------------: | :------------------------: |
|	PROD_MARTS	|	GODS	|   VWRPT_GITOS_ROADMAPSUMMARYVIEWREPORTALLYEARS	|  |
|	PROD_MARTS	|	GODS	|   VWRPT_ROADMAPSUMMARYACTUAL_AY	|  |
|	PROD_MARTS	|	GODS	|   VWRPT_ROADMAPSUMMARYBASELINE_AY	|  |
|	PROD_MARTS	|	GODS	|   VWRPT_ROADMAPSUMMARYFORECAST_AY	|  |
|	PROD_MARTS	|	GODS	|   VW_AERMINTASK	|  |
|	PROD_MARTS	|	GODS	|   VW_APPROVALS	|  |
|	PROD_MARTS	|	GODS	|   VW_APPTIO_PPM_OBSDETAILS	|  |
|	PROD_MARTS	|	GODS	|   VW_APPTIO_PPM_PROJECTS	|  |
|	PROD_MARTS	|	GODS	|   VW_APPTIO_PPM_TIMESHEETS	|  |
|	PROD_MARTS	|	GODS	|   VW_APPTIO_PPM_TIMESHEETS_WIP	|  |
|	PROD_MARTS	|	GODS	|   VW_BI_REPORT_DETAILS	|  |
|	PROD_MARTS	|	GODS	|   VW_CLOSEDMONTHACTUALS_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_CLOSEDMONTHNPDACTUALS_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_CURRENTROADMAPPROJECTINFO_CURRENTFY	|  |
|	PROD_MARTS	|	GODS	|   VW_DW_CAPPM_PDE_DETAILS_SNAPSHOT_2018_ROADMAPSUMMARYFORECAST	|  |
|	PROD_MARTS	|	GODS	|   VW_DW_CAPPM_PDE_DETAILS_SNAPSHOT_2019_ROADMAPSUMMARYFORECAST	|  |
|	PROD_MARTS	|	GODS	|   VW_DW_CAPPM_PDE_DETAILS_SNAPSHOT_2020_ROADMAPSUMMARYFORECAST	|  |
|	PROD_MARTS	|	GODS	|   VW_DW_CAPPM_PDE_DETAILS_SNAPSHOT_2021_ROADMAPSUMMARYFORECAST	|  |
|	PROD_MARTS	|	GODS	|   VW_DW_CAPPM_PDE_DETAILS_SNAPSHOT_2022_ROADMAPSUMMARYFORECAST	|  |
|	PROD_MARTS	|	GODS	|   VW_ENHANCEMENTLIST	|  |
|	PROD_MARTS	|	GODS	|   VW_ENHANCEMENTSCOMBINED	|  |
|	PROD_MARTS	|	GODS	|   VW_ENHANCEMENTS_CLOSED_REPORTVIEW	|  |
|	PROD_MARTS	|	GODS	|   VW_ENHANCEMENT_REQUESTITEM	|  |
|	PROD_MARTS	|	GODS	|   VW_ENHANCEMENT_REQUESTITEM_STATIC_COMBINED	|  |
|	PROD_MARTS	|	GODS	|   VW_ENH_AERMINTASK	|  |
|	PROD_MARTS	|	GODS	|   VW_ENH_ROMESTMINTASK	|  |
|	PROD_MARTS	|	GODS	|   VW_EPR_INV_HIERARCHIES	|  |
|	PROD_MARTS	|	GODS	|   VW_EPR_STATS	|  |
|	PROD_MARTS	|	GODS	|   VW_EVRBYPROJECT	|  |
|	PROD_MARTS	|	GODS	|   VW_FT_ALTERYX_UPLOAD_EFFORT_ACTUALS_DATA	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_90DAYPROJECTSTARTSREPORT	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_EOFINVESTMENTSREPORT_1	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_MONTHENDLABORREPORT	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_MONTHENDLABORREPORTLATESTARTS	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_MONTHLYRESOURCETIMEANALYSISREPORT	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_MSPDISTRIBUTIONANALYSISREPORT	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_OBSANALYSISREPORT	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_PHASEVALIDATIONANALYSISREPORT_1	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_PHASEVALIDATIONANALYSISREPORT_2	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_PIPELINEIDEASREPORT	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_PMOHEALTHTRENDREPORT_PROJECTS	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_PROJECTASSIGNMENTSREPORT	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_PROJECTATTRIBUTESREPORT_PRJSINFO	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_PROJECTATTRIBUTESREPORT_PRJSINFO_ALL	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_PROJECTATTRIBUTESREPORT_STATUSINFO	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_PROJECTATTRIBUTESREPORT_STATUSINFO_ALL	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_ROADMAPSUMMARYVIEWREPORT	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_TIMECOMPLIANCEREPORT_1	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_TIMECOMPLIANCEREPORT_3	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_TIMESHEETDETAILSREPORT	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_TOLLGATEREPORT_PROJ	|  |
|	PROD_MARTS	|	GODS	|   VW_GITOS_TOLLGATEREPORT_STAT	|  |
|	PROD_MARTS	|	GODS	|   VW_HCLENHANCEMENTS	|  |
|	PROD_MARTS	|	GODS	|   VW_HCLENHANCEMENTS_STATIC_COMBINED	|  |
|	PROD_MARTS	|	GODS	|   VW_IDEAS_ALL_IN_FY	|  |
|	PROD_MARTS	|	GODS	|   VW_IDEAS_ALL_IN__FISCAL_FY	|  |
|	PROD_MARTS	|	GODS	|   VW_INCIDENT_P1S	|  |
|	PROD_MARTS	|	GODS	|   VW_INVESTMENTLIST	|  |
|	PROD_MARTS	|	GODS	|   VW_INVESTMENT_COST_SUMMARY	|  |
|	PROD_MARTS	|	GODS	|   VW_MSPPROJECTDETAILS_CONSULTING	|  |
|	PROD_MARTS	|	GODS	|   VW_OBSDEPARTMENTDETAILS	|  |
|	PROD_MARTS	|	GODS	|   VW_OBSDETAILS	|  |
|	PROD_MARTS	|	GODS	|   VW_OBSDETAILSACTIVE_TBM	|  |
|	PROD_MARTS	|	GODS	|   VW_OBSDETAILSALL	|  |
|	PROD_MARTS	|	GODS	|   VW_OBSDETAILSALLDETAILED	|  |
|	PROD_MARTS	|	GODS	|   VW_OBSDETAILSALLFORSERVICEXOG	|  |
|	PROD_MARTS	|	GODS	|   VW_OBSDETAILSV2	|  |
|	PROD_MARTS	|	GODS	|   VW_OBSDETAILS_MODELED	|  |
|	PROD_MARTS	|	GODS	|   VW_PDE	|  |
|	PROD_MARTS	|	GODS	|   VW_PDETEST	|  |
|	PROD_MARTS	|	GODS	|   VW_PPM_PHASE_DATA_BY_PHASE	|  |
|	PROD_MARTS	|	GODS	|   VW_PROBLEM	|  |
|	PROD_MARTS	|	GODS	|   VW_PROJECTS_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_REQUESTITEMVARIABLES	|  |
|	PROD_MARTS	|	GODS	|   VW_RESOURCEALLOCATIONBYPROJECTBYMONTH	|  |
|	PROD_MARTS	|	GODS	|   VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL	|  |
|	PROD_MARTS	|	GODS	|   VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL_ALLCONVERTED	|  |
|	PROD_MARTS	|	GODS	|   VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL_ALLCONVERTEDWITHIDEAS	|  |
|	PROD_MARTS	|	GODS	|   VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL_ALLCONVERTED_SERVICEDUPLICATES	|  |
|	PROD_MARTS	|	GODS	|   VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL_ALLCONVERTED_VELOCITY	|  |
|	PROD_MARTS	|	GODS	|   VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL_ALLCONVERTED_VELOCITYALLRESOURCES	|  |
|	PROD_MARTS	|	GODS	|   VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL_PROJECTSCONVERTED	|  |
|	PROD_MARTS	|	GODS	|   VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_MODELED	|  |
|	PROD_MARTS	|	GODS	|   VW_RESOURCEDOMAINOBSDETAILS	|  |
|	PROD_MARTS	|	GODS	|   VW_RESOURCEOBSDETAILS	|  |
|	PROD_MARTS	|	GODS	|   VW_RESOURCEOBSDETAILSALL	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYACTUALEFFORT_VELOCITY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYACTUAL_CPY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYACTUAL_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYBASELINE_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYBASELINE_FY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYBUDGET_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYBUDGET_FY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYBYPROJECT_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYBYPROJECT_CY_PLUS_1	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYFORECAST6_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYFORECAST_ALLYEARS	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYFORECAST_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYFORECAST_FY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYIDEAFORECAST_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYIDEAFORECAST_FY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYNPDACTUALADMIN_CPY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYNPDACTUAL_CPY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYNPDACTUAL_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYNPDBUDGET_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYNPDBUDGET_FY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYNPDFORECASTADMIN_FY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYNPDFORECAST_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYNPDFORECAST_FY	|  |
|	PROD_MARTS	|	GODS	|   VW_ROADMAPSUMMARYRESOURCEALLOCATIONS_CALENDAR	|  |
|	PROD_MARTS	|	GODS	|   VW_SBSDETAILS	|  |
|	PROD_MARTS	|	GODS	|   VW_SITC_MSPDISTRIBUTIONANALYSISREPORT	|  |
|	PROD_MARTS	|	GODS	|   VW_SOX_AUDIT_DATA_FINAL	|  |
|	PROD_MARTS	|	GODS	|   VW_SOX_PROJECT_INFO	|  |
|	PROD_MARTS	|	GODS	|   VW_TBM	|  |
|	PROD_MARTS	|	GODS	|   VW_TOTALPROJECTCOST_CY	|  |
|	PROD_MARTS	|	GODS	|   VW_UNSUBMITTEDTIMESHEETS_CY		|  |
|	PROD_MARTS	|	GODS	|   VW_VELOCITY_GENERICDEMAND	|  |
|	PROD_MARTS	|	GODS	|   TBL_ENHANCEMENTSCOMBINED	|  |
|	PROD_MARTS	|	GODS	|   TBL_REQUESTITEMVARIABLES	|  |

## Data Lineage <a name="dbt_project_data_lineage"></a>

![Scheme](etc/images/dbt-dag-gods.png "This is ")


## Functional Context <a name="dbt_project_functional_context"></a>



# Using This dbt Project <a name="dbt_project_using_this_one"></a>

## Project structure

The project strucutre looks as follows: 

```
.
├── README.md
├── analyses
│   └── .gitkeep

│   ├── data
│   │   │  ├── dbo_forecast_6.csv	
│   │   │  ├── metric_instance_from_sys_history.csv	
│   │   │  ├── dbo_es_bi_report_classifications.csv	
│   │   │  ├── dbo_msp_project_list.csv	
│   │   │  ├── dbo_mws_exceptions_list.csv	
│   │   │  ├── dbo_tbl_dw_cappm_cost_centers.csv		
│   │   │  ├── ppm_tbl_mspdomaintowermapping.csv		
│   │   │  ├── dbo_tbl_dw_cappm_pde_projects_snapshot
│   │   │  ├── ppm_tbl_resourcehoursmodeled.csv			
│   │   │  ├── dbo_tbl_dw_cappm_rate_matrix.csv	
│   │   │  ├── ppm_phase_data_by_phase.csv	
│   │   │  ├── ppm_phase_data_by_phase_archive.csv
│   │   │  ├── tbl_hclenhancements.csv	
│   │   │  ├── tbl_hclenhancements_snapshots.csv	
│   │   │  ├── tbl_hclenhancements_stage.csv	
│   ├── dbt_project.yml
│   ├── macros
│   │   ├── init_project.sql
│   │   └── execute_procs.sql
│   ├── models
│   │   ├── marts	
│   │   │   │   ├── VWRPT_GITOS_ROADMAPSUMMARYVIEWREPORTALLYEARS	
│   │   │   │   ├── VWRPT_ROADMAPSUMMARYACTUAL_AY	
│   │   │   │   ├── VWRPT_ROADMAPSUMMARYBASELINE_AY	
│   │   │   │   ├── VWRPT_ROADMAPSUMMARYFORECAST_AY	
│   │   │   │   ├── VW_AERMINTASK	
│   │   │   │   ├── VW_APPROVALS	
│   │   │   │   ├── VW_APPTIO_PPM_OBSDETAILS	
│   │   │   │   ├── VW_APPTIO_PPM_PROJECTS	
│   │   │   │   ├── VW_APPTIO_PPM_TIMESHEETS	
│   │   │   │   ├── VW_APPTIO_PPM_TIMESHEETS_WIP	
│   │   │   │   ├── VW_BI_REPORT_DETAILS	
│   │   │   │   ├── VW_CLOSEDMONTHACTUALS_CY	
│   │   │   │   ├── VW_CLOSEDMONTHNPDACTUALS_CY	
│   │   │   │   ├── VW_CURRENTROADMAPPROJECTINFO_CURRENTFY	
│   │   │   │   ├── VW_DW_CAPPM_PDE_DETAILS_SNAPSHOT_2018_ROADMAPSUMMARYFORECAST	
│   │   │   │   ├── VW_DW_CAPPM_PDE_DETAILS_SNAPSHOT_2019_ROADMAPSUMMARYFORECAST	
│   │   │   │   ├── VW_DW_CAPPM_PDE_DETAILS_SNAPSHOT_2020_ROADMAPSUMMARYFORECAST	
│   │   │   │   ├── VW_DW_CAPPM_PDE_DETAILS_SNAPSHOT_2021_ROADMAPSUMMARYFORECAST	
│   │   │   │   ├── VW_DW_CAPPM_PDE_DETAILS_SNAPSHOT_2022_ROADMAPSUMMARYFORECAST	
│   │   │   │   ├── VW_ENHANCEMENTLIST	
│   │   │   │   ├── VW_ENHANCEMENTSCOMBINED	
│   │   │   │   ├── VW_ENHANCEMENTS_CLOSED_REPORTVIEW	
│   │   │   │   ├── VW_ENHANCEMENT_REQUESTITEM	
│   │   │   │   ├── VW_ENHANCEMENT_REQUESTITEM_STATIC_COMBINED	
│   │   │   │   ├── VW_ENH_AERMINTASK	
│   │   │   │   ├── VW_ENH_ROMESTMINTASK	
│   │   │   │   ├── VW_EPR_INV_HIERARCHIES	
│   │   │   │   ├── VW_EPR_STATS	
│   │   │   │   ├── VW_EVRBYPROJECT	
│   │   │   │   ├── VW_FT_ALTERYX_UPLOAD_EFFORT_ACTUALS_DATA	
│   │   │   │   ├── VW_GITOS_90DAYPROJECTSTARTSREPORT	
│   │   │   │   ├── VW_GITOS_EOFINVESTMENTSREPORT_1	
│   │   │   │   ├── VW_GITOS_MONTHENDLABORREPORT	
│   │   │   │   ├── VW_GITOS_MONTHENDLABORREPORTLATESTARTS	
│   │   │   │   ├── VW_GITOS_MONTHLYRESOURCETIMEANALYSISREPORT	
│   │   │   │   ├── VW_GITOS_MSPDISTRIBUTIONANALYSISREPORT	
│   │   │   │   ├── VW_GITOS_OBSANALYSISREPORT	
│   │   │   │   ├── VW_GITOS_PHASEVALIDATIONANALYSISREPORT_1	
│   │   │   │   ├── VW_GITOS_PHASEVALIDATIONANALYSISREPORT_2	
│   │   │   │   ├── VW_GITOS_PIPELINEIDEASREPORT	
│   │   │   │   ├── VW_GITOS_PMOHEALTHTRENDREPORT_PROJECTS	
│   │   │   │   ├── VW_GITOS_PROJECTASSIGNMENTSREPORT	
│   │   │   │   ├── VW_GITOS_PROJECTATTRIBUTESREPORT_PRJSINFO	
│   │   │   │   ├── VW_GITOS_PROJECTATTRIBUTESREPORT_PRJSINFO_ALL	
│   │   │   │   ├── VW_GITOS_PROJECTATTRIBUTESREPORT_STATUSINFO	
│   │   │   │   ├── VW_GITOS_PROJECTATTRIBUTESREPORT_STATUSINFO_ALL	
│   │   │   │   ├── VW_GITOS_ROADMAPSUMMARYVIEWREPORT	
│   │   │   │   ├── VW_GITOS_TIMECOMPLIANCEREPORT_1	
│   │   │   │   ├── VW_GITOS_TIMECOMPLIANCEREPORT_3	
│   │   │   │   ├── VW_GITOS_TIMESHEETDETAILSREPORT	
│   │   │   │   ├── VW_GITOS_TOLLGATEREPORT_PROJ	
│   │   │   │   ├── VW_GITOS_TOLLGATEREPORT_STAT	
│   │   │   │   ├── VW_HCLENHANCEMENTS	
│   │   │   │   ├── VW_HCLENHANCEMENTS_STATIC_COMBINED	
│   │   │   │   ├── VW_IDEAS_ALL_IN_FY	
│   │   │   │   ├── VW_IDEAS_ALL_IN__FISCAL_FY	
│   │   │   │   ├── VW_INCIDENT_P1S	
│   │   │   │   ├── VW_INVESTMENTLIST	
│   │   │   │   ├── VW_INVESTMENT_COST_SUMMARY	
│   │   │   │   ├── VW_MSPPROJECTDETAILS_CONSULTING	
│   │   │   │   ├── VW_OBSDEPARTMENTDETAILS	
│   │   │   │   ├── VW_OBSDETAILS	
│   │   │   │   ├── VW_OBSDETAILSACTIVE_TBM	
│   │   │   │   ├── VW_OBSDETAILSALL	
│   │   │   │   ├── VW_OBSDETAILSALLDETAILED	
│   │   │   │   ├── VW_OBSDETAILSALLFORSERVICEXOG	
│   │   │   │   ├── VW_OBSDETAILSV2	
│   │   │   │   ├── VW_OBSDETAILS_MODELED	
│   │   │   │   ├── VW_PDE	
│   │   │   │   ├── VW_PDETEST	
│   │   │   │   ├── VW_PPM_PHASE_DATA_BY_PHASE	
│   │   │   │   ├── VW_PROBLEM	
│   │   │   │   ├── VW_PROJECTS_CY	
│   │   │   │   ├── VW_REQUESTITEMVARIABLES	
│   │   │   │   ├── VW_RESOURCEALLOCATIONBYPROJECTBYMONTH	
│   │   │   │   ├── VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL	
│   │   │   │   ├── VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL_ALLCONVERTED	
│   │   │   │   ├── VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL_ALLCONVERTEDWITHIDEAS	
│   │   │   │   ├── VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL_ALLCONVERTED_SERVICEDUPLICATES	
│   │   │   │   ├── VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL_ALLCONVERTED_VELOCITY	
│   │   │   │   ├── VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL_ALLCONVERTED_VELOCITYALLRESOURCES	
│   │   │   │   ├── VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_FINAL_PROJECTSCONVERTED	
│   │   │   │   ├── VW_RESOURCEALLOCATIONBYPROJECTBYMONTH_MODELED	
│   │   │   │   ├── VW_RESOURCEDOMAINOBSDETAILS	
│   │   │   │   ├── VW_RESOURCEOBSDETAILS	
│   │   │   │   ├── VW_RESOURCEOBSDETAILSALL	
│   │   │   │   ├── VW_ROADMAPSUMMARYACTUALEFFORT_VELOCITY	
│   │   │   │   ├── VW_ROADMAPSUMMARYACTUAL_CPY	
│   │   │   │   ├── VW_ROADMAPSUMMARYACTUAL_CY	
│   │   │   │   ├── VW_ROADMAPSUMMARYBASELINE_CY	
│   │   │   │   ├── VW_ROADMAPSUMMARYBASELINE_FY	
│   │   │   │   ├── VW_ROADMAPSUMMARYBUDGET_CY	
│   │   │   │   ├── VW_ROADMAPSUMMARYBUDGET_FY	
│   │   │   │   ├── VW_ROADMAPSUMMARYBYPROJECT_CY	
│   │   │   │   ├── VW_ROADMAPSUMMARYBYPROJECT_CY_PLUS_1	
│   │   │   │   ├── VW_ROADMAPSUMMARYFORECAST6_CY	
│   │   │   │   ├── VW_ROADMAPSUMMARYFORECAST_ALLYEARS	
│   │   │   │   ├── VW_ROADMAPSUMMARYFORECAST_CY	
│   │   │   │   ├── VW_ROADMAPSUMMARYFORECAST_FY	
│   │   │   │   ├── VW_ROADMAPSUMMARYIDEAFORECAST_CY	
│   │   │   │   ├── VW_ROADMAPSUMMARYIDEAFORECAST_FY	
│   │   │   │   ├── VW_ROADMAPSUMMARYNPDACTUALADMIN_CPY	
│   │   │   │   ├── VW_ROADMAPSUMMARYNPDACTUAL_CPY	
│   │   │   │   ├── VW_ROADMAPSUMMARYNPDACTUAL_CY	
│   │   │   │   ├── VW_ROADMAPSUMMARYNPDBUDGET_CY	
│   │   │   │   ├── VW_ROADMAPSUMMARYNPDBUDGET_FY	
│   │   │   │   ├── VW_ROADMAPSUMMARYNPDFORECASTADMIN_FY	
│   │   │   │   ├── VW_ROADMAPSUMMARYNPDFORECAST_CY	
│   │   │   │   ├── VW_ROADMAPSUMMARYNPDFORECAST_FY	
│   │   │   │   ├── VW_ROADMAPSUMMARYRESOURCEALLOCATIONS_CALENDAR	
│   │   │   │   ├── VW_SBSDETAILS	
│   │   │   │   ├── VW_SITC_MSPDISTRIBUTIONANALYSISREPORT	
│   │   │   │   ├── VW_SOX_AUDIT_DATA_FINAL	
│   │   │   │   ├── VW_SOX_PROJECT_INFO	
│   │   │   │   ├── VW_TBM	
│   │   │   │   ├── VW_TOTALPROJECTCOST_CY	
│   │   │   │   ├── VW_UNSUBMITTEDTIMESHEETS_CY		
│   │   │   │   ├── VW_VELOCITY_GENERICDEMAND	
│   │   │   │   ├── TBL_ENHANCEMENTSCOMBINED	
│   │   │   │   ├── TBL_REQUESTITEMVARIABLES
│   │   │   ├── source.yml
│   │   │   ├── onboarding
│   │   │   ├── marts
│   │   │   │  	├── proc_sp_dbo_tbl_dw_cappm_pde_projects_snapshot.sql
│   │   │   │  	├── proc_sp_ppm_phase_data_by_phase.sql
│   │   │   │  	├── proc_sp_tbl_hclenhancements_snapshots.sql
│   │   │   │  	├── proc_sp_updatehclenhancementstable.sql
│   │   ├── packages.yml

├── dbt_project.yml

```
This same project tree view above is persisted/versioned under *etc/project_tree_structure.md* - If project changes, please update both markdown documents.

## Permissions <a name="dbt_project_permissions"></a>

### Database Permissions

In order for this project to run successfuly, the following permissions are needed on Snowflake. 

| **DATABASE NAME** | **SCHEMA** | **TABLE NAME** | **PERMISSION** |
|--------------|---------------------|------------------------|------|
|    `<ENV>_RAW`          |       ALL              |      ALL                  |   READ   |
|    `<ENV>_MARTS`          |       SBDVAULT & GODS              |      ALL                  |   READ & WRITE  |

### Warehouse Permissions

Please consider the following virtual warehouse privileges

**Privilege** | **Usage**                                                                                                                                                                                                                                                   
----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 usage          | Enables using a virtual warehouse and, as a result, executing queries on the warehouse. If the warehouse is configured to auto-resume when a SQL statement (e.g. query) is submitted to it, the warehouse resumes automatically and executes the statement. 
 monitor        | Enables viewing current and past queries executed on a warehouse as well as usage statistics on that warehouse.               

**NOTE:** Replace `<ENV>` with the any of the following environment codes: `DEV, TEST or PROD`

## Project Settings <a name="dbt_project_settings"></a>

The project settings for this projects are persisted in the `dbt_project.yml` file

## Project Packages/Dependencies <a name="dbt_project_packages_dependencies"></a>

Project dependencies and packages are defined in the `packages.yml` file in the mart folder root level.

| Package               | Version | Usage                                |
|-----------------------|---------|--------------------------------------|
| Datavault-UK/dbtvault | 0.7.9   | Datavault 2.0 Packages and utilities |
| mart audit            | main    | Used to audit                        |
|                       |         |                                      |

## Development Environment Setup <a name="dbt_project_development_environnment"></a>

There are two possible environents where development can happen while building in Caspian environment. Namely: 
  1. Local Development - this can be IDE that is leveraging dbt core
  2. Cloud IDE - dbt cloud environment (COMING SOON to SBD Caspian)

Below are instructions to get setup on both of these environments.

### Local Development: VSCode/Atom etc <a name="dbt_project_input_local_development"></a>


  
1. #### Install Requirements <a name="dbt_project_input_local_development"></a>
    [Install dbt](https://docs.getdbt.com/dbt-cli/installation).   
    Optionally, you can [set up venv to allow for environment switching](https://discourse.getdbt.com/t/setting-up-your-local-dbt-run-environments/2353). 

2. #### Setup <a name="dbt_project_input_local_development"></a>

    Set up a profile called `marts_gods` to connect to a data warehouse by following [these instructions](https://docs.getdbt.com/docs/configure-your-profile). If you have access to a data warehouse, you can use those credentials – we recommend setting your [target schema](https://docs.getdbt.com/docs/configure-your-profile#section-populating-your-profile) to be a new schema (dbt will create the schema for you, as long as you have the right privileges). If you don't have access to an existing data warehouse, you can also setup a local postgres database and connect to it in your profile.
    Open your terminal and navigate to your `profiles.yml`. This is in the `.dbt` hidden folder on your computer, located in your home directory.

    On macOS, you can open the file from your terminal similar to this (which is using the Atom text editor to open the file):
    ```console
    $ atom ~/.dbt/profiles.yml
    ```

    Insert the following into your `profiles.yml` file and change out the bracketed lines with your own information.
    [Here is further documentation](https://docs.getdbt.com/docs/available-adapters#dbt-labs-supported) for setting up your profile.
    ```yaml
    marts_gods:
        outputs:
            dev:
            type: snowflake
            account: sbd_caspian.us-east-1

            # User/password auth
            user: <email username>@sbdinc.com
            authenticator: externalbrowser

            role: DEV_MARTBUILD_RW
            database: PROD_MARTS
            warehouse: DEV_MARTS_WH
            schema: DBT_<YOUR_USERNAME>
            threads: 50
            client_session_keep_alive: True
            query_tag: dbt_gods
        target: dev                        
    ```

    | Configuration Key              | Definition                                                                                                                                                                                                              |
    | ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | my_project                     | This is defining a profile - this specific name should be the profile that is referenced in our dbt_project.yml                                                                                                         |
    | target: dev                    | This is the default environment that will be used during our runs.                                                                                                                                                      |
    | outputs:                       | This is a prompt to start defining targets and their configurations. You likely won't need more than `dev`, but this and any other targets you define can be used to accomplish certain functionalities throughout dbt. |
    | dev:                           | This is defining a target named `dev`.                                                                                                                                                                                  |
    | type: [warehouse_name]         | This is the type of target connection we are using, based on our warehouse. For Caspian, snowflake should be used: Can be [env]_EDW_WH or [env]_MARTS_WH for example in DEV environment, the warehouse for EDW layer would be `DEV_EDW_WH`                                                               |
    | threads: 50                    | This is the amount of concurrent models that can run against our warehouse, for this user, at one time when conducting a `dbt run`                                                                                      |
    | account: sbd_caspian.us-east-1 | Change this out to the warehouse's account.  Defaulted to Caspian Snowflake URL                                                                                                                                         |
    | user: [your_username]          | Change this to use your own username that you use to log in to the warehouse. Use SBD userid of format ABC1234                                                                                                          |
    | authenticator: authenticator   | To use with SBD Single Sign On, use `authenticator` as the value to be prompted for a sign on window from Snowflake. Must use MFA during sign in.                                                                       |
    | role: transformer              | This is the role that has the correct permissions for working in this project.                                                                                                                                          |
    | database: analytics            | This is the database name where our models will build                                                                                                                                                                   |
    | schema: dbt_[userid]        | Change this to a custom name. Follow the convention `dbt_userid`. This is the schema that models will build into / test from when conducting runs locally.                                          |

3. Clone this repository
    
    ```console
    $ $ git clone -c core.longpaths=true -b feature/gods_servicenow https://srk0127@bitbucket.org/sbddatalake/sbd-dbt-marts.git
    ```

4. Change into the `gods` directory from the command line:
    ```console
    $ cd gods
    ```

5. Try running the following generic/common commands one at a time from your command line:
    - `dbt debug` - tests your connection. If this fails, check your profiles.yml.
    - `dbt deps`  - installs any packages defined in the packages.yml file.  
    For project specific commands see the section below on [dbt Commands: How to Run](#dbt_project_howtorun)


### Developing in the Cloud IDE <a name="dbt_project_input_cloud_ide_development"></a>

The easiest way to contribute to this project is by developing in dbt Cloud. If you have access, navigate to the develop tab in the menu and fill out any required information to get connected.

In the command line bar at the bottom of the interface, run the following generic/common commands one at a time:

- `dbt deps`  - installs any packages defined in the packages.yml file.

For project specific commands see the section below on [dbt Commands: How to Run](#dbt_project_howtorun)

# dbt Commands: How to Run <a name="dbt_project_howtorun"></a>
Assuming you have your environment setup as described in previous section, you can run the following commands to manage this dbt project during deployment.

### To get dependencies:  <a name="dbt_howtorun_deps"></a>

[dbt docs on deps command](https://docs.getdbt.com/reference/commands/deps)

    dbt deps

### To compile the dbt project  <a name="dbt_howtorun_compile"></a>
Generates executable SQL from source model, test, and analysis files. You can find these compiled SQL files in the target/ directory of your dbt project in your development environment. [See dbt docs on compile](https://docs.getdbt.com/reference/commands/compile)

    dbt compile

### To get the documentation:  <a name="dbt_howtorun_docsgenerate"></a>
Generate documentation for the project. [See dbt docs on docs generate](https://docs.getdbt.com/reference/commands/cmd-docs#dbt-docs-generate)

    dbt docs generate

To view the generated in local IDE, run the following command to start a webserver on default port 8000 and serve the generated documents. [See dbt docs on docs serve](https://docs.getdbt.com/reference/commands/cmd-docs#dbt-docs-serve)

    dbt docs serve

### Loading static/seed files <a name="dbt_howtorun_seed"></a>
Builds any .csv files as tables in the warehouse. These are located in the data/seed folder of the project. Otherwsie specified in the dbt_project.yml. This materializes the CSVs as tables in your target schema. Note that **not all projects require this step** since the assummption that raw data is already in your warehouse. See [dbt docs on seed](https://docs.getdbt.com/docs/building-a-dbt-project/seeds)

    dbt seed

### Mart build <a name="dbt_howtorun_martbuild"></a>

[dbt docs on seed](https://docs.getdbt.com/docs/building-a-dbt-project/seeds)

    dbt run

### List Project resources <a name="dbt_howtorun_ls"></a>

List project resource. [dbt docs on ls command and reference to resource selection syntax](https://docs.getdbt.com/reference/commands/list#overview)

    dbt ls

# Control/Audit Framework <a name="dbt_project_audit_control_framework"></a>

##	Introduction
Mart Auditor is a dbt package developed to capture runtime information about marts being executed in Caspian data loads. These runtime metrics can be used to analyze data marts executed in past and for auditing purpose.

##	Design
Any data mart that is developed in Caspian project can plug in Mart Auditor package to capture data mart run time metrics. Mart Auditor creates two different tables i.e., Batch and Batch_Loging for all marts in database. These tables can be used to query to know past executions, errors, execution re try's etc. 

 ![Scheme](etc/images/mart_audit_model.png)

Mart Auditor is a light weight dbt package that inserts records into above tables as mart progresses and creates table or views as part of model creating and execution. There is only one entry per execution of Mart in Batch table and multiple entries one per model in batch_logging table. Association between batch and batch_logging table is: 1 -> M



###	Batch table structure
To get the DDL Structure from Snowflake, run the command: `select get_ddl('table', 'PROD_MARTS.cf.batch');` and it will output the following:

```jql
create or replace TABLE BATCH (
	BATCHID NUMBER(38,0),
	RETRY_CNT NUMBER(38,0),
	DBT_MART VARCHAR(16777216),
	DBT_MART_REFRESH_TYPE VARCHAR(16777216),
	START_DATE TIMESTAMP_NTZ(9),
	END_DATE TIMESTAMP_NTZ(9),
	DURATION_IN_SECONDS NUMBER(38,0),
	LOAD_STATUS VARCHAR(16777216)
);
```

###	Batch_logging table structure
To get the DDL Structure from Snowflake, run the command: `select get_ddl('table', 'PROD_MARTS.gods.batch_logging');` and it will output the following:

```jql
create or replace TABLE BATCH_LOGGING (
	BLG_KEY NUMBER(38,0),
	BATCHID NUMBER(38,0),
	DBT_MART VARCHAR(16777216),
	DBT_MART_REFRESH_TYPE VARCHAR(16777216),
	DBT_MODEL_NAME VARCHAR(16777216),
	SF_TABLE_NAME VARCHAR(16777216),
	ROWS_BEFORE NUMBER(38,0),
	ROWS_AFTER NUMBER(38,0),
	STARTDATE TIMESTAMP_NTZ(9),
	COMPLETEDATE TIMESTAMP_NTZ(9),
	ERROR_MESSAGE VARCHAR(16777216)
);
```

##	Macros developed in Mart Auditor: 
Total 4 macros are developed as part of Mart Auditor dbt package. These macros can be called by any dbt mart by deploying into their dbt mart project.

###	Insert_batch : 
This macro inserts a record into batch table as soon as mart stars execution. Status in batch table will be inserted as “Started” along with Mart name, BatchID, StartDateTime etc.

###	insert_batch_logging : 
This macro inserts a record into batch_logging table as soon as any model in dbt mart stars executing. It will insert all the information about models that we execute as part of data mart. Important information like model name, mart name, rows in table/view before model executes, model execution start date time and model execution status as “Started” will be captured into table.

###	update_batch_logging: 
This macro is developed to validate the model executed by data mart. If a model in mart is executed successfully then this macro updates the previously inserted record in batch_logging table with updated values like status will be updated as completed, rows in table after model executes, end date time for model and Table or View name that macro creates in database.

###	Update_batch : 
Once all the models in data mart are executed successfully then this macro updates batch table record by changing status to completed and captures information like duration in seconds, retry_count etc. If any of the model in the mart is failed then this macro updates batch table with failed status and increase the retry count value by one.

##	Steps to use Mart Auditor in your dbt mart: 

*Note*: Mart Auditor is available in bitbucket at following location: 

Bitbucket Location: `https://bitbucket.org/sbddatalake/sbd_caspian_dbt_common_utilities/src/main/`

1.	Add Mart Auditor package in packages.yml file like below example:


2.	Execute “dbt deps” command to deploy mart auditor package into your dbt mart

3.	You can find mart auditor deployed into your “dbt pakages” folder of your project

4.	You can call above macros in your dbt_proejct.yml file with below example:

    1. Insert_batch(dbt_mart_name, dbt_mart_refresh_type) : 
        This macro accepts two parameters for Mart_name and Mart_refresh_type. Mart_refresh_type is optional parameter and if you don’t provide refresh type parameter then it will insert NULL value into batch table. Call this macro at “on-run-start” section of dbt_project.yml.

    2. insert_batch_logging (dbt_mart_name, dbt_model_name, table_name, refresh_type):
    This macro accepts four parameters for Mart_name, model_name, table_name and refresh_type. Table_name and refresh_type are optional parameters where table name takes model name and refresh_type takes null value by default if you don’t supply. Call this macro at pre-hook section of dbt_project.yml. Pass current model name to the macro with keyword “this”.

    3. Update_batch_logging (dbt_mart_name, dbt_model_name, table_name, refresh_type):
    This macro accepts four parameters for Mart_name, model_name, table_name and refresh_type. Table_name and refresh_type are optional parameters where table name takes model name and refresh_type takes null value by default if you don’t supply. Call this macro at post-hook section of dbt_project.yml

    4. update_batch (dbt_mart_name, dbt_mart_refresh_type) : 
    This macro accepts two parameters for Mart_name and Mart_refresh_type. Mart_refresh_type is optional parameter and if you don’t provide refresh type parameter then it will insert null value into batch table. Call this macro at “on-run-end” section of dbt_project.yml.


# Testing <a name="dbt_project_testing"></a>

## Continuos Integration: Bitbucket Pipelines <a name="dbt_project_ci"></a>


### Credentials <a name="dbt_project_ci_credentials"></a>

Credentials in a bitbucket pipe are passed through Repository variables. See more on Bitbucket pipeline and environment variables: [User-defined variables](https://support.atlassian.com/bitbucket-cloud/docs/variables-and-secrets/). 
The following variables have been configured with `DEV` service account details.

| **Custom Variable** | **Variable Description** |
|---------------------|--------------------------|
| DBT_TARGET_TYPE     |                          |
| DBT_TARGET_URL      |                          |
| DBT_USER            |                          |
| DBT_PASSWORD        |                          |

Most parameters are configured as a secret in Bitbucket and cannot be viewed.

### Pipe Setup <a name="dbt_project_ci_pipe_setup"></a>

This datamart project CI pipe is configured as step in a shared bitbucket pipeline yml file (at root level of this repo). The following is the settings for this mart. 

```yml
      - step:
          name: 'GODS DM - Compile'
          trigger: manual
          script:
            - echo "Starting build for GODS DM"
            - echo "$DBT_PROJECT_BITBUCKET_PUB_CERT" > ~/.ssh/authorized_keys
            - mkdir ~/.dbt
            - touch ~/.dbt/profiles.yml
            - 'echo -e "marts_gods:\n  outputs:\n    dev:\n      type: $DBT_TARGET_TYPE\n      account: $DBT_TARGET_URL\n\n      user: $DBT_USER\n      password: $DBT_PASSWORD\n\n      role: $DBT_ROLE\n      database: PROD_MARTS\n      warehouse: $DBT_WH\n      schema: GODS\n      threads: $DBT_NUM_THREADS\n      client_session_keep_alive: True\n      query_tag: dbt\n  target: dev\n " >> ~/.dbt/profiles.yml'
            - cd gods/
            - ls -ltr
            - dbt deps
            - dbt compile
            - echo "Done build for GODS DM"

```
## dbt Tests <a name="dbt_ci_dbt_tests"></a>

# Deployment<a name="dbt_project_deployment"></a>

## Continuous Deployment: dbt_runner <a name="dbt_cd_dbt_runner"></a>

This project can be run in Caspian TMC environment using the [dbt_runner template](https://sbd-ddbot.atlassian.net/wiki/spaces/CAS/pages/2202861577/dbt+Runner). This template is available on all environments and leveraged during from SIT to Deployment phase of a build project. 
The dbt_runner artifcat/template is responsible for: 

1. Cloning the latest code from specified branch and url in a repo
2. Setting up a profiles.yml for the tasks run based on the provided credentials.
3. Execute a `dbt deps` to get the project prepared for any commands passed
4. Run the provided dbt commands - send notification incase of error during this run
5. At job end, upload the dbt artifact files to S3 for technical lineage harvesting. The following files are uploaded to S3: `manifest.json`, `catalog.json (if available)` and the `run_results.json`

The three Caspian environments available for building and deployment of dbt projects: 

| **ENVIRONMENT** | **PURPOSE**                | **Branch used**               |
|-----------------|----------------------------|-------------------------------|
| DEV             | System Integration Testing | feature/[more_descptive_name] |
| TEST            | User Acceptance Testing    | feature/[more_descptive_name] |
| PROD            | Deployment (Go Live)       | main                          |

All developer unit testing are done on the local/Cloud IDE. See [Setting development environment](#dbt_project_input_local_development)

### Credentials <a name="dbt_project_cd_credentials"></a>

The [dbt_runner](https://sbd-ddbot.atlassian.net/wiki/spaces/CAS/pages/2202861577/dbt+Runner) in Caspian TMC uses [Credentials Vaulting Framework](https://sbd-ddbot.atlassian.net/wiki/spaces/CAS/pages/311099432/Caspian+Credentials+Vaulting) to store credentials for various projects. dbt_runner needs two main credentials to run. The following credentials are used to run this project across all Caspian Environments

| **\\**                            | **DEV**                 | **TEST**                 | **PROD**                 |
|---------------------------------|-------------------------|--------------------------|--------------------------|
| Caspian_SNOWFLAKE_CredVaultKey  | `dev/snowflake/mart/gods` | `test/snowflake/mart/gods` | `prod/snowflake/mart/gods` |
| Caspian_BUGTRACKER_CredVaultKey | N/A-Applicable          | N/A-Applicable               |sbd/caspian/prod/operations/alerts/caspian_bug_tracker_service

 |


### Alerts <a name="dbt_project_cd_alerts"></a>
The dbt_runner template has a notification/alerting mechanism incase of any WARNING, ERROR or FATAL messages. To configure notification in dbt_runner for this project;

1. In the advanced parameter `Email_Notify` parameter, provide the value `true`
2. In the advanced parameter `Caspian_BUGTRACKER_CredVaultKey` parameter, provide a valid credential key provided by the Caspian platform team. See the values to use per environment in [above section](#dbt_project_cd_credentials)


### Job Names <a name="dbt_project_cd_job_names"></a>
The following is a list of dbt_runner tasks needed to run this mart successfully end to end

| **JOB_NAME**                           | **JOB_DESCRIPTION**                          | **JOB_RUN_PARAMETERS** | **NOTES** |
|----------------------------------------|----------------------------------------------|------------------------|-----------|
|DBT_RUNNER-MARTS_GODS-INIT_PROJECT 		| 			 | `dbt run-operation create_tables --vars '{"env":"PROD"}'` |One time run on migration      |
|DBT_RUNNER-MARTS-GODS-SEED_STATIC_FILES 	| Loads static tables from CSV files           | `dbt seed --full-refresh` |One time run on migration      |
|DBT_RUNNER-MARTS-GODS_PROCS_EXECUTE 		|                           | `dbt run --vars '{"env":"PROD"}'` |Scheduled on daily basis       |
|DBT_RUNNER-MARTS-GODS						|	Populates DM tables		| `dbt run --vars '{"env":"PROD"}'` |Scheduled on daily basis       |


### Plan Names <a name="dbt_project_cd_plan_names"></a>
The following is a list of plan needed to run this mart successfully end to end

| **PLAN_NAME**                           | **JOBS**                          			 | **NOTES** |
|---------------------------------------- |----------------------------------------------|------------------------|
|MART-GODS 		| DBT_RUNNER-MARTS-GODS_PROCS_EXECUTE, DBT_RUNNER-MARTS-GODS	|	Scheduled on daily basis      |
### Adhoc Runs

#### (Re-)Loading seeded files <a name="dbt_howtorun_seed"></a>

Incase of changes to the static files that hosted within the dbt project in the `data` or `seeds` folder (varies with the project as specified by the seed-paths config in *dbt_project.yml*)
Below steps should be followed to reload the seeded data once this project has been deployed to PRODUCTION.
1. Create a new feature branch from main
2. Checkout feature branch to IDE
3. Replace the existing files in the data/ref_data_seeds folder.
4. Commit the changes to seed files and push to remote feature branch
5. Create a Pull Request from feature branch to main
6. Merge the feature branch into main
7. Run the TMC Task `DBT_RUNNER-MARTS-GODS-SEED_STATIC_FILES` to refresh the static seeded data for GODS.
    - If no new files are provided but Seed data has to be refreshed, then only Run the TMC Task `DBT_RUNNER-MARTS-GODS-SEED_STATIC_FILES`

##### (Re-)Loading static S3 files <a name="dbt_howtorun_seed"></a>

Incase of changes to the static files that hosted within Caspian S3 folders
Below steps should be followed to reload the snowflake data once this project has been deployed to PRODUCTION.
1. Load the new files to S3 production bucket: check in `macros/init_project.sql` for precise S3 data locations.
2. Run the TMC Task `DBT_RUNNER-MARTS_GODS-INIT_PROJECT` to refresh the Ref Data for UMM_NA.
    - If no new files are provided but Seed data has to be refreshed, then only Run the TMC Task `DBT_RUNNER-MARTS_GODS-INIT_PROJECT`

### Orchestration <a name="dbt_project_cd_orchestration"></a>

To run this project end to end, the following diagram illustrates all the steps and dependencies and their orchestration flow


# Support Team Structure <a name="dbt_project_support_team_structure"></a>

Below is the support team structure for this project:

| **Team**       | **Contact Information** |
|----------------|-------------------------|
| Build Team     | EON Collective - Snowflake Migration project |
| Run Team       | caspianrunteam@sbdinc.com                        |
| Source Team    |                         |
| Consumer Team  |                         |

# Service Level Agreements (SLA) <a name="dbt_project_sla"></a>

This project utilizes the following SLA schedule.

| **PRIORITY LEVEL** | **TARGET RESPONSE TIME** | **TARGET RESOLUTION TIME** | **SLA CLOCK** |
|--------------------|--------------------------|----------------------------|---------------|
| 1 - Critical       | 30 Minutes               | 4 Hours                    | 24 x 7        |
| 2 - High           | 40 Hours                 | 1 Business Day             | In Region     |
| 3 - Medium         | N/A                      | 5 Business Days            | In Region     |
| 4 - Low            | N/A                      | 10 Business Days           | In Region     |

# Troubleshoot/ F.A.Q <a name="dbt_troubleshoot"></a>

## Known Issues <a name="dbt_troubleshoot_known_issues"></a>

## Debugging <a name="dbt_troubleshoot_debugging"></a>
1. [See dbt docs on Debugging errors](https://docs.getdbt.com/docs/guides/debugging-errors#general-process-of-debugging) - this has a comprehensive list and categorization of common errors seen on a typical dbt project. Note the [common pitfalls section](https://docs.getdbt.com/docs/guides/debugging-errors#common-pitfalls) also


# Migration Notes <a name="dbt_project_migration_notes"></a>

During the migration of this project/mart from Redshift to snowflake, the following elements may have been changed to accomodate the lift and shift of this project to Snowflake.

The following tables cannot be found in Snowflake and need to be migrated as one time static tables into Snowflake. 

- consolidated_entity_c11
- consolidated_salesorg_enthierachy
- dim_calendar
- dim_factory_calendar
- gods_filter
- plant_regions

The unload statements from Redshift to Snowflake can be found under the analysis folder with the name `redshift_unload_to_s3.sql`

# Resources<aname="resources-"><a>                                                                  

- Learn more about dbt [in the docs](https://docs.getdbt.com/docs/introduction)
- Check out [Discourse](https://discourse.getdbt.com/) for commonly asked questions and answers
- Join the [chat](http://slack.getdbt.com/) on Slack for live discussions and support
- Find [dbt events](https://events.getdbt.com) near you
- Check out [the blog](https://blog.getdbt.com/) for the latest news on dbt's development and best practices
- https://www.data-vault.co.uk/what-is-data-vault/                     
- https://www.talend.com/resources/what-is-the-data-vault/                        
- https://community.snowflake.com/s/article/Snowflake-Data-Vault-Reference-Architecture                
- https://gtoonstra.github.io/etl-with-airflow/datavault2.html                                
- https://danlinstedt.com/allposts/datavaultcat/data-vault-and-staging-area/                
- https://datavaultalliance.com/news/dv/source-system-datavault-and-business-keys/                                                        
- https://books.google.com/books?id=lgDJBAAAQBAJ&pg=PA426&lpg=PA426&dq=md5+coalesce+hashdiff&source=bl&ots=VZTADrHXqv&sig=ACfU3U029TiPRf9HX-q-Y-ydRiaUEnDOWg&hl=en&sa=X&ved=2ahUKEwjqlLXlq_LlAhUJd98KHWOoDHUQ6AEwAHoECAkQAQ#v=onepage&q=md5%20coalesce%20hashdiff&f=false

# Cutover Plan
<!---
This checklist is mostly useful as a reminder of small things that can easily be
forgotten â€“ it is meant as a helpful tool rather than hoops to jump through.
Put an `x` in all the items that apply, make notes next to any that haven't been
addressed, and remove any items that are not relevant to this cut over plan.
-->

- [X] CREDENTIALS: snowflake Credvault Key is available in environment AWS account - Adarsh - [07/11/2022]
- [X] CREDENTIALS: IAM role used in talend remote engine is provisioned to have access to Snowflake Credvault Key - Adarsh - [07/11/2022]
- [X] SNOWFLAKE_ROLE: Assigned user and role has the following priviledges: NOTE: execute the following `ALTER USER PROD_MART_OITF SET DEFAULT_ROLE = 'PROD_MARTBUILD_RW';` and `ALTER USER PROD_MART_OITF SET DEFAULT_WAREHOUSE = 'PROD_MART_WH` - Adarsh - [07/11/2022]
	1. Read access to RAW layer tables
	2. Read + Write Access to MARTS.GODS schema
	3. User should have the role role as `PROD_MARTBUILD_RW`
	4. User should have a default warehouse assigned as `PROD_MART_WH`
- [X] Make sure feature branch is using prod locations - Adarsh - [07/11/2022]
- [X] Ensure Static files in sandbox landingzone are copied to PROD landingzone - Adarsh - [07/11/2022]
- [ ] TMC Tasks created - use TEST TMC plan as a base. TMC tasks should use the feature branch for intial run.
- [ ] Create schema by executing the init_project.sql model: s3 staged files are loaded.
- [ ] Run seed task
- [ ] Run GODS mart build
- [ ] Validate data mart run
- [ ] PR merge of feature to main - delete source branch
- [ ] Change tasks to use main branch
- [ ] Schedule


