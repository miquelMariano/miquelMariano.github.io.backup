---
title: Back-to-basics 3 - ESXi logs
date: '2018-02-28 00:00:00'
layout: post
image: /assets/images/posts/2018/03/logs.png
headerImage: true
tag:
- vmware
- vsphere
- vexpert
- devops
- backtobasics
category: blog
author: miquelMariano
description: Back-to-basics 2 - ESXi logs
hidden: false
permalink: /basics3/
---

Buenos dias a tod@as!!

En el post de hoy vamos a ver [donde se encuentran los principales logs de un entorno VMWare](https://kb.vmware.com/s/article/1021806)

Para mí, los mas interesantes son los de un host ESXi, ya que es desde donde podremos extraer la mayor información de lo que está pasando en en entorno. Ahí van los principales logs y donde los encontraremos.

| Componente          | Ubicación                                                                                                                                                                   | Descripción                                                                                                                                                                       |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| VMkernel            | /var/log/vmkernel.log                                                                                                                                                       | Records activities related to virtual machines and ESXi.                                                                                                                          |
| VMkernel warnings   | /var/log/vmkwarning.log                                                                                                                                                     | Records activities related to virtual machines.                                                                                                                                   |
| VMkernel summary    | /var/log/vmksummary.log                                                                                                                                                     | Used to determine uptime and availability statistics for ESXi (comma separated).                                                                                                  |
| ESXi host agent log | /var/log/hostd.log                                                                                                                                                          | Contains information about the agent that manages and configures the ESXi host and its virtual machines.                                                                          |
| vCenter agent log   | /var/log/vpxa.log                                                                                                                                                           | Contains information about the agent that communicates with vCenter Server (if the host is managed by vCenter Server).                                                            |
| Shell log           | /var/log/shell.log                                                                                                                                                          | Contains a record of all commands typed into the ESXi Shell as well as shell events (for example, when the shell was enabled).                                                    |
| Authentication      | /var/log/auth.log                                                                                                                                                           | Contains all events related to authentication for the local system.                                                                                                               |
| System messages     | /var/log/syslog.log                                                                                                                                                         | Contains all general log messages and can be used for troubleshooting. This information was formerly located in the messages log file.                                            |
| Virtual machines    | The same directory as the affected virtual machine's configuration files, named vmware.log and vmware*.log. For example, /vmfs/volumes/datastore/virtual machine/vwmare.log | Contains virtual machine power events, system failure information, tools status and activity, time sync, virtual hardware changes, vMotion migrations, machine clones, and so on. |

Para leerlos, desde una sesión SSH, simplemente tendremos que ejecutar el comando `tail -f nombre\del\log` y en tiempo real veremos como se va actualizando con todo lo que está pasando.

Espero que os pueda ser de utilidad.


Un saludo!

Miquel.


