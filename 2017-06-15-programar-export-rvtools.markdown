---
title: Programar export automático de RVTools
date: '2017-06-15 00:00:00'
author: miquelMariano
tags: [VMWare,vSphere,vExpert,automation]
categories: [prueba1]
published: true
comments: true
permalink: /rvtools/
layout: post
---

RVTools es una aplicación de Windows .NET 4.0 que utiliza el VI SDK para mostrar información sobre entornos virtuales. 
Puede interactuar con vCenter o directamente contra un hosts ESXi
Es capaz de listar información sobre VMs, CPU, memoria, discos, particiones, red, unidades de disquete, unidades de CD, instantáneas, herramientas de VMware, grupos de recursos, clústeres, hosts ESX, HBA, Nics, Switches, Puertos , Interruptores Distribuidos, Puertos Distribuidos, Consolas de Servicio, Núcleos VM, Almacén de Datastores, información de rutas múltiples, información de licencia y controles de salud. 
Con RVTools puede desconectar las unidades de CD-ROM o de disquete de las máquinas virtuales y actualizar las VMware Tools instaladas dentro de cada máquina virtual a la última 
Soporta vCenter 6.5 y ESX 6.5.
Puede exportar la información a .xls o .csv



https://github.com/Sneddo/Powershell/blob/master/VMware/Export-RVTools.ps1 

```
<# 
.SYNOPSIS 
   Performs full export from RVTools
.DESCRIPTION
   Performs full export from RVTools. Archives old versions.
.NOTES 
   File Name  : Export-RVTools.ps1 
   Author     : John Sneddon
   Version    : 1.0.0
.PARAMETER Servers
   Specify which vCenter server(s) to connect to
.PARAMETER BasePath
   Specify the path to export to. Server name and date appended.
.PARAMETER OldFileDays
   How many days to retain copies
#>
param
(
   $Servers = @("Server"),
   $BasePath = "C:\Scripts\Powershell\RVToolsExport\Archive",
   $OldFileDays = 30
)

$Date = (Get-Date -f "yyyyMMdd")

foreach ($Server in $Servers)
{
   # Create Directory
   New-Item -Path "$BasePath\$Server\$Date" -ItemType Directory -ErrorAction SilentlyContinue | Out-Null

   # Run Export
   . "C:\Program Files (x86)\RobWare\RVTools\RVTools.exe" -passthroughAuth -s "$Server.internal.southernhealth.org.au" -c ExportAll2csv -d "$BasePath\$Server\$Date"

   # Cleanup old files
   $Items = Get-ChildItem "$BasePath\$server"
   foreach ($item in $items)
   {
      $itemDate = ("{0}/{1}/{2}" -f $item.name.Substring(6,2),$item.name.Substring(4,2),$item.name.Substring(0,4))
      
      if ((((Get-date).AddDays(-$OldFileDays))-(Get-Date($itemDate))).Days -gt 0)
      {
         $item | Remove-Item -Recurse
      }
   }
}
```

Un saludo

Miquel.