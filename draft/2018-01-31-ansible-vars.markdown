---
title: Uso de variables con Ansible
date: '2018-01-31 00:00:00'
layout: post
image: /assets/images/posts/2017/11/ansible.png
headerImage: true
tag:
- Ansible
- devops
- automation
category: blog
author: miquelMariano
description: Uso de variables con Ansible
hidden: false
o: "{{"
c: "}}"
permalink: /avars/
---

https://liquidat.wordpress.com/2016/01/26/howto-introduction-to-ansible-variables/

Buenos dias a tod@as!!

Para permitir mas flexibilidad en playbooks y roles, Ansible tiene la capacidad de trabajar con variables. Estas variables se pueden usar para recorrer una serie de valores determinados, acceder a informacion diversa, como el hostname o la ip de un sistema, e incluso reemplacer ciertas cadenas en una plantilla por valores específicos.

Las variables se pueden proporcionar a través del inventario, de un archivo de variables, o se pueden incluir por linea de comandos al llamar un playbook.

> Hay que tener en cuenta que los nombres de las variables deben ser letras, números o guiones bajos.
> Y que las variables siempre deben comenzar con una letra.


Dicho esto, la pregunta es ¿cómo usar variables? ¿Y cómo conseguirlos en primer lugar?

# Variables y loops

En general, los bucles son uno de los casos de uso mas comunes de variables. Si bien no estamos utilizando variables proporcionadas externamente, voy a intentar dar una primera idea de como usarlos.

Por ejemplo, voy a copiar un conjunto de archivos, es posible escribir una tarea para cada archivo o simplemente recorrerlos:

```yaml
tasks:
  - name: Copia ficheros
    copy: 
      src=/etc/tmp/{{ page.o }} item {{ page.c }}
      dest=/tmp/{{ page.o }} item {{ page.c }}
    with_items:
      - prueba1.txt
      - prueba2.txt
```

> Primer concepto básico: Las variables se pueden usar en los argumentos del módulo y se referencian 
> entre llaves {{ page.o }} variable {{ page.c }}

# Variables y templates

Las variables se pueden usar también para substituir parámetros en ficheros de configuración con valores específicos del sistema, extraidos directamente en tiempo de ejecución. Imaginemos por un momento, un archivo que debe contener el hostname real. Todas las máquinas son casi idénticas excepto por el nombre de host, por lo que esta variable no podrá estar predefinida, sinó que deberemos capturarla en tiempo de ejecución

En este caso, es mejor tener una copia del archivo de configuración, con una variable como place-maker en lugar de los nombres de host: aquí es donde las plantillas entran en juego:

```ssh
$ cat template.j2
My host name is {{ page.o }} ansible_hostname {{ page.c }}.
```

El módulo de Ansible para usar plantillas y sustitución de variables es el [módulo template](http://docs.ansible.com/ansible/latest/template_module.html):

```yaml
tasks:
  - name: copy template
    template: 
        src: template.j2 
        dest: "/tmp/tmp.conf
```
Cuando esta tarea se ejecute, copiará el fichero template.j2 con el nombre tmp.conf y substituirá la variable {{ page.o }} ansible_hostname {{ page.c }} por el nombre de host de cada servidor donde se ejecute.

> Los templates tinen que tener la extensión .j2 y utilizan el lenguage jinja2. Podeis leer mas en la [web 
> oficial](http://jinja.pocoo.org/docs/2.10/) del proyecto

# Usando variables dentro de condicionales

Las variables se pueden usar dentro de condiciones, lo que garantiza que ciertas tareas solo se ejecuten cuando, la variable solicitada se establece en un valor determinado:

```yaml
tasks:
  - name: Install Apache on Solaris
    pkg5: name=web/server/apache-24
    when: ansible_os_family == "Solaris"
 
  - name: Install Apache on RHEL
    yum:  name=httpd
    when: ansible_os_family == "RedHat"
```

> En este caso, la primera tarea solo se aplica en servidores Solaris, mientras que la segunda solo se ejecuta > en máquinas Red Hat.

# Usar variables del sistema



# Getting variables from the command line

# Setting variables in playbooks

# Setting variables in the inventory

# Setting variables on a system: local facts

# Using the results of tasks: registered variables

# Accessing variables of other hosts

# Conclusión

Las variables son una característica muy poderosa que nos ayuda a enriquecer la funcionalidad de Ansible. Junto con los templates y el lenguaje Jinja2, las posibilidades son casi infinitas.

Tarde o temprano, cada administrador tendrá que dejar atrás los simples roles y playbooks y comenzar a sumergirse en variables, templates y loops para hacer la automatización del sistema aún más fácil y dinámica.

Espero que esta pequeña guia os pueda ser de utilidad.

Un saludo!

Miquel.


