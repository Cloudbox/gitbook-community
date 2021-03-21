**Recommended Unpack Options:**
-
![](https://i.imgur.com/fVuDce1.png) 
***
**ExtCleanupDisk Recommended Options:**

`.par2, .sfv, .url, .txt, .jpg, .idx, .sfv.1, .rar.1, .jpg, .png, .htm, .html, _brokenlog.txt, *duplicate1.rar, .duplicate1.rar, .srs, .info, .md5, .1, .nfo, .srr, .exe, .sh, .rar, .gif, .wmv`
***
## **NZBGET SCRIPTS NOW AVAILABLE ON MASTER BRANCH** 
***
**Upgrading your NZBGet experience with Cloudbox:**

Cloudbox can install a handful of useful NZBGet extension scripts to help your get your files in order by running the following...

`sudo ansible-playbook cloudbox.yml --tags nzbget`
***
**Scripts installed as a result of using the `--tags nzbget`**

[Clinton-hall's flatten.py](https://github.com/clinton-hall/GetScripts/blob/master/flatten.py)

This will remove subdirectories and put all downloaded files into the root download directory. You can specify a unique directory and append category sub directory if wanted.

[Clinton-hall's DeleteSamples.py](https://github.com/clinton-hall/GetScripts/blob/master/DeleteSamples.py)

This will delete "-sample" files found alongside downloaded files.

[l3uddz's HashRenamer.py](https://raw.githubusercontent.com/Cloudbox/Cloudbox/master/roles/nzbget/files/HashRenamer.py)

Renames hashed filenames to the NZB's title.

[Prinz23's reverse_name.py](https://github.com/Prinz23/nzbget-pp-reverse)

This extension script for NZBGet will reverse filenames first then rename to folder name on failure.
***
**Other notable scripts worth mentioning:**

[Caronc's NZB-Notify](https://github.com/caronc/nzb-notify)

Push Notifications to a large number of supported services for NZBGet and SABnzbd. Push notifications to Boxcar, Discord, Emby, Faast, Growl, IFTTT, Join, Kodi, Mattermost, Prowl, Pushalot, PushBullet, Pushjet, Pushover, Rocket.Chat, Slack, Stride, Super Toasty, Telegram, Twitter, XBMC, Windows Notications & many more...