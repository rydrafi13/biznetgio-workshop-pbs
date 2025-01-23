# biznetgio-workshop-pbs
Documentation Lab Biznetgio PBS Workshop

## Preparation Server
Access to VM Debian via ssh for linux os host
```
ssh -l debian 103.x.x.x -i name-xxx.key
```

Access to VM Debian via putty/mobaxterm for windows os host
```
https://kb.biznetgio.com/id_ID/informasi/cara-akses-instance-neo-cloud-melalui-putty
```

login as super user
```
sudo su
```

set hostname
```
hostnamectl set-hostname pbs-xxx
```

set timezone
```
timedatectl set-timezone Asia/Jakarta
```

Update and Upgrade package
```
apt update -y && apt upgrade -y
```

Create credentials for login debian
```
passwd debian
```

## Installation Proxmox Backup Server
login as super user
```
sudo su
```

Create debian package repository 
```
nano /etc/apt/sources.list.d/pbs-server.list
```

/etc/apt/sources.list.d/pbs-server.list
```
# debian 12 package
deb http://deb.debian.org/debian bookworm main contrib
deb http://deb.debian.org/debian bookworm-updates main contrib

# Proxmox Backup Server pbs-no-subscription repository provided by proxmox.com,
deb http://download.proxmox.com/debian/pbs bookworm pbs-no-subscription

# security updates
deb http://security.debian.org/debian-security bookworm-security main contrib
```

Install key
```
wget https://enterprise.proxmox.com/debian/proxmox-release-bookworm.gpg -O /etc/apt/trusted.gpg.d/proxmox-release-bookworm.gpg
```

Update repository
```
apt update
```

Update debian 12
```
apt upgrade
```

Install package proxmox-backup-server
```
apt install proxmox-backup-server
```

Check service proxmox-backup
```
systemctl status proxmox-backup
```

Check listen port proxmox-backup
```
ss -tulpn
```

Create password for root user
```
passwd root
```

Restart VM
```
reboot
```

Access from browser to pbs
```
https://103.x.x.x:8007
```

Proxmox Backup Server Dashboard
<img src="images/pbs-dashboard.png" alt="proxmox backup server dashboard"/>

## Proxmox Backup Server Administration

### Disk Management
Disk Management Menu
<img src="images/pbs-disk-management.png" alt="proxmox backup server disk management"/>

Create Datastore
<img src="images/pbs-create-datastore.png" alt="proxmox backup server create datastore"/>

Verify Datastore
<img src="images/pbs-datastore.png" alt="proxmox backup server datastore"/>

Create Backup Namespace
<img src="images/pbs-backup-namespace.png" alt="proxmox backup server backup namespace"/>

### User Management
User Management Menu
<img src="images/pbs-user-management.png" alt="proxmox backup server user management"/>

Create User Configuration
<img src="images/pbs-user-configuration.png" alt="proxmox backup server user configuration"/>

Create Access Control to User
<img src="images/pbs-access-control.png" alt="proxmox backup server access control"/>

Verify login with new user
<img src="images/pbs-login-admin.png" alt="proxmox backup server login admin"/>

## Proxmox VE Integration
### Integration
Login PVE
<img src="images/pve-login.png" alt="proxmox ve login"/>

PVE dashboard
<img src="images/pve-dashboard.png" alt="proxmox ve dashboard"/>

Add new storage with Proxmox Backup Server type
<img src="images/pve-storage-type.png" alt="proxmox ve storage type"/>

Fill the credentials to Proxmox Backup Server login
<img src="images/pve-add-storage.png" alt="proxmox ve add storage"/>

Check storage
<img src="images/pve-pbs-integration.png" alt="proxmox ve and pbs integration"/>

### Test Backup 1
Access to VM on PVE
<img src="images/pve-vm.png" alt="proxmox vm"/>

Create sample folder and file
<img src="images/pve-create-file.png" alt="proxmox ve create folder and file"/>

Test Backup Scenario
<img src="images/pve-backup.png" alt="proxmox ve backup scenario"/>

Verify Backup Status
<img src="images/pve-completed-backup.png" alt="proxmox ve completed backup"/>

Verify Backup
<img src="images/pve-backup-status.png" alt="proxmox ve backup status"/>

Verify Backup Content
<img src="images/pbs-backup-content.png" alt="pbs backup content"/>

Verify usage datastore
<img src="images/pbs-datastore-dashboard.png" alt="pbs datastore dashboard"/>

### Test Backup 2
Access to VM on PVE
<img src="images/pve-vm.png" alt="proxmox vm"/>

Test create 2gb file size
<img src="images/pve-fallocate.png" alt="proxmox ve create file 2G"/>

Test Backup Scenario
<img src="images/pve-backup.png" alt="proxmox ve backup scenario"/>

Verify Backup Status
<img src="images/pve-backup-completed-2.png" alt="proxmox ve completed backup"/>

Verify Backup
<img src="images/pve-backup-status-2.png" alt="proxmox ve backup status"/>

Verify Backup Content
<img src="images/pbs-backup-content-2.png" alt="proxmox ve backup status"/>

Verify usage datastore
<img src="images/pbs-datastore-dashboard-2.png" alt="pbs datastore dashboard"/>

### Test Restore
Access to VM on PVE
<img src="images/pve-vm.png" alt="proxmox vm"/>

Delete sample folder and file
<img src="images/pve-vm-delete.png" alt="proxmox vm delete data"/>

Shutdown/Stop VM
<img src="images/pve-vm-stop.png" alt="proxmox vm stop"/>

Test restore Scenario
<img src="images/pve-vm-restore.png" alt="proxmox vm restore data"/>

Restore completed
<img src="images/pve-restore-status.png" alt="proxmox vm restore progress"/>

Verify VM
<img src="images/pve-vm-restore-2.png" alt="proxmox vm restore vm"/>

### Set schedule backup
Add new schedule backup
<img src="images/pve-schedule-backup.png" alt="proxmox ve schedule backup"/>

## Proxmox Backup Server Maintenance
Prune and GC Menu
<img src="images/pbs-prune-gc-menu.png" alt="proxmox backup server menu"/>

### Prunning
Set prune jobs
<img src="images/pbs-prune-jobs.png" alt="proxmox backup server prune jobs"/>

### Garbage Collect
Set garbage collect schedule
<img src="images/pbs-gc-schedule.png" alt="proxmox backup server gc schedule"/>
