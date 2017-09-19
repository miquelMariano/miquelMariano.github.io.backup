---
title: Error al eliminar fichero de datastore VMFS
date: '2017-09-22 00:00:00'
layout: post
image: /assets/images/posts/2017/08/vcenter-backup.png
headerImage: false
tag:
- vmware
- vexpert
- vCenter
- VCSA
- VMFS
category: blog
author: miquelMariano
description: Error al eliminar fichero de datastore VMFS
hidden: false
permalink: /cannotdeletefile/
---

Buenos dias a tod@as!!

Os habrá pasado alguna vez intentar eliminar una VM de un datastore y encontraros con el siguiente error:

![img1]({{ site.imagesposts2017 }}/09/cannot-delete1.png)

Incluso intentar eliminarlo por ssh directamente desde el ESXi:

```ssh
/vmfs/volumes/57b321fa-349912dc-bc05-90b11c3dbf06/AD_replica # rm todelete-flat.vmdk
rm: can't remove 'todelete-flat.vmdk': Device or resource busy
```




Un saludo!

Miquel.

http://tomaskalabis.com/wordpress/vmware-esxi-cannot-delete-file/


