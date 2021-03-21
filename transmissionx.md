See [ArrX](https://github.com/Cloudbox/Community/wiki/arrX).

Suggested desktop client is [Transmission Remote GUI](https://github.com/transmission-remote-gui/transgui). It is to be set up with ssl enabled on port 443

/watch is hard-coded in the software and not editable from the settings.json, see [related issue](https://github.com/linuxserver/docker-transmission/issues/100). To get around this the folder is mounted to `/mnt/local/downloads/torrents/transmission{{ rolename }}/watch`

Do not change the published ports if you want to be connectable.