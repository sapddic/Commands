### Systems Maintenance

```sh
useradd -d /home/kothapra -c "test ssh key pair" -s /bin/bash
```



### NFS Server

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


```