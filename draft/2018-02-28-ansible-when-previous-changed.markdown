---
title: Back-to-basics 2 - Licenciemiento vSphere
date: '2018-02-28 00:00:00'
layout: post
image: /assets/images/posts/2018/02/logovsphere65.jpeg
headerImage: true
tag:
- vmware
- vsphere
- vexpert
- devops
- backtobasics
category: blog
author: miquelMariano
description: Back-to-basics 2 - Licenciamiento vSphere
hidden: false
permalink: /changed/
---

https://raymii.org/s/tutorials/Ansible_-_Only-do-something-if-another-action-changed.html


```yaml
- hosts: "{{ servers }}:!localhost"
  user: root
  serial: 1
  tasks:
     - name: Replace vpxa log level
       replace:
          path: /etc/vmware/vpxa/vpxa.cfg
          regexp: '<level>verbose</level>'
          replace: '<level>info</level>'
          backup: yes
       register: replace_status

     - name: Restart vpxa agent
       shell: /etc/init.d/vpxa restart
       when: replace_status.changed
```

Buenos dias a tod@as!!

En esta segunda entrada de la serie [back-to-basics](https://miquelmariano.github.io/tags/#backtobasics), me gustaria dar un repaso al licenciamiento vSphere



# Licencias enterprise

![enterprise]({{ site.imagesposts2018 }}/02/enterprise.png)

# Kit Essentials

Los paquetes de VMware vSphere 6 Essentials y VMware vSphere 6 Essentials Plus se deben considerar por separado. Han sido diseñados específicamente para pequeñas empresas y pueden virtualizar hasta tres servidores físicos. La administración central de estos servidores solo es posible a través de vCenter Server for Essentials. vCenter Server Standard, que permite la administración central de cualquier número de servidores host físicos, solo se puede usar con licencias regulares de vSphere con o sin vSOM.

![essentials]({{ site.imagesposts2018 }}/02/essentials.png)

# Acceleration Kit

![acceleration]({{ site.imagesposts2018 }}/02/accelerationkit.png)





Un saludo!

Miquel.


