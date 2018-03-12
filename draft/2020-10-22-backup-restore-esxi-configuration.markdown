---
title: Backup & Restore de la configuración de un host ESXi
date: '2017-09-22 00:00:00'
layout: post
image: /assets/images/posts/2018/04/esxi-backup.jpeg
headerImage: true
tag:
- backup
- restore
- esxi
- vexpert
- powercli
category: blog
author: miquelMariano
description: Backup & Restore de la configuración de un host ESXi
hidden: false
permalink: /esxibackup/
---

Buenos dias a tod@as!!

http://buildvirtual.net/using-powercli-to-backup-and-restore-esxi-host-configuration/..

```powershell
Get-VMHostFirmware -VMHost $host -BackupConfiguration -DestinationPath C:\HostBackups
```

```powershell
Set-VMHostFirmware -VMHost $Host -Restore -SourcePath c:\Hostbackups\backupfile.tgz -HostUser user -HostPassword password
```

Un saludo!

Miquel.


