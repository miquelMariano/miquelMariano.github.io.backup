---
title: Módulo de Telegram para Ansible
date: '2017-08-11 00:00:00'
author: miquelMariano
tags: [ansible,automation,devops]
categories: [prueba1]
published: true
comments: true
permalink: /ansible-telegram/
layout: post
---

Buenos dias, el otro dia me enteré que desde la versión 2.2 de Ansible, es posible [integrar notificaciones con Telegram](https://docs.ansible.com/ansible/telegram_module.html)

Para ello, solo necesitamos disponer de un bot, que [en su dia ya vimos como crear](https://miquelmariano.github.io/2017/02/notificaciones-automaticas-con-telegram/)

La integración en un playbook seria con el siguiente código:

```yaml
---

- name: Test telegram module
  hosts: localhost
  connection: local
  tasks:
    - name: Send test message
      telegram:
        token: "bot304017237:AAHpKXZBaw_wOF3H-ryhWl3F3wqIVP_Zqf8"
        chat_id: 6343788
        msg: "Message sent from Ansible playbook :)"
```

Acuerdate de modificar tu `token` y tu `chat_id` si no quieres que las notificaciones me lleguen a mi :-)

Podrás encontrar mas info sobre Ansible, [aquí](https://miquelmariano.github.io/tags/#ansible)


Un saludo

Miquel.