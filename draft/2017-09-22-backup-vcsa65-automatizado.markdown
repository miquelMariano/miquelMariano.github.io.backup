---
title: Programar backup automático en VCSA 6.5
date: '2017-07-15 00:00:00'
author: miquelMariano
tags: [vmware,vexpert,devops,automation]
categories: [prueba1]
published: true
comments: true
permalink: /vcsaautobackup/
layout: post
---

Buenos dias a tod@as!!

Hace varias semanas, publicamos un [#NcoraTutorial](https://miquelmariano.github.io/2017/03/backup-restore-vCenter-65/) sobre como hacer un backup de la configuración de un vCenter Appliance 6.5

En aquella ocasión, el procedimiento era algo manual ya que se hacia a través de la propia GUI de la administración del appliance.

En esta ocasión, veremos como podemos automatizar ese procedimiento y hacer backup de forma periódica de nuestro VCSA 6.5 usando un [FTP externo](https://miquelmariano.github.io/ftp/)


1) Nos conectamos por SSH a nuestro VCSA 6.5 y crearemos/configuraremos el fichero que contendrá el código. Se podrá ubicar en la ruta que creamos conveniente, en mi caso `/usr/local/bin`.

```
# Commands:
vi /usr/local/bin/vCSA-Backup.sh

# Make the file executable
chmod u+x /usr/local/bin/vCSA-Backup.sh

# Make it only accessible by root
chmod g-rxw /usr/local/bin/vCSA-Backup.sh
chmod o-rxw /usr/local/bin/vCSA-Backup.sh
```

2) Copiaremos el código del [script](https://miquelmariano.github.io/vCSA-Backup) en nuestro fichero

3) Realizamos el primer backup

```
/usr/local/bin/vCSA-Backup.sh
```

...la salida del script será similar a la siguiente:

```
root@vcenter65 [ /tmp ]# ./vCSA-Backup.sh
{"value":"6b0faced3684839d9107f3e2b57a52e7"}Backup job id: 20170717-132629-5318154
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   234    0   234    0     0   3957      0 --:--:-- --:--:-- --:--:--  4034
Backup job state: INPROGRESS
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   280    0   280    0     0   4695      0 --:--:-- --:--:-- --:--:--  4745
Backup job state: INPROGRESS
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   330    0   330    0     0   6201      0 --:--:-- --:--:-- --:--:--  6226
Backup job state: INPROGRESS
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   283    0   283    0     0   5384      0 --:--:-- --:--:-- --:--:--  5442
Backup job state: SUCCEEDED

Backup job completion status: SUCCEEDED
root@vcenter65 [ /tmp ]#

```

4) Configuramos el cron para automatizar periódicamente el backup. Por ejemplo, cada dia a las 2am 

```
#Command:
crontab -e

# Press 'i' to goto insert mode
# Insert you task into crontab
0 2 * * * /usr/local/bin/vCSA-Backup.sh

# Press ':wq'
# Press ENTER
```



Un saludo!

Miquel.



*[referencia](https://vm.knutsson.it/2017/01/vmware-vcsa-6-5-scheduled-backup/)