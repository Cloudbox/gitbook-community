Deluge is a torrent client that can be used as an alternative to rutorrent.

# **Installing**
To install Deluge, enter the following commands:

1. `cd ~/community`
2. `sudo ansible-playbook community.yml --tags deluge`

# **Configuration**

Access deluge at https://deluge.yourdomain.com

> The default password is "deluge", you will be prompted to change this
> when first logging in.

Click Preferences in the top bar and on the Downloads section enter the following paths:
* Download to: `/downloads/torrents/deluge/incoming`
* (optional) Move completed to: `/downloads/torrents/deluge/completed`
* (optional) Autoadd .torrent files from: `/downloads/torrents/deluge/watched`

![Download Section Screenshot](https://i.imgur.com/I8LtIhC.png)

Select Network section, uncheck `Use Random Ports` under `Incoming Ports` and set both input fields to `58112`.

![Network Section Screenshot](https://i.imgur.com/ijeCUBx.png)

Click Plugins and enable the labels plugin.

![Plugins Section Screenshot](https://i.imgur.com/sfDr8xc.png)

You can change the settings in the queue to match your preferred ratio requirements.

In order for Sonarr or Radarr to import media packaged within .rar files, they have to be extracted. In the same Plugins window, enable the "Extractor" plugin.

![Extractor Plugin Enable Screenshot](https://imgur.com/pwhnHDg.png)

After clicking "Apply", select the Extractor plugin on the left. Make sure the directory points to the `completed` folder within your Deluge data directory. Also, make sure that the `Create torrent name sub-folder` setting is checked.

![Extractor Plugin Configuration Screenshot](https://imgur.com/gT3YeMh.png)


# **Adding to Sonarr/Radarr**

To add Deluge as a download client in Sonarr/Radarr use the following settings. Both are able to remove completed torrents after they have finished seeding.

![Download Client Screen](https://i.imgur.com/PpMKBKx.png)

