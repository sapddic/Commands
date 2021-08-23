# Suse-Info



##### Option1:

 Login to SAPVHECPDB2

-  crm configure property maintenance-mode=true

- crm status (all services should be in unmanaged status)

  HDB stop


Systems team takes node2  down  and  once server is back online

- crm configure property maintenance-mode=false

  

  perform below checks to check cluster health



- sbd -d /dev/sdg list
- crm cluster status
- crm status
- SAPHanaSR-showAttr (check lpt value)
- HDBSettings.sh systemReplicationStatus.py

##### Option2:

 Login to SAPVHECPDB2
 crm -w node standby sapvhecpdb2
 crm cluster stop
 systems team takes node2  down  and  once server is back online
 crm node online sapvhecpdb2
 perform below checks to check cluster health
•	 sbd -d /dev/sdg list
•	 crm cluster status
•	 crm status
•	 SAPHanaSR-showAttr (check lpt value)
•	 HDBSettings.sh systemReplicationStatus.py