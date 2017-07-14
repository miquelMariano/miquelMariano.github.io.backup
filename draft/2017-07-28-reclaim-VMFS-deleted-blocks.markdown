---
title: Reclamar bloques eliminados en datastores VMFS
date: '2017-07-28 00:00:00'
author: miquelMariano
tags: [VMWare,vSphere,vExpert,storage,VMFS]
categories: [prueba1]
published: true
comments: true
permalink: /reclaim/
layout: post
---

Buenos dias, en el post de hoy vamos a ver como reclamar bloques eliminados en nuestros datastores VMFS.

El proceso, consiste en reclamar el espacio que ya no se está utilizando en un datastore VMFS y devolverlo a la cabina para su posterior reutilización.

Es un proceso sencillo y se ejecuta en backgroud sin afectar al funcionamiento normal de la cabina. Para que se pueda recuperar este espacio no utilizado, es necesario que el ESXi marque estos bloques a 0, indicando de esta forma a la cabina, que no los está utilizando. En la nueva versión ESXi 6.5 el [proceso de unmap aparece como una de las mejoras](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/whitepaper/vsphere/vmw-white-paper-vsphr-whats-new-6-5.pdf), pero si disponemos una versión anterior, debejemos ejecutar el siguiente procedimiento.

1. Accedemos a cualquier ESXi del clúster por SSH
2. Verificamos que todos los volúmenes tienen Thin Provisioning habilitado:

```
esxcli storage core device list
``

![esxcli_storage_core_device_list]({{ site.imagesposts2017 }}/07/esxcli_storage_core_device_list.png)

3. Verificamos que todos los volúmenes utilizan el driver de Hitachi VMW_VAAIP_HDS y que soporta en Zero Status y el Delete Status

```
esxcli storage core device vaai status get
```

![esxcli_storage_core_device_vaai_status_get]({{ site.imagesposts2017 }}/07/esxcli_storage_core_device_vaai_status_get.png)

4. Lanzamos el commando para que marque con un 0 los bloques no utilizado de cada datastore

```
esxcli storage vmfs unmap -l DATASTORE01
```

5. Con el comando esxtop podremos ver como empieza a marcar bloques como eliminables


![esxtop1]({{ site.imagesposts2017 }}/07/esxtop1.png)


Para obtener esta vista en esxtop es necesario entrar en el menú de selección de columnas pusando f y seleccionar  solo las columnas a o p
Los valores mostrados en la columna Delete es el nº de bloques que se van a eliminar. El valor de cada bloque en VMFS5 es de 1MB



```python
#!/bin/python
 
import sys
import subprocess
 
tab = {}
print "\n* Analizando datatores..."
try:
# obtenemos stores y device
        program = ['esxcli', 'storage', 'vmfs', 'extent', 'list']
        out = subprocess.check_output(program)
        for i in out.splitlines():
                if i.find("naa.") != -1:
                        col = ' '.join(i.split()).split()
                        tab[col[3]]={'store': col[0],'thin':'', 'zero':'', 'delete': '', 'plugin': ''}
# obtenemos estado thin provisioning de los devices
        program = ['esxcli', 'storage', 'core', 'device', 'list']
        out = subprocess.check_output(program)
        parse = out.splitlines()
        iter = 0
        while iter < len(parse):
                while iter < len(parse) and parse[iter].startswith(" "):
                        iter += 1
                if parse[iter].startswith("naa."):
                        key = parse[iter]
                        iter += 1
                        while iter < len(parse) and parse[iter].startswith(" "):
                                if parse[iter].find("Thin Provisioning") != -1:
                                        if key in tab.keys():
                                                tab[key]['thin'] = parse[iter].split(':')[1].strip()
                                        else:
                                                print "Thin Provisioning Status: Key {0} not found".format(key)
 
                                iter+=1
                else:
                        iter+=1
# obtenemos soporte de stados Zero y Delete
        program = ['esxcli', 'storage', 'core', 'device', 'vaai', 'status', 'get']
        out = subprocess.check_output(program)
        parse = out.splitlines()
        iter = 0
        while iter < len(parse):
                while iter < len(parse) and parse[iter].startswith(" "):
                        iter += 1
                if parse[iter].startswith("naa."):
                        key = parse[iter]
                        iter += 1
                        while iter < len(parse) and parse[iter].startswith(" "):
                                if parse[iter].find("Zero Status") != -1:
                                        if key in tab.keys():
                                                tab[key]['zero'] = parse[iter].split(':')[1].strip()
                                        else:
                                                print "Zero Status: Key {0} not found".format(key)
                                if parse[iter].find("Delete Status") != -1:
                                        if key in tab.keys():
                                                tab[key]['delete'] = parse[iter].split(':')[1].strip()
                                        else:
                                                print "Delete Status: Key {0} not found".format(key)
                                if parse[iter].find("VAAI Plugin") != -1:
                                        if key in tab.keys():
                                                tab[key]['plugin'] = parse[iter].split(':')[1].strip()
                                        else:
                                                print "VAAI Plugin: Key {0} not found".format(key)
                                iter+=1
                else:
                        iter +=1
except subprocess.CalledProcessError as c:
        print 'Command:',c.cmd
        print 'Return:',c.returncode
        print 'Output:',c.output
 
print "\n* Comandos a lanzar:"
failed = []
for k,v in tab.iteritems():
        if v['thin'] != 'yes' or v['zero'] != 'supported' or v['delete'] != 'supported' or v['plugin'] != 'VMW_VAAIP_HDS':
                failed.append("Unsuported Reclaim Zero Pages disk: {0} {1}".format(k,v))
        else:
#                print "esxcli storage vmfs unmap -n 200 -l {0}".format(v['store'])
                print " Executing: esxcli storage vmfs unmap -n 200 -l {0}".format(v['store'])
                program = ['esxcli', 'storage', 'vmfs', 'unmap', '-n', '200', '-l', v['store']]
                out = subprocess.check_output(program)
 
print "\n* Datastore erroneos:"
for d in failed:
        print d
 
print "\n* Fin."
sys.exit
```

Ejemplo de salida del script:

```
python /tmp/reclaimZeroPages.py
```


```
* Analizando datatores...
Thin Provisioning Status: Key naa.60060e801332e000502032e000003106 not found
VAAI Plugin: Key naa.60060e801332e000502032e000003106 not found
Zero Status: Key naa.60060e801332e000502032e000003106 not found
Delete Status: Key naa.60060e801332e000502032e000003106 not found
 
* Comandos a lanzar:
 Executing: esxcli storage vmfs unmap -n 200 -l HUS110_Datastore000
 Executing: esxcli storage vmfs unmap -n 200 -l VSPG800_Datastore000
 Executing: esxcli storage vmfs unmap -n 200 -l VSPG800_Datastore002
 Executing: esxcli storage vmfs unmap -n 200 -l VSPG800_Datastore003
 Executing: esxcli storage vmfs unmap -n 200 -l HUSVM_Datastore000
 
* Datastore erroneos:
 
* Fin.
```


 
Un saludo

Miquel.