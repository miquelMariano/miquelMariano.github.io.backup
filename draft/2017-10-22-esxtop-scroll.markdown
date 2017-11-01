---
title: Limitando nuestra vista sin necesidad de scroll para nuestra salida ESXTOP
date: '2017-09-22 00:00:00'
layout: post
image: /assets/images/posts/2017/08/vcenter-backup.png
headerImage: true
tag:
- vmware
- vexpert
- vCenter
- VCSA
- VMFS
category: blog
author: miquelMariano
description: Limitando nuestra vista sin necesidad de scroll para nuestra salida ESXTOP
hidden: false
permalink: /scroll/
---

http://www.vmwarearena.com/esxtop-limiting-your-view-no-need-to-scrollpagedown-your-esxtop-output/


Muy buenos dias a tod@as, en el post de hoy os voy a mostrar una pequeña funcionalidad que tiene el comando esxtop y que me ha sido de mucha ayuda en mas de una ocasión.



```ssh
esxtop -export-entity /tmp/limited-view
```

```ssh
vi /tmp/limited-view
```

En este caso concreto, tenia una lista demasiado extensa de datastores, por lo que ncesitba filtrar y mostrar solo los discos que a mi me interesaban en ese momento, así que simplemente comentando (#) las lineas puedo "ocultar" información irrelevante.

```ssh
...
Adapter
vmhba2
vmhba3
vmhba32

Device
#naa.60060e8012ad9c005040ad9c000030f0
#naa.60060e8012ad9c005040ad9c000030f3
naa.60060e8012ad9c005040ad9c00000010
naa.60060e8012ad9c005040ad9c00000011
naa.60060e8012ad9c005040ad9c00000012
naa.60060e8012ad9c005040ad9c00000013
naa.60060e8012ad9c005040ad9c00000014
naa.60060e8012ad9c005040ad9c00000015
naa.60060e8012ad9c005040ad9c00000016
#naa.60060e8012ad9c005040ad9c00002013
#naa.60060e8012ad9c005040ad9c00002014
#naa.60060e8012ad9c005040ad9c00002015
#naa.60060e8012ad9c005040ad9c00002016
#naa.60060e8022155e005041155e00003e00
naa.60060e8012ad9c005040ad9c00000000
#naa.60060e8022155e005041155e00003e01
naa.60060e8012ad9c005040ad9c00000001
naa.60060e8012ad9c005040ad9c00000002
naa.60060e8012ad9c005040ad9c00000003
naa.60060e8012ad9c005040ad9c00000004
naa.60060e8012ad9c005040ad9c00000005
naa.60060e8012ad9c005040ad9c00000006
naa.60060e8012ad9c005040ad9c00000007
naa.60060e8012ad9c005040ad9c00000008
naa.60060e8012ad9c005040ad9c00000009
#naa.60060e8012ad9c005040ad9c00002025
#naa.60060e8012ad9c005040ad9c00002026
#naa.60060e8012ad9c005040ad9c00002027
#naa.60060e8012ad9c005040ad9c00002028
#naa.60060e8012ad9c005040ad9c00002029

NetPort
33554433 Management
33554434 vmnic0
33554435 Shadow of vmnic0
33554436 vmnic1
...
```


```ssh
esxtop -import-entity /tmp/limited-view
```


Vista de "disk device" pulsando "u"

```ssh
  P:  VAAILATSTATS/cmd = VAAI Latency Stats (ms)

Toggle fields with a-p, any other key to return:
12:49:54am up 36 days  9:37, 1110 worlds, 6 VMs, 58 vCPUs; CPU load average: 0.27, 0.27, 0.27

DEVICE                               CLONE_RD CLONE_WR  CLONE_F MBC_RD/s MBC_WR/s      ATS ATSF     ZERO   ZERO_F MBZERO/s   DELETE DELETE_F  MBDEL
mpx.vmhba32:C0:T0:L0                        0        0        0     0.00     0.00        0    0        0        0     0.00        0        0     0.
naa.60060e8012ad9c005040ad9c00000000        0        0        0     0.00     0.00  1007140 6213      532        0     0.00        0        0     0.
naa.60060e8012ad9c005040ad9c00000001        0        0        0     0.00     0.00    70729   14        2        0     0.00        0        0     0.
naa.60060e8012ad9c005040ad9c00000002        0        0        0     0.00     0.00    70528   17        0        0     0.00        0        0     0.
naa.60060e8012ad9c005040ad9c00000003        0        0        0     0.00     0.00    70533   25        1        0     0.00        0        0     0.
naa.60060e8012ad9c005040ad9c00000004        0        0        0     0.00     0.00    71009   22        2        0     0.00        0        0     0.
naa.60060e8012ad9c005040ad9c00000005        0        0        0     0.00     0.00    71504   26        5        0     0.00        0        0     0.
naa.60060e8012ad9c005040ad9c00000006        0        0        0     0.00     0.00    70943   17        2        0     0.00        0        0     0.
naa.60060e8012ad9c005040ad9c00000007        0        0        0     0.00     0.00    71178   47        3        0     0.00        0        0     0.
naa.60060e8012ad9c005040ad9c00000008        0        0        0     0.00     0.00    71042   24        1        0     0.00        0        0     0.
naa.60060e8012ad9c005040ad9c00000009        0        0        0     0.00     0.00    71145   25        3        0     0.00        0        0     0.
naa.60060e8012ad9c005040ad9c00000010        0        0        0     0.00     0.00  3566321 4771        0        0     0.00        0        0     0.
```

Un saludo!

Miquel.


