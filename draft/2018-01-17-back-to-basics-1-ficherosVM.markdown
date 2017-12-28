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

# Ficheros de configuración

---

+ **vm_name.vmx:**	El fichero de configuración de una máquina virtual contiene todos los detalles para que la VM pueda arrancar. Información del Virtual Hardware, SO, Networking, Almacenamiento, ...
Cada vez que creamos una VM, el fichero .vmx aparece automaticamente y contiene la información de todas las configuraciones que hemos ido perfilando durante el wizard de creación
+ **vm_name.vmtx:** El fichero .vmx se convierte en .vmtx cuanto una VM se convierte a plantilla. Contiene los detalles de configuración de esta VM convertida a plantilla
+ **vm_name.vmxf**	Es un XML que contiene configuración y opciones adicionales de una VM
+ **vm_name.nvram**	Corresponde al fichero de configuración de la BIOS o EFI que utiliza la VM
+ **vm_name.vmss:** Corresponde al fichero del estado suspendido de una VM. Almacena información cuando una VM está en estado “suspended”. Si la VM está en otro estado, este fichero no existe


# Ficheros de disco

---

<vm name>.vmdk	Called the descriptor, this text file contains configuration information about a VM’s virtual hard drive.
<vm name>-flat.vmdk	The virtual equivalent of a physical hard drive, this is where raw data is written to. You won’t find this file listed in Directory Browser. It is instead amalgamated with the descriptor file and presented as a single file.

# Ficheros de Snapshot

---

<vm name>.vmsd	A database containing information about the snapshots taken for a specific virtual machine.
<vm name>-Snapshotn.vmsn	This file captures the VM’s memory state at the time the snapshot is taken regardless of whether the “Snapshot the virtual machine’s memory” option is selected. Starting with 1, n is incremented at every snapshot taken.
<vm name>-00000n-delta.vmdk	A delta vmdk is created whenever a snapshot is taken. The pre-snapshot vmdk in use is locked for writing. Any changes from there on are written to the VM’s delta disk. This allows a VM to be restored to any state prior to a specific snapshot being taken.
<vm name>-00000n.vmdk	The descriptor file for the delta vmdk file.

# Ficheros de Log

---

vmware.log	The current log file for the VM. Useful for troubleshooting operations.
vmware-n.log	Older VM log files where larger values of n correspond to recently written files.

# Otros ficheros

---

<vm name>-ctk.vmdk	This file is created whenever changed block tracking (CBT) is enabled for the VM. CBT is a VMware feature used by incremental backups and leveraged by backup software providers such as Altaro VMBackup.
*.vswp	The VM’s swap file is used to reduce the overhead memory reservation for a VM by swapping out memory to an  ESXi host with over-committed memory.






http://blog.kanishksethi.in/2016/04/back-to-basics-virtual-machine-files.html

http://www.on-cloud9.com/2012/01/16/virtual_machine_files_explained/

..


Un saludo!

Miquel.

