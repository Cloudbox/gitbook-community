## **Configure Rclone VFS Automatic Failover To Plexdrive**
###   **THIS WIKI IS STILL IN DRAFT, USE AT YOUR OWN RISK!**

One of the benefits of using a mergerfs mount over unionfs mount is that the mergerfs mount actually supports config changes on the fly, no need to make changes and then restart the mount to take affect. We can utilize this to automatically failover to plexdrive if there are any issues with the Rclone VFS mount.

The script below will check every second if a control file exists within /mnt/rclone, if the control file does not exist it will automatically swap the path used to be /mnt/plexdrive. After 5 minutes it will then attempt to restart the rclone service, perform the control file check and if successful swap the path back to /mnt/rclone.

### Requirements:
1) RcloneVFS mount setup.
2) MergerFS mount setup.
3) [Mergerfs.ctl](https://github.com/trapexit/mergerfs-tools)
4) A control file within your google drive. If you don't have one then a simple `touch /mnt/rclone/mounted.bin` will create it for you.

### Amendments to Rclone VFS & MergerFS
You need to make a few amendments to the defaults of RcloneVFS & Mergerfs.

1) `sudo nano /etc/systemd/system/mnt-unionfs.mount`  
Locate the following "xattr=nosys" and change it to "xattr=passthrough". This is required as the file that needs to be modified is a xattr file.

2) `sudo nano /etc/systemd/system/mnt-unionfs.mount`  
Locate the following "Requires=rclone.service" and remove this line completely. This is required otherwise when restarting the rclone service via the script it will cause the mount to restart also.




### Create script
Create the following  
`nano /opt/scripts/rclone/mergerfsmonitor.sh`
```
#!/usr/bin/env bash
while true
do
        while true
        do
                if [ ! -f /mnt/rclone/mounted.bin ]; then
                        echo "$(date) - Control file cannot be found, swapping from rclone to plexdrive" >> ~/logs/mergerfsmonitor.log
                        mergerfs.ctl add path /mnt/plexdrive
                        sleep 1s
                        mergerfs.ctl remove path /mnt/rclone
                        if [ -f /mnt/mergerfs/mounted.bin ]; then echo "$(date) - Mergerfs successfully swapped to use plexdrive." >> ~/logs/mergerfsmonitor.log; fi
                        break
                fi
        sleep 5s
        done

        while true
        do
                echo "$(date) - Waiting 5 minutes before attempting to recover rclone." >> ~/logs/mergerfsmonitor.log
                sleep 5m
                echo "$(date) - Attempting to restart rclonemount service and verify if mount is back up." >> ~/logs/mergerfsmonitor.log
                sudo /bin/systemctl restart rclone.service
                sleep 10s
                if [ -f /mnt/rclone/mounted.bin ]; then
                        echo "$(date) - Control file located, swapping from plexdrive back to rclone." >> ~/logs/mergerfsmonitor.log
                        mergerfs.ctl add path /mnt/rclone
                        sleep 1s
                        mergerfs.ctl remove path /mnt/plexdrive
                        if [ -f /mnt/mergerfs/mounted.bin ]; then echo "$(date) - Mergerfs successfully swapped to use rclone." >> ~/logs/mergerfsmonitor.log; fi
                        break
                fi
        done
done
```

And make it executable.  
`sudo chmod +x /opt/scripts/rclone/mergerfsmonitor.sh`

### Create Service File

Create the following  
`sudo nano /etc/systemd/system/mergerfsmonitor.service`

```
# /etc/systemd/system/mergerfsmonitor.service

[Unit]
Description=MergerFS Mount Monitor
After=network-online.target rclone.service mnt-unionfs.mount

[Service]
Type=simple
User=seed
Group=seed
ExecStartPre=/bin/sleep 10
ExecStart=/bin/bash /opt/scripts/rclone/mergerfsmonitor.sh

[Install]
WantedBy=default.target
```

Set the service to start on boot.  
`sudo systemctl enable mergerfsmonitor`

Start the service.  
`sudo systemctl start mergerfsmonitor`