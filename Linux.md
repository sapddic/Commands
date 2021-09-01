##	Systems Maintenance

```sh
useradd -d /home/kothapra -c "test ssh key pair" -s /bin/bash

ls -ltr | awk '$6 == "May" && $7 >=01 && $7 <= 31 {print $6"-"$7,$9}'
ls -ltr | awk '$6 == "Jul" && $7 = 26 {print $9}'

find . -type f -mtime +2  -exec rm {} \;
find . -type f -mtime +1  -exec ll {} \;

ls -al --time-style=+%D | grep $(date +%D)

nohup scp -rp ECP_TenantBackup hdqadm@SAPVHEC2DB:/backup/DONTDELETE_LOG_BACKUP/TSTBKP

echo "Hello World" | mail -s " Subject" rajeshwarkothapalli@gmail.com


ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head

echo $(date +"%F_%k_%M")

su -ndbadm -c "/usr/sap/NDB/HDB00/exe/hdbcons mm gc -f”

scp -pr `find . -type f -mtime 3` bdradm@SAPVHBDRDB1:/backup/DONTDELETE_LOG_BACKUP/SYSTEMDB

mount -t cifs -o username=sapadm //10.1.152.27/share/2020_BSoH/Software /backup/Media
cd /backup/Media/HANA_2.0SP04_DUMP/51053787_HANA2.0SP04/DATA_UNITS/HDB_LCM_LINUX_X86_64

hostip=10.1.152.55 gateway=10.1.152.1  netmask=255.255.255.0 install=http://10.1.148.115 autoyast=http://10.1.148.115/autoinst_staticip.xml

hostname=SAPVHBDRDB2 hostip=10.1.152.56/24 gateway=10.1.152.1 install=http://10.1.148.115 autoyast=http://10.1.148.115/autoinst_staticip.xml

hostname=SAPVHBDRDB2 hostip=10.1.152.56/24 gateway=10.1.152.1 install=http://10.1.148.115
```



## NFS Server

```sh
# NFS server installation and mount work

To restart NFS Service:
rcnfsserver restart

To restart NFS Client:
rcnfs restart

zypper install nfs-kernel-server
systemctl enable --now nfsserver.service
/usr/lib/systemd/system/nfsserver.service

vi /etc/exports
echo "/backup 10.1.146.66(rw,sync)" | cat >> /etc/exports
echo "/backup 10.1.146.67(rw,sync)" | cat >> /etc/exports
echo "/backup 10.1.152.14(rw,sync)" | cat >> /etc/exports

systemctl reload nfsserver.service
showmount -e

mount -l 
cat /etc/mtab
umount -l /backup-bdr-nfs

mkdir /backup-pop-nfs
mkdir /backup-scp-nfs
mkdir /backup-ecp-nfs

permissions 
chmod 775 /backup
chown hdqadm:sapsys /backup
mkdir -p /backup/DONTDELETE_LOG_BACKUP
mkdir -p /backup/DB13_BACKUP

configure nfsclient 
yast2 nfs &

```