**Note from author:** I accept zero responsibility for if this breaks your setup. Works fine for me. Results may vary. Only issue I've seen is Radarr sometimes complains about a missing intermediate directory.

***

**Before you start, clear all folders & files from `/mnt/local/downloads/` and make sure NZBGet / rutorrent have no queued files in them.**

1. `cd ~/cloudbox`
2. Set the following... `nano settings.yml`
```
downloads:
  nzbs: /mnt/local/downloads/nzbs
  torrents: /mnt/local/downloads/torrents
```

***

**Important note:** if you are not **already** using the following paths above, change them in `settings.yml` and reinstall Cloudbox **now**.

`sudo ansible-playbook cloudbox.yml --tags cloudbox`

Wait for the install to finish then `sudo reboot` and wait for box to come back online.

***

3. `docker stop sonarr,sonarr4k,radarr,radarr4k,nzbget,rutorrent`
4. Set the following... `nano /opt/rutorrent/rtorrent/rtorrent.rc` 
```
# Default directory
directory.default.set = /downloads/torrents/rutorrent/completed

############################################################################
SCROLL DOWN A BIT & COMMENT OUT THE SECTION AS SEEN BELOW
############################################################################

# move completed downloads from incoming/ to completed/
# method.insert = d.get_finished_dir, simple, "cat=/downloads/torrents/rutorrent/completed/,$d.custom1="
# method.insert = d.data_path, simple, "if=(d.is_multi_file), (cat,(d.directory),/), (cat,(d.directory),/,(d.name))"
# method.insert = d.move_to_complete, simple, "d.directory.set=$argument.1=; execute=mkdir,-p,$argument.1=; execute=mv,-u,$argument.0=,$argument.1=; d.save_full_session="
# method.set_key = event.download.finished,move_complete,"d.move_to_complete=$d.data_path=,$d.get_finished_dir="
```
5. `docker start nzbget`
6. If anything starts to download, **stop it and delete it.** 
7. In NZBGet, go to `SETTINGS` then `PATHS`.
8. Set `MainDir` to `/downloads/nzbs/nzbget`, leave the rest as default i.e. `DestDir = ${MainDir}/completed` etc
9. `docker restart nzbget`
10. In NZBGet, click the `Pause for 3hrs` option to stop anything downloading for a bit.
11. `cd ~/cloudbox`
12. `sudo ansible-playbook cloudbox.yml --tags sonarr,sonarr4k,radarr,radarr4k,rutorrent`
13. Open Sonarr, go to Settings, Download Client and set the following `Remote Path Mappings`.
![](https://i.imgur.com/auPiAFM.png)
14. Repeat the `Remote Path Mappings` for `sonarr4k | radarr | radarr4k`. **Side note:** any extra containers you may have made will need these mappings as well.
15. Open all your Sonarr / Radarr instances, go to `Media Management` and set `Use Hardlinks instead of Copy` to `ON`.
16. Change all your root paths in Sonarr / Radarr to `/mnt/unionfs/Media/etc...`
17. Set "exclude_open_files" to `false` with `nano /opt/cloudplow/config.json`
```"uploader": {
        "google": {
            "check_interval": 1,
            "exclude_open_files": false,
            "max_size_gb": 2,
            "opened_excludes": [
                "/downloads/**"
```
18. `sudo systemctl restart cloudplow`
19. Enjoy hardlinking.