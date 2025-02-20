# pbs-wrapper
Proxmox Backup Server Wrapper Script for proxmox-backup-client

## Install
### Debian

1) download proxmox backup wrapper:<br>
<code>wget https://raw.githubusercontent.com/adminforge/pbs-wrapper/master/pbs</code>
2) install: <code>sudo bash pbs install</code>
3) edit <code>/etc/.pbs.config</code> and choose PBS_REPOSITORY, PBS_PASSWORD and PBS_FINGERPRINT
4) a daily backup will run every day between 0-5am

## Usage
You can run <code>pbs -h</code> to list wrapper help or <code>pbs</code> to list proxmox-backup-client original help. <p>

### run backup
<pre>
# pbs run
Starting backup: host/pve1/2025-02-20T09:40:50Z    
Client name: pve1    
Starting backup protocol: Thu Feb 20 10:40:50 2025    
Using encryption key from '/root/backup.key'..    
Encryption key fingerprint: 3c:df:0b:fc:61:d0:5d:7b    
Downloading previous manifest (Thu Feb 20 09:42:27 2025)    
Upload directory '/' to 'user@pbs!tokenname@ip:8007:datastore' as root.pxar.didx
  root.pxar: had to backup 186.732 MiB of 6.831 GiB (compressed 41.414 MiB) in 21.07 s (average 8.863 MiB/s)
root.pxar: backup was done incrementally, reused 6.649 GiB (97.3%)
Uploaded backup catalog (1.692 MiB)
Duration: 22.58s    
End Time: Thu Feb 20 10:41:12 2025  
</pre>

### list backups
<pre>
# pbs snapshot list
┌────────────────────────────────┬───────────┬────────────────────────────────────┐
│ snapshot                       │      size │ files                              │
╞════════════════════════════════╪═══════════╪════════════════════════════════════╡
│ host/pve1/2025-02-20T07:42:56Z │ 6.831 GiB │ catalog.pcat1 index.json root.pxar │
├────────────────────────────────┼───────────┼────────────────────────────────────┤
│ host/pve1/2025-02-20T08:42:27Z │ 6.832 GiB │ catalog.pcat1 index.json root.pxar │
├────────────────────────────────┼───────────┼────────────────────────────────────┤
│ host/pve1/2025-02-20T09:40:50Z │ 6.833 GiB │ catalog.pcat1 index.json root.pxar │
└────────────────────────────────┴───────────┴────────────────────────────────────┘
</pre>

### restore complete backup to RESTOREFOLDER="/tmp"
<pre>
# pbs restore host/pve1/2025-02-20T07:42:56Z root.pxar
</pre>

### mount a snapshot
<pre>
# pbs mount host/pve1/2025-02-20T07:42:56Z root.pxar /mnt
</pre>
