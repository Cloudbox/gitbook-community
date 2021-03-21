qBittorrent is a torrent client that can be used as an alternative to rutorrent.\
This role is based on the [Linuxserver qBittorrent](https://hub.docker.com/r/linuxserver/qbittorrent/) docker image.

# **Installation**
Enter the following commands to install qBittorrent:

1. `cd ~/community`
2. `sudo ansible-playbook community.yml --tags qbittorrent`

# **Configuration**

Access qbittorrent at https://qbittorrent.yourdomain.com
Default username is `admin` and default password is `adminadmin`.

First go to `Options` -> `Web UI` and set a new username and password.

![Authentication Section Screenshot](https://i.imgur.com/Jbzg622.png)

Then go to `Options` -> `Connection` and set the port to 56881.

![Port Section Screenshot](https://i.imgur.com/PQcJIi4.png)

Now go to `Options` -> `Downloads` and set the following:
- Save files to location: `/mnt/local/downloads/torrents/qbittorrent/completed/`
- Keep incomplete torrents in: `/mnt/local/downloads/torrents/qbittorrent/incoming/`
- Copy .torrent files to: `/mnt/local/downloads/torrents/qbittorrent/torrents/`
- Copy .torrent files for finished downloads to: `/mnt/local/downloads/torrents/qbittorrent/torrents/`
- Additionally you can set monitored folder to: `/mnt/local/downloads/torrents/qbittorrent/watched/`
![Hard Disk Section Screenshot](https://i.imgur.com/S7U1XrB.png)

To extract torrents that are in rar format. Go to `Options` -> `Downloads` and tick `Run external program on torrent completion` and paste this into the box: `/usr/bin/unrar x -r "%F/." "%F/"`

Side note: if you're using private trackers only, then you might want to go to `Options` -> `BittTorrent` and uncheck everything in Privacy section.