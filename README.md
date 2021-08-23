# Suse-Info



##### Option1:
######Login to Node2
- crm configure property maintenance-mode=true
- crm status (all services should be in unmanaged status)
  HDB stop
######Systems team takes node2  down  and  once server is back online
- crm configure property maintenance-mode=false
######Perform below checks to check cluster health
- sbd -d /dev/sdg list
- crm cluster status
- crm status
- SAPHanaSR-showAttr (check lpt value)
- HDBSettings.sh systemReplicationStatus.py

##### Option1:
######Login to Node2
- crm -w node standby Node2
- crm cluster stop
######systems team takes node2  down  and  once server is back online
- crm node online Node2
######Perform below checks to check cluster health
- sbd -d /dev/sdg list
- crm cluster status
- crm status
- SAPHanaSR-showAttr (check lpt value)
- HDBSettings.sh systemReplicationStatus.py