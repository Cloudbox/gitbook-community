_Originally by Kaiser; modified by desimaniac_

_< desimaniac: could also be replaced with a script that calls on different config files >_

_Note: You will only need this if you are running multiple instance of sonarrx or radarrx because this will point to different instances of sonarr, for example using it for animes specific sonarr or 1080remux radarr movies and we will use systemd, no cron job. Also this is assuming you have installed [Traktarr](https://github.com/l3uddz/Traktarr) (by [l3uddz](https://github.com/l3uddz/))_

### Config

1. First of all, we are going to make a copy of the `config.json` as well. Make sure to name it something similar or easy to remember hence why naming it to something similar with the `traktarr-animes.py` in my case I have named it `config-animes.json`.

   ```bash
   cp /opt/traktarr/config.json /opt/traktarr/config-animes.json
   ```

   _Note: Don't forget to edit the new `config-animes.json` file to add your sonarrx or radarrx api key._

### Systemd Setup

1. First head over to `cd /etc/systemd/system/` then we are going to make a copy of the service file for the `traktarr.service` again naming it something similar in my case I am going to be naming it `traktarr-animes.service`
 
   ```bash
   sudo cp traktarr.service traktarr-animes.service
   ```
1. Then we want to make sure to edit the file and point it to the new `traktarr-animes.py`
  
   ```bash
   sudo nano traktarr-animes.service
   ```

1. Edit the `ExecStart=/usr/bin/python3 /opt/traktarr.py run` to `ExecStart=/usr/bin/python3 /opt/traktarr/traktarr.py --config '/opt/traktarr/config-animes.json' --logfile '/opt/traktarr/activity-animes.log' run`.

   save the file by pressing
   ```bash
   ctrl + o
   ```
   Then to exit
   ```bash
   ctrl + x
   ```

1. Enable and start the service

   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable traktarr-animes.service
   sudo systemctl start traktarr-animes.service
   ```

### Shortcut

Lastly we are going to make a shortcut called 'traktarr-animes' so that we can access it anywhere just like `traktarr shows arg arg`.

1. Create the following file in '/usr/local/bin/traktarr-animes' .. `sudo nano /usr/local/bin/traktarr-animes'..

   ```bash
   #!/bin/bash
 
   CONFIGFILE='config-animes.json'
   LOGFILE='activity-animes.log'

   /usr/bin/python3 /opt/traktarr/traktarr.py --config "/opt/traktarr/$CONFIGFILE" --logfile "/opt/traktarr/$LOGFILE" "$@"
   ```

   save the file by pressing
   ```bash
   ctrl + o
   ```
   Then to exit
   ```bash
   ctrl + x
   ```

1. Then `sudo chmod +x /usr/local/bin/traktarr-animes`

1. If you have done everything correctly then you should be able to do `traktarr-animes` and get an output : 

   ![Traktarr Complete](https://i.imgur.com/7ZGE1ev.png)