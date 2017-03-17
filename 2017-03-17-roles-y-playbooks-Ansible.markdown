---
title: ¿Como se usan los roles y playbooks en Ansible?
date: '2017-03-17 00:14:00'
author: miquelMariano
tags: [ansible,devops,automation]
categories: [prueba1]
published: true
comments: true
permalink: /rpa/
layout: post
---


Queridos lectores del blog, como lo prometido es deuda, aquí tenéis la continuación de mi último post, [Ansible for dummies](https://miquelmariano.github.io/2017/01/ansible-for-dummies/).

En esta ocasión, vamos a profundizar un poco más en la utilización de playbooks y roles para ser mas ágiles en el control de la configuración de nuestra granja de servidores.

Como muchos ya sabréis, Ansible se puede utilizar en modo Ad-Hoc o mediante playbook. El modo ad-hoc nos permite ejecutar directamente comandos en una sola línea sobre nuestros hosts utilizando los módulos que ya tiene Ansible. Este modo se utiliza cuando queremos efectuar una acción simple sobre nuestros hosts, como es hacer un reinicio, verificar la conectividad con nuestro servidor de Ansible o simplemente realizar un ping a los miembros de un inventario.

![ansible-ping]({{ site.imagesposts2017 }}/03/ansible-ping.png)

Otra cosa es querer manejar las configuraciones o realizar despliegues sobre nuestra granja. En este caso, los playbooks son mucho mas atractivos 😉

Los playbooks estan escritos en formato YAML y pueden estar en un solo fichero o siguiendo un modelo estructurado. Cada playbook puede contener uno o más “plays”, que son los que nos van a ayudar a manejar/configurar nuestros diferentes hosts.

![automate-all-things]({{ site.imagesposts2017 }}/03/automate_all_the_things.jpeg)

Aquí un ejemplo de playbook con una estructura simple en un mismo fichero.

``` yaml
--- 
- hosts: webservers 
  vars: 
     http_port: 80 
     max_clients: 200 
     remote_user: root 
  tasks: 
    - name: ensure apache is at the latest version 
      yum: pkg=httpd 
      state=latest 
    - name: write the apache config file 
      template: 
        src=/srv/httpd.j2 
        dest=/etc/httpd.conf 
        notify: 
          - restart apache 
    - name: ensure apache is running service: 
      name=httpd state=started
```

En el ejemplo de arriba hemos creado toda la configuración en un mismo fichero. Esto esta bien si escribimos el playbook para un único despliegue o la configuración es simple. Sin embargo, para escenarios mas complejos es mejor utilizar roles, donde podremos moldear más a nuestro gusto las configuraciones.

Ejemplo de playbook llamando a un role:


``` yaml
---

- hosts: all 
  sudo: yes 
  roles: 
    - { role: apache }
```

# *Roles*

A medida que vamos añadiendo funcionalidad y complejidad a nuestros playbooks, cada vez se hace más difícil manejarlo con un solo fichero. Los roles, nos permiten crear un playbook con una mínima configuración y definir toda la complejidad y lógica de las acciones a más bajo nivel.

Según la propia documentación de Ansible: “Roles in Ansible build on the idea of include files and combine them to form clean, reusable abstractions – they allow you to focus more on the big picture and only dive down into the details when needed.”

Para la correcta utilización de los roles, es necesario crear toda una estructura de carpetas y subcarpetas donde iremos depositando nuestra configuración. Tenemos dos opciones para crear estas carpetas, de forma manual o utilizando ansible-galaxy. [Ansible-galaxy](https://galaxy.ansible.com/) es un sitio para la búsqueda, la reutilización y el intercambio de roles desarrollados por la comunidad.

Para crear un role mediante ansible-galaxy, ejecutamos el siguiente comando dentro de /etc/ansible/roles:

```
ansible-galaxy init webservers
```

Una vez creado el role, tendremos la siguiente estructura. Para entender bien los roles es importante entender dicha estructura:

![ansible-role-structure]({{ site.imagesposts2017 }}/03/ansible-role-structure.png)

+ Defaults:Este directorio debe contener un fichero llamado main.yml que contendrá información de las variables globales utilizadas por este role; como el directorio de instalación de apache o el puerto de escucha por defecto, entre otros.




