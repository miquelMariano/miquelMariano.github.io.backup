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
permalink: /basics2/
---

https://www.altaro.com/vmware/a-quick-look-at-vmware-vsphere-editions-and-licensing/

Buenos dias a tod@as!!

Incluso los administradores mas experimentados, a veces, se confunden con las peculiaridades de las licencias vSphere, las opciones disponibles y las características.

En esta segunda entrada de la serie [back-to-basics](https://miquelmariano.github.io/tags/#backtobasics), me gustaria dar un repaso al licenciamiento vSphere. En este caso trataré de explicar las ediciones de VMware vSphere disponibles, sus características, diferencias, en versión 6.5 (lanzado en octubre de 2016).

# Aspectos a tener en cuenta
Resaltemos las reglas principales a tener en cuenta al planear y comprar licencias de VMware vSphere 6.5.

+ Un servidor ESXi debe licenciarse según la cantidad de procesadores físicos (CPU). Cada CPU del servidor requiere una licencia vSphere.
+ La funcionalidad disponible de un servidor ESXi estrá determinada por la licencia de vSphere instalada.
+ Cada licencia de vSphere requiere un paquete de soporte de servicio (al menos por un año).
+ VMware no impone ninguna restricción al tamaño de la memoria (RAM) instalada en el servidor físico ni a la cantidad de máquinas virtuales en ejecución.

# Licencias enterprise

![enterprise]({{ site.imagesposts2018 }}/02/enterprise.png)

# Kit Essentials

Los paquetes de VMware vSphere 6 Essentials y VMware vSphere 6 Essentials Plus se deben considerar por separado. Han sido diseñados específicamente para pequeñas empresas y pueden virtualizar hasta tres servidores físicos. La administración central de estos servidores solo es posible a través de vCenter Server for Essentials. vCenter Server Standard, que permite la administración central de cualquier número de servidores host físicos, solo se puede usar con licencias regulares de vSphere con o sin vSOM.

![essentials]({{ site.imagesposts2018 }}/02/essentials.png)

# Acceleration Kit

![acceleration]({{ site.imagesposts2018 }}/02/accelerationkit.png)





Un saludo!

Miquel.


