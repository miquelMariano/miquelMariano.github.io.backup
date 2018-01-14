---
title: Configuración y administración vSphere Auto Deploy
date: '2018-01-17 00:00:00'
layout: post
image: /assets/images/posts/2018/01/autodeploy.png
headerImage: true
tag:
- vmware
- vsphere
- vexpert
- vcap
category: blog
author: miquelMariano
description: Configuración y administración vSphere Auto Deploy
hidden: false
permalink: /111/
---

Auto deploy usa [PXE](https://es.wikipedia.org/wiki/Preboot_Execution_Environment) para el desplieqgue de ESXi en una red. Cuanto un host se despliega mediante Auto deploy, la información de estado se carga en memoria durante el arranque. El estado, por defecto, no se almacena de forma permanente en el host.

Podemos usar Host Profile con Auto deploy para customizar el estado de nuestros hosts ESXi. A demás, desde  el menú de configuración avanzada de un ESXi, podemos configurar el host sin estado, o con un estado al arrancar.

En este post, veremos como se configura auto deploy y como se usa para provisionar nuevos hosts ESXi.

### Habilitar Auto Deploy en vCenter

Para habilitar el servicio Auto deploy, hacemos login en nuestro vCenter a través del web client.

Administración > Configuración del sistema > Servicios > Auto Deploy

![autodeploy1]({{ site.imagesposts2018 }}/01/autodeploy1.png)

### Configurar DHCP y TFTP

### Crear reglas de Autodeploy usando PowerCLI
