## Enable and disable maintenance mode whole cluster :

### Login to Node2

```sh
- crm configure property maintenance-mode=true
- crm status (all services should be in unmanaged status)
- HDB stop
```

### Systems team takes node2 down and once server is back online

```sh
- crm configure property maintenance-mode=false
```

### Perform below checks to check cluster health

```sh
- sbd -d /dev/sdg list
- crm cluster status
- crm status
- SAPHanaSR-showAttr (check lpt value)
- HDBSettings.sh systemReplicationStatus.py
```

## Enable and disable maintenance mode single node ( Migrate services) :

### Login to Node2

```sh
- crm -w node standby Node2
- crm cluster stop
```

### Systems team takes node2 down and once server is back online

```sh
- crm node online Node2
```

### Perform below checks to check cluster health

```sh
- sbd -d /dev/sdg list
- crm cluster status
- crm status
- SAPHanaSR-showAttr (check lpt value)
- HDBSettings.sh systemReplicationStatus.py
```
