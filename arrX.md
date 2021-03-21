# Create multiple (Sonarr / Radarr / Bazarr) containers

Read through this entire page, even if you are only installing one of the apps.  The instructions at the bottom of the page assume you have read the material at the top of the page.

## Background
There are several roles in the community repo which can be used to create an arbitrary number of instances of a given application.  As of this writing, they are:

| Role          | Branch       | Description                 |
| ------------- | ------------ | --------------------------- |
| bazarrx       | Master       | Subtitle downloading        |
| lidarrx       | Develop      | Music management            |
| ombix         | Master       | Request management          |
| radarrx       | Master       | Movie management            |
| requestrrx    | Develop      | Discord request bot         |
| sonarrx       | Master       | TV management               |
| transmissionx | Develop      | Torrent client              |

They're all named something*X* because they allow creation of *X* number of *something*.

This started as a generalized replacement for the `radarr4k` and `sonarr4k` roles which were removed from cloudbox.

They are all configured in the same way.

In general terms, you'll enter the instances you want into `settings.yml`:

```yaml
appnamex:
  roles: ["", bing, bang, boing]
```

That will create:
  - appname
  - appnamebing
  - appnamebang
  - appnameboing

as docker containers, subdomain, and data directories in `/opt`  when you run the relevant tag.

For example, with this configuration:

```yaml
sonarrx:
  roles: ["", bing, bang, boing]
```

Running the community `sonarrx` tag would produce:

| entry         | Container    | Config dir         | Subdomain                    | Note                         |
| ------------- | ------------ | ------------------ | ---------------------------- | ---------------------------- |
| ""            | sonarr       | `/opt/sonarr`      | sonarr.YOURDOMAIN.TLD        | Replaces the stock container |
| bing          | sonarrbing   | `/opt/sonarrbing`  | sonarrbing.YOURDOMAIN.TLD    |                              |
| bang          | sonarrbang   | `/opt/sonarrbang`  | sonarrbang.YOURDOMAIN.TLD    |                              |
| boing         | sonarrboing  | `/opt/sonarrboing` | sonarrboing.YOURDOMAIN.TLD   |                              |

NOTE: the names have to be compliant with both domain names and docker names, so no funny business. Do not use anything but a-z and 0-9, no spaces, no commas, no colons, no dash, no exclamation marks, no nothing!

The names, within the constraints above, are completely arbitrary.  There is nothing magic about the example configs [1080webdl, 1080remux] given below.  They represent some common use cases, but you can use whatever names you wish, as in the "bing, bang, boing" examples above.

You will need to configure these new containers just as you did the stock containers.  One change; **be sure each one gets a unique download category**, so that each instance imports only those downloads meant for it.

Also, you probably want to put some thought into the directory and library structure you want to use.  See ["Customizing Plex Libraries"](https://github.com/Cloudbox/Cloudbox/wiki/Customizing-Plex-Libraries).

## Overwriting the stock container

The example above shows a `""` config entry.  For those apps which are also found in the stock cloudbox install, this will *overwrite* the existing container.  Then, when you rerun the cloudbox tag, this container will get overwritten by the stock one again.  You probably don't want that.  

For one thing, these "arrX" roles _may_ be based on different images than the stock images.  For example, for a while the `radarrx` role installed Radarr v3 while the stock role installed v2.  You should pick one: use this role to replace the stock one, or not.

You probably want to overwrite your existing role with this one; that will ensure that all your instances of Sonarr are based on the same image and get updated in the same way.  It's up to you, though, how you want to manage them.

### If you want to use this to overwrite your existing Sonarr/Radarr/etc container:

1. Include a `""` entry in the config:
   ```yaml
   sonarrx:
     roles: ["", bing, bang, boing]
   ```
2. Run the role as described below.
   ```bash
   cd ~/community
   sudo ansible-playbook community.yml --tags sonarrx
   ```
3. Add the tag to the `[skip]` section in `~/cloudbox/ansible.cfg`:
   ```
   [tags]
   skip = sonarr,whatever,whatever
   ```
That will ensure that the stock `sonarr` tag doesn't overwrite the container you are creating here.

When you want to update Sonarr, you'll run the Community `sonarrx` tag instead.

The same thing holds for every `arrX` variant discussed here.

### If you DO NOT want to overwrite your existing Sonarr/Radarr/etc container:

1. Make sure there IS NOT a `""` entry in the config:
   ```yaml
   sonarrx:
     roles: [bing, bang, boing]
   ```

That's all.  Your existing `sonarr` container will not be touched.

Again, the same thing holds for every `arrX` variant discussed here.

## Develop branch versions not discussed here

You'll note that there are only three variants specifically discussed below, and more than 3 variants in the table above.

The variants from above which are on the `develop` branch are not discussed in this article.  However, the keen eye will discern that the three sets of instructions below are identical in every way but role name, so one should be able to extrapolate how those `develop` roles may work.  If not, perhaps skip installing those things for now.

## Create multiple Sonarr v3 containers

1. Edit `settings.yml` and change the sonarrx roles to what you want:

   <details>
     <summary>I want to add a 4K version and leave my existing container untouched.</summary>
     <br />

   ```yaml
   sonarrx:
     roles: [ 4k ]
   ```
   </details>

   <details>
     <summary>I want to add webdl and remux versions and leave my existing container untouched.</summary>
     <br />

   ```yaml
   sonarrx:
     roles: [ 1080webdl, 1080remux ]
   ```
   </details>

   <details>
     <summary>I want to replace my existing version and add reality and kids versions.</summary>
     <br />

   ```yaml
   sonarrx:
     roles: [ "", reality, kids ]
   ```
   **Refer to the notes above about overwriting the default container.**

   </details>

1. Run the sonarrx role as a normal community role.

   ```bash
   cd ~/community
   sudo ansible-playbook community.yml --tags sonarrx
   ```

Remember that all those names are arbitrary and purely cosmetic for your own use.  There is nothing that ties `sonarrreality.YOURDOMAIN.TLD` to reality TV aside from the configuration that you are going to give it.

## Create multiple Radarr containers

1. Edit `settings.yml` and change the radarrx roles to what you want:

   <details>
     <summary>I want to add a 4K version and leave my existing container untouched.</summary>
     <br />

   ```yaml
   radarrx:
     roles: [ 4k ]
   ```
   </details>

   <details>
     <summary>I want to add webdl and remux versions and leave my existing container untouched.</summary>
     <br />

   ```yaml
   radarrx:
     roles: [ 1080webdl, 1080remux ]
   ```
   </details>

   <details>
     <summary>I want to replace my existing version and add documentary and kids versions.</summary>
     <br />

   ```yaml
   radarrx:
     roles: [ "", documentary, kids ]
   ```
   **Refer to the notes above about overwriting the default container.**

   </details>

1. Run the radarrx role as a normal community role.

   ```bash
   cd ~/community
   sudo ansible-playbook community.yml --tags radarrx
   ```

Remember that all those names are arbitrary and purely cosmetic for your own use.  There is nothing that ties `radarrdocumentary.YOURDOMAIN.TLD` to documentary movies aside from the configuration that you are going to give it.

## Create multiple Bazarr containers

1. Edit `settings.yml` and change the bazarrx roles to what you want:

   <details>
     <summary>I want to add a 4K version and leave my existing container untouched.</summary>
     <br />

   ```yaml
   bazarrx:
     roles: [ 4k ]
   ```
   </details>

   <details>
     <summary>I want to add webdl and remux versions and leave my existing container untouched.</summary>
     <br />

   ```yaml
   bazarrx:
     roles: [ 1080webdl, 1080remux ]
   ```
   </details>

   <details>
     <summary>I want to replace my existing version and add documentary and kids versions.</summary>
     <br />

   ```yaml
   bazarrx:
     roles: [ "", documentary, kids ]
   ```
   **Refer to the notes above about overwriting the default container.**

   </details>

1. Run the bazarrx role as a normal community role.

   ```bash
   cd ~/community
   sudo ansible-playbook community.yml --tags bazarrx
   ```
Remember that all those names are arbitrary and purely cosmetic for your own use.  There is nothing that ties `bazarrdocumentary.YOURDOMAIN.TLD` to documentary movies aside from the configuration that you are going to give it.

## Create a single Bazarr container

1. Edit `settings.yml` and change the bazarrx roles to:

   ```
   bazarrx:
    roles: [""]
   ```

1. Run the bazarrx role as a normal community role.

   ```bash
   cd ~/community
   sudo ansible-playbook community.yml --tags bazarrx
   ```


## Get Sonarr4k and Radarr4k Containers Again

1. Refer to the first example under the "Multiple Radarr/Sonarr" sections above.

1. Containers should be up and running again. With the same paths as were setup with CB, i.e. your data will have been migrated over if you had the original "radarrx" and "sonarrx" installed.  

# Tips

## Radarr

### Caching

If you use NZBHydra2 as an indexer in Radarr create a duplicate entry with [caching](https://github.com/theotherp/nzbhydra2/wiki/External-API,-RSS-and-cached-queries) enabled as an additional parameter. Repeat for Sonarr.

![Radarr Index Example](https://i.imgur.com/E3HX4Ao.png)

## Setting up Sonarr and Radarr in Bazarr
During the initial install of Bazarr, use either of the following setups to set up Sonarr and Radarr

* Hostname or IP Address: name of your Radarr/Sonarr container
* Listening port: 8989
* Base URL: empty
* SSL Enabled: no
* API Key: API Key retrieved from Sonarr/Radarr settings -> general

![Configure with container name](https://i.imgur.com/EB7VJzL.png)

* Hostname or IP Address: full domain of your Radarr/Sonarr instance, do not specify https (e.g., sonarr.example.com) 
* Listening port: 443
* Base URL: empty
* SSL Enabled: yes
* API Key: API Key retrieved from Sonarr/Radarr settings -> general

![Configure with domain name](https://i.imgur.com/QOM248v.png)

The latter may be simpler if you are configuring multiple BazarrX instances connected to multiple RadarrX/SonarrX instances, since you won't need to gather the ports for each individual instance.
