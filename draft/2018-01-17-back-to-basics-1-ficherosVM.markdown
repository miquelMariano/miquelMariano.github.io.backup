---
title: Back-to-basics 1 - Ficheros de una VM
date: '2018-01-17 00:00:00'
layout: post
image: /assets/images/posts/2017/11/vmfiles1.png
headerImage: true
tag:
- vmware
- vsphere
- vexpert
- devops
- backtobasics
category: blog
author: miquelMariano
description: Back-to-basics 1 - Ficheros de una VM
hidden: false
permalink: /basics1/
---

Buenos dias a tod@as!!

En esta [serie que voy a empezar](https://miquelmariano.github.io/tags/#backtobasics), me gustaría dar un repaso a los principales conceptos y aspectos que hay que tener en cuenta en un entorno vSphere.

En este primer post, vamos a recordar los diferentes ficheros que conforman una Máquina Virtual y para que sirven.

# Archivos que conforman una VM

![vmfiles]({{ site.imagesposts2017 }}/11/vmfiles.jpg)

Los archivos que conforman una Máquina Virtual, generalmente, residen dentro de la carpeta (nombre de su VM) colocada en un datastore. Los archivos presentes en esta carpeta dependerán del estado en el que se encuentre la VM (Encendido / Apagado / Suspendido) y la acción que se está realizando en un momento determinado.

+ VMX file – Configuración
+ VMDK files – Ficheros relacionados con los discos de datos, incluye .vmdk, -delta.vmdk, -rdm.vmds
+ VSWP file – Memory overflow. Fichero SWAP
+ VMSD file – Detalles de snapshot
+ VMSS file – Contenido de memoria RAM en una VM suspendida
+ VMSN file – Fichero de snapshot
+ NVRAM file – Fichero de BIOS
+ Log files

# VMX file

El fichero de configuración de una máquina virtual contiene todos los detalles para que la VM pueda arrancar. Información del Virtual Hardware, SO, Networking, Almacenamiento, ...

Cada vez que creamos una VM, el fichero .vmx aparece automaticamente y contiene la información de todas las configuraciones que hemos ido perfilando durante el wizard de creación

# VMDK Files




http://blog.kanishksethi.in/2016/04/back-to-basics-virtual-machine-files.html

http://www.on-cloud9.com/2012/01/16/virtual_machine_files_explained/

..


Un saludo!

Miquel.


