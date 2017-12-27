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
      src=/etc/tmp/{{ item }} 
      dest=/tmp/{{ item }}
    with_items:
      - prueba1.txt
      - prueba2.txt
```

> Primer concepto básico: Las variables se pueden usar en los argumentos del módulo y se referencian 
> entre llaves &#123;&#123;&#125;&#125;

# Variables and templates

# Using variables in conditions

# Getting variables from the system

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


