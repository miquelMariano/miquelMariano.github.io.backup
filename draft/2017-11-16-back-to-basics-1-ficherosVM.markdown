---
title: Back-to-basics 1 - Ficheros de una VM
date: '2017-11-16 00:00:00'
layout: post
image: /assets/images/posts/2017/11/vmfiles1.png
headerImage: true
tag:
- Ansible
- devops
- automation
category: blog
author: miquelMariano
description: Back-to-basics 1 - Ficheros de una VM
hidden: false
permalink: /basics1/
---

Buenos dias a tod@as!!

En esta serie que voy a empezar, me gustaría dar un repaso a los principales conceptos y aspectos que hay que tener en cuenta en un entorno vSphere.

En este primer post, vamos a recordar los diferentes ficheros conforman una Máquina Virtual y para que sirven.

![vmfiles]({{ site.imagesposts2017 }}/11/vmfiles.jpg)

# Archivos que conforman una VM

Los archivos que conforman una Máquina Virtual, generalmente, residen dentro de la carpeta (nombre de su VM) colocada en un datastore. Los archivos presentes en esta carpeta dependerán del estado en el que se encuentre la VM (Encendido / Apagado / Suspendido) y la acción que se está realizando en un momento determinado.

VMX file – Configuración
VMXF file – Configuración suplementeria
VMDK Files – Ficheros relacionados con los discos de datos, incluye .vmdk, -delta.vmdk, -rdm.vmds
VSWP File – Memory overflow. Fichero SWAP
VMSD File – Detalles de snapshot
VMSS File – Contenido de memoria RAM en una VM suspendida
VMSN File – Fichero de snapshot
NVRAM File – Fichero de BIOS
Log files

http://blog.kanishksethi.in/2016/04/back-to-basics-virtual-machine-files.html

http://www.on-cloud9.com/2012/01/16/virtual_machine_files_explained/

..


Un saludo!

Miquel.


