---
title: Migrar configuración de un vCenter a otro
date: '2017-03-15 00:00:00'
author: @miquelMariano
tags: [VMWare,vSphere,dvswitch,drs,vExpert]
categories: [prueba1]
published: true
comments: true
permalink: /borrador2/
layout: post
---

Hola de nuevo!

En el post de hoy voy a mostraros como migrar las configuraciones de un vCenter a otro.

El problema se plantea cuando por un motivo u otro es necesario hacer una reinstalación "start from the scratch" y claro, necesitamos mantener ciertas configuraciones:

+ vdSwitches
+ Roles
+ Permisos
+ Estructura de carpetas
+ Configuración/reglas de DRS

La migración de un vdSwitch es relativamente sencilla, simplemente con el [procedimiento de export/import](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2034602) tendremos la configuración en el nuevo vCenter.

El reto se plantea al querer migrar el resto de configuraciones, que por su volúmen, se hace imposible hacerlo de forma manual.

Gracias a la comunidad, encontré este [post](https://virtuallyjason.blogspot.com.es/2016/02/migrating-from-one-vcenter-to-another.html) que me resultó tremendamente interesente para hacer la migración lo menos "dolorosa" posible.

 
Un saludo

Miquel.