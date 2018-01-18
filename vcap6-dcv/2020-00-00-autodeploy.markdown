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

Hacemos click en el desplegable de "Acciones" y le damos a "Iniciar"

![autodeploy1]({{ site.imagesposts2018 }}/01/autodeploy1.png)

Adicionalmente, en caso de tener nuestra instancia sobre VCSA, también podremos habilitar el servicio de la siguiente manera:

```sshCommand>
Command> shell.set --enabled True
Command> shell
    ---------- !!!! WARNING WARNING WARNING !!!! ----------

Your use of "pi shell" has been logged!

The "pi shell" is intended for advanced troubleshooting operations and while
supported in this release, is a deprecated interface, and may be removed in a
future version of the product.  For alternative commands, exit the "pi shell"
and run the "help" command.

The "pi shell" command launches a root bash shell.  Commands within the shell
are not audited, and improper use of this command can severely harm the
system.

Help us improve the product!  If your scenario requires "pi shell," please
submit a Service Request, or post your scenario to the
https://communities.vmware.com/community/vmtn/vcenter/vc forum and add
"appliance" tag.

miquel-vcsa60:~ # service vmware-rbd-watchdog start
Starting /usr/bin/rbd-watchdog-linux:                                                                                    done
miquel-vcsa60:~ #
```

Una vez arrancado el servicio, podemos configurar el arranque automático desde el menú "Editar tipo de inicio"

![autodeploy2]({{ site.imagesposts2018 }}/01/autodeploy2.png)
![autodeploy3]({{ site.imagesposts2018 }}/01/autodeploy3.png)

Para configurar Autodeploy, navegaremos desde el web client Home > Lista de inventarios globales > Instancias de vCenter Server > seleccionamos nuestro vCenter > Pestaña configuración > Auto Deploy

Descargaremos el fichero TFTP Boot Zip para posteriormente subirlo en nuestro servidor DHCP/TFTP.

![autodeploy3]({{ site.imagesposts2018 }}/01/autodeploy4.png)

### Configurar DHCP y TFTP

Una vez arrancado y configurado el servicio auto deploy, el proximo paso es desplegar y configurar nuestro servidor DHCP y TFTP para poder arrancar por [PXE](https://es.wikipedia.org/wiki/Preboot_Execution_Environment) nuestros ESXi.

En mi caso, estoy utilizando un Windows 2012 R2 para levantar los servicios de DHCP y TFTP.

Lo primero, configuraremos el servicio TFTP. Estoy utilizando SolarWinds TFTP Server como servidor, es gratis y se puede descargar desde [aquí.](http://www.solarwinds.com/free-tools/free-tftp-server)

Instalamos el TFTP server y arrancamos la aplicación.

> El ejecutable se encuentra en C:\Program Files (x86)\SolarWinds\TFTP Server. Para mas comodidad, os podeis crear un icono en 
> vuestro escritorio.





### Crear reglas de Autodeploy usando PowerCLI



























