### SUM DoC notes

------

![image-20210914125140779](HANA%20SUM%20DoC.assets/image-20210914125140779-16316455039875.png)



[1616401 - Parallelism in the Upgrades, EhPs and Support Packages implementations](https://launchpad.support.sap.com/#/notes/1616401)



- R3Loads 3 to 5 times the number of CPUs, being "5" the theorical top limit.(1000 to 2500 R3loads) **EU_IMPORT\*** (in system releases upgrade) and in **DMO** (**data migration option**) scenarios
- SQL  1:1 -  DDL "create table", "alter table", "create index"  , MVNTAB and PARCONV
- **WP** - DBCLONE (10 - in update scenarios), ACT_UPG -6 and PARDIST -10 in uptime, and XPRAs in downtime
- R3trans 1:1
  - DDIC_UPG, SHADOW_IMPORT* and TABIM_UPG
  - SAP Note [1127194 ](https://launchpad.support.sap.com/#/notes/1127194)**"R3trans import with parallel processes**
  - ACC_IMPORT - note #[1223360](https://launchpad.support.sap.com/#/notes/1223360)



![image-20210921123527834](HANA%20SUM%20DoC.assets/image-20210921123527834.png)

-----

[2351294 - S/4HANA System Conversion / Upgrade: Measures to reduce technical downtime](https://launchpad.support.sap.com/#/notes/2351294)

- As of S/4HANA 1709, many of the data conversion methods are using a common parallelization framework. Therefore, the configuration has also been harmonized for all data conversion methods using parallel tasks. The configuration is stored in table SHDB_PFW_CONF and can be preset / adjusted via transaction SE16 or an SQL command line. A suitable point in time to perform this configuration is just before entering the technical downtime, e.g. when SUM reaches phase CHECK4NOTES_TOOL_SHD2

- **Measures specific to HANA**

  - [mergedog] -> load_balancing_func value to “LCC / 2”
  - [mergedog] -> token_per_table
  - [indexing] -> parallel_merge_threads 
  -  [indexing] -> parallel_merge_part_threads
  - [sql] -> multistore_feature_toggle to value (multistore_operator,column,update,false)
  - [2222250 - FAQ: SAP HANA Workload Management](https://launchpad.support.sap.com/#/notes/2222250)
  - Table logging

- **Measures specific to AS ABAP (Upgrade Instance)** - DIA to 20 or more based on the resoruces available

- **Measures specific to SUM**

  - "HANA Table properties" Per default all standard SAP application tables should have AUTO_MERGE_ON as well as AUTO_OPTIMIZE_COMPRESSION_ON enabled (true). 

  - - SELECT TABLE_NAME, AUTO_MERGE_ON, AUTO_OPTIMIZE_COMPRESSION_ON FROM TABLES WHERE AUTO_MERGE_ON = 'FALSE' OR AUTO_OPTIMIZE_COMPRESSION_ON = 'FALSE'﻿
    - ﻿ALTER TABLE "<schema>"."<table>" ENABLE AUTOMERGE; ALTER TABLE "<schema>"."<table>" WITH PARAMETERS ('AUTO_OPTIMIZE_COMPRESSION' = 'ON')﻿

- **Observe and manage available system resources**

  Most of the measures described above are around configuring an appropriate number of parallel tasks. If doing so, you should monitor both your SAP (on OS level) and HANA database (on OS level or SAP HANA Cockpit) systems for CPU, disk I/O activity and memory consumption.

  In case of underutilization < 60% for more than a minute, increase the number of parallel tasks 

  In case of very high CPU usage and/or disk activity > 85% for more than a minute),and high wait time 10% for min

  For monitor use the visual load history of the HANA cockpit, or the relevant monitoring views such as **M_SERVICE_MEMORY or M_HEAP_MEMORY**.

[2778832 - XCLA Uptime Procedure for Downtime-Optimized conversion Scenario](https://launchpad.support.sap.com/#/notes/2778832) - # defines the approach of how to manage the XCLA based on previous runtime , optimation is explanind in # **2351294**



![CRR for Migration and Upgrade](HANA%20SUM%20DoC.assets/CRR%20for%20Migration%20and%20Upgrade-16322447949171.png)



[3049338 - Executing and Monitoring Downtime-Optimized Conversion to SAP S/4HANA with SUM 2.0 SP 11](https://launchpad.support.sap.com/#/notes/3049338)







​	

