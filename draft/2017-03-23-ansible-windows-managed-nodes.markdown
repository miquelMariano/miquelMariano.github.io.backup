---
title: Configuración de windows para ser manejado con Ansible
date: '2017-03-23 18:00:00'
author: miquelMariano
tags: [VMWare,vSphere,vExpert,devops,NcoraTeam]
categories: [prueba1]
published: true
comments: true
layout: post
permalink: /winrm/
---

Buenos dias queridos lectores!

En el post de hoy vamos a ver como con unos sencillos pasos, podremos configurar nuestros servidores windows para que puedan ser manejados desde Ansible.

# Preparar servidores widows

Inicialmente será necesario configurar el [WinRM](https://msdn.microsoft.com/en-us/library/aa384426%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396
) de tal forma que acepte conexiones desde nuestro nodo de control.

Los chicos de Ansible, se han currado un [script en PowerShell](https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1), con lo que solo con descargarlo y ejecutarlo ya tendremos esta parte configurada  

![WinRM]({{ site.imagesposts2017 }}/05/WinRM.png)

# Preparar servidor Ansible

Para ello, hay que instalar el gestor de paquetes de python-pip y todos los modulos necesarios, como pywinrm o kerberos:

```
yum install -y python-pip
pip install https://github.com/diyan/pywinrm/archive/master.zip#egg=pywinrm
yum -y install gcc python-devel krb5-devel krb5-workstation
pip install kerberos
```

# Crear inventario

Antes de crear o modificar nuestro fichero de inventario, deberemos crear las variables necesarias para conectarnos a nuestros windows, para ello, en el mismo directorio donde tengamos nuestro fiehero de inventario, crearemos la carpeta group_vars y el fichero de variabmes:

```
vim inventory/group_vars/windows.yml
```

Este fichero de variables deberá contener los siguientes datos:

```
ansible_ssh_user: administrador
ansible_ssh_pass: Secret123!
ansible_ssh_port: 5986
ansible_connection: winrm
ansible_winrm_server_cert_validation: ignore
```

En nuestro fiechero de inventario, deberemos de crear un bloque con el mismo nombre que el fichero de variables, en nuestro caso 'windows'

```
[windows]
demo01
demo02
demo03
``


# Comprobar

curl -vk -d "" -u administrator:VmwarE2016! http://172.25.34.249:5985/wsman


ansible -m win_ping -i inventory/servers windows -vvv

ansible -m win_file -a 'path=c:\\test.txt state=touch' -i inventory/servers windows

ansible -m win_updates -a 'category_names=SecurityUpdates' -i inventory/servers windows


En el post de hoy, voy a compartir este [#NcoraTutorial](https://www.ncora.com/tv/program/ncora-tutorials/), publicado hace unos dias, en el que vemos paso a paso cómo en vSphere 6.5 podemos realizar un backup y una restauración del vCenter, pieza clave en nuestro entorno corporativo y que probablemente queremos proteger por todos los medios posibles.

Espero que os guste!

[![Ncora tutorial 15](https://img.youtube.com/vi/OL7RC8_KI1A/0.jpg)](https://www.youtube.com/watch?v=OL7RC8_KI1A "Backup y restore de vCenter 6.5")

Un saludo

Miquel.