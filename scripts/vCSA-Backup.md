---
title: vCSA-Backup.sh
permalink: /vCSA-Backup/
layout: page
---

Ir al [post](https://miquelmariano.github.io/2017/08/backup-vcsa65-automatizado/)

```sh
#!/bin/bash
 ##### EDITABLE BY USER to specify vCenter Server instance and backup destination. #####
 VC_ADDRESS=vcenter.domain.local
 VC_USER=administrator@vsphere.local
 VC_PASSWORD=password
 FTP_ADDRESS=ftp-server.domain.local
 FTP_USER=ftp-user
 FTP_PASSWORD=ftp-password
 BACKUP_FOLDER=vCSA-Backup
 ############################

 # Authenticate with basic credentials.
 curl -u "$VC_USER:$VC_PASSWORD" \
    -X POST \
    -k --cookie-jar cookies.txt \
    "https://$VC_ADDRESS/rest/com/vmware/cis/session"

 # Create a message body for the backup request.
 TIME=$(date +%Y-%m-%d-%H-%M-%S)
 cat << EOF >task.json
 { "piece":
      {
          "location_type":"FTP",
          "comment":"Automatic backup",
          "parts":["seat"],
          "location":"ftp://$FTP_ADDRESS/$BACKUP_FOLDER/$TIME",
          "location_user":"$FTP_USER",
          "location_password":"$FTP_PASSWORD"
      }
 }
EOF

 # Issue a request to start the backup operation.
 echo Starting backup $TIME >>backup.log
 curl -k --cookie cookies.txt \
    -H 'Accept:application/json' \
    -H 'Content-Type:application/json' \
    -X POST \
    --data @task.json 2>>backup.log >response.txt \
    "https://$VC_ADDRESS/rest/appliance/recovery/backup/job"
 cat response.txt >>backup.log
 echo '' >>backup.log

 # Parse the response to locate the unique identifier of the backup operation.
 ID=$(awk '{if (match($0,/"id":"\w+-\w+-\w+"/)) \
           print substr($0, RSTART+6, RLENGTH-7);}' \
          response.txt)
 echo 'Backup job id: '$ID

 # Monitor progress of the operation until it is complete.
 PROGRESS=INPROGRESS
 until [ "$PROGRESS" != "INPROGRESS" ]
 do
      sleep 10s
      curl -k --cookie cookies.txt \
        -H 'Accept:application/json' \
        --globoff \
        "https://$VC_ADDRESS/rest/appliance/recovery/backup/job/$ID" \
        >response.txt
      cat response.txt >>backup.log
      echo ''  >>backup.log
      PROGRESS=$(awk '{if (match($0,/"state":"\w+"/)) \
                      print substr($0, RSTART+9, RLENGTH-10);}' \
                     response.txt)
      echo 'Backup job state: '$PROGRESS
 done

 # Report job completion and clean up temporary files.
 echo ''
 echo "Backup job completion status: $PROGRESS"
 rm -f task.json
 rm -f response.txt
 rm -f cookies.txt
 echo ''  >>backup.log
```

Ir al [post](https://miquelmariano.github.io/2017/08/backup-vcsa65-automatizado/)