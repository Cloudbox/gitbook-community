## IMPORTANT NOTE: 
For the `Plex` role, this is now built into Cloudbox's `adv_settings.yml`. You can change the value and _reinstall Plex_ and it will do it for you. The deprecated manual way is seen below.

***


Plex uses `sqlite3` for its database. It has default amount of data that it can load into RAM that isn't really fit for purpose for massive libraries. Run the below **line by line** to increase the amount of data loaded into RAM to ensure quicker loading of your **dashboard library i.e. navigating Plex**.

**I take zero responsibility if your library becomes corrupted as a result of running this tweak. Run at your own risk.**

The `PRAGMA default_cache_size` default is `2000`.

Type one line at a time.

```
docker stop plex
cd "/opt/plex/Library/Application Support/Plex Media Server/Plug-in Support/Databases"
sqlite3 com.plexapp.plugins.library.db
PRAGMA default_cache_size = 6000000;
PRAGMA default_cache_size; 
.exit

docker start plex
```
## Emby
```
docker stop emby
cd /opt/emby/data/
sqlite3 library.db
pragma default_cache_size;
# (this will show current size)
pragma default_cache_size = 5000000;
pragma default_cache_size;
# (this will show current size, just to check it worked)
.exit
docker start emby
```
## Jellyfin
```
docker stop jellyfin
cd /opt/jellyfin/app/data/data/
sqlite3 library.db
pragma default_cache_size;
# (this will show current size)
pragma default_cache_size = 5000000;
pragma default_cache_size;
# (this will show current size, just to check it worked)
.exit
docker start jellyfin
```