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

Buenos dias a tod@as!!

Para permitir mas flexibilidad en playbooks y roles, Ansible tiene la capacidad de trabajar con variables. Estas variables se pueden usar para recorrer una serie de valores determinados, acceder a informacion diversa, como el hostname o la ip de un sistema, e incluso reemplacer ciertas cadenas en una plantilla por valores específicos.

Las variables se pueden proporcionar a través del inventario, de un archivo de variables, o se pueden incluir por linea de comandos al llamar un playbook.

> Hay que tener en cuenta que los nombres de las variables deben ser letras, números o guiones bajos.
> Y que las variables siempre deben comenzar con una letra.


Dicho esto, la pregunta es ¿cómo usar variables? ¿Y cómo conseguirlos en primer lugar?

# Variables y loops


```yaml
tasks:
  - name: copy files
    copy: src={{ item }} dest=/tmp/{{ item }}
    with_items:
      - alha
      - beta
```

https://liquidat.wordpress.com/2016/01/26/howto-introduction-to-ansible-variables/

..


Un saludo!

Miquel.


