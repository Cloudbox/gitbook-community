# Create multiple (Sonarr / Radarr / Bazarr) roles

NOTE: the names have to be compliant with both domain names and docker names, so no funny business. Do not use anything but a-z and 0-9, no spaces, no commas, no colons, no dash, no exclamation marks, no nothing!

ALSO NOTE: All apps will prefix subdomain and docker container names with the name of the app. For example the subdomain and names of sonarrs docker containers will, with the default settings, be sonarr1080webdl and sonarr1080remux.

## Create multiple Sonarr v3 roles

1. Edit `settings.yml` and change the sonarrx roles to what you want:

   ```yaml
   sonarrx:
     roles: [1080webdl, 1080remux]
   ```

1. Run the sonarrx role as a normal community role.

   ```bash
   cd ~/community
   sudo ansible-playbook community.yml --tags sonarrx
   ```

## Create multiple Radarr roles

1. Edit `settings.yml` and change the radarrx roles to what you want:

   ```yaml
   radarrx:
    roles: [1080webdl, 1080remux]
   ```

1. Run the radarrx role as a normal community role.

   ```bash
   cd ~/community
   sudo ansible-playbook community.yml --tags radarrx
   ```


## Create multiple Bazarr roles

1. Edit `settings.yml` and change the bazarrx roles to what you want:

   ```
   bazarrx:
    roles: [1080webdl, 1080remux]
   ```

1. Run the bazarrx role as a normal community role.

   ```bash
   cd ~/community
   sudo ansible-playbook community.yml --tags bazarrx
   ```

## Get Sonarr4k and Radarr4k Containers Again

1. Edit `settings.yml`.

1. Add the following:

   ```yaml
   sonarrx:
    roles: ['4k']
   radarrx:
    roles: ['4k']
   ```

1. Run the following tags:

   ```bash
   cd ~/community
   sudo ansible-playbook community.yml --tags sonarrx,radarrx
   ```

1. Containers should be up and running again. With the same paths as were setup with CB, i.e. your data will have been migrated over.  

# Tips

## Radarr

### Caching

If you use NZBHydra2 as an indexer in Radarr create a duplicate entry with [caching](https://github.com/theotherp/nzbhydra2/wiki/External-API,-RSS-and-cached-queries) enabled as an additional parameter. Repeat for Sonarr.

![Radarr Index Example](https://i.imgur.com/E3HX4Ao.png)
