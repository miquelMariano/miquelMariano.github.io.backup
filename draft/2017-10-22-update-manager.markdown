---
title: Actualización HW virtual y VMWare Tools con vSphere Update Manager
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
description: Actualización HW virtual y VMWare Tools con vSphere Update Manager
hidden: false
permalink: /updatemanager/
---

Buenos dias a tod@as!!!

Introducción
El presente documento pretende servir de guía para la configuración y posterior uso de vSphere Update Manager como herramienta para la actualización de HW Virtual y VMWare Tools en nuestras máquinas virtuales de un entorno vSphere
El procedimiento aplica a entornos con vSphere 6.x y vSphere Web Client

Procedimiento
1.	Iniciar sesión en vCenter a través del vSphere Cient
NOTA: Utilizaremos la etiqueta locale=en_US en caso de querer la interfaz en inglés
https://172.24.0.47/vsphere-client/?locale=en_US

2.	Seleccionamos cualquier objeto de nuestro árbol de inventario y la pestaña Update Manager

3.	Añadimos los correspondientes Baseline a los objetos seleccionados

4.	Escaneamos estado de todos los componentes

5.	Una vez terminado el proceso de scan, nos mostrará el estado

6.	Lo primero que se tiene que actualizar es el VM Hardware, seleccionando el componente nos dará información de estado actual y versión actualizable

7.	Marcamos el componente de VM Hardware y “Remediate” para actualizar el Hardware Virtual



NOTA: Tenemos la posibilidad de programar la tarea o ejecutarlo en el momento

NOTA: Es recomendable tomar un snapshot antes de realizar la acción y marcar que se elimine automáticamente pasadas 24 horas


NOTA: La actualización de VM Hardware requiere de reinicio, por lo que tomar en cuenta cuando se aplicará este procedimiento
8.	Finalizado el proceso, aparecerá el componente como “Compliant”

9.	El proceso de actualización de las VMWare Tools es prácticamente idéntico al del VM Hardware

10.	Marcamos el componente de VMware Tools y “Remediate”






NOTA: La actualización de VMWare Tools requiere de reinicio, por lo que tomar en cuenta cuando se aplicará este procedimiento
11.	Una vez finalizado el proceso, ambos componentes estarán en estado “Compliant”






Un saludo!

Miquel.


