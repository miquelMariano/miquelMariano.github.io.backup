---
title: reclaimZeroPages.py
permalink: /reclaimZeroPages/
layout: page
---

Ir al [post](https://miquelmariano.github.io/2017/09/reclaim-VMFS-deleted-blocks)

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

Ir al [post](https://miquelmariano.github.io/2017/09/reclaim-VMFS-deleted-blocks/)