# Python-PlexLibrary 

https://github.com/adamgot/python-plexlibrary

Create custom dynamic Plex Libraries like...
```
Movies - 1001 Movies You Must See Before You Die
Movies - Anime
Movies - IMDB Top 250
Movies - Kids
Movies - Recommended
Movies - Trending
TV - Trending
```

1. `cd ~/cloudbox` 
2. `sudo ansible-playbook cloudbox.yml --tags python-plexlibrary`
3. `nano /opt/python-plexlibrary/config.yml` (fill out details)
4. `cp /opt/python-plexlibrary/recipes/examples/cloudbox/movies_1001_movies_you_must_see_before_you_die.yml /opt/python-plexlibrary/recipes`
5. `nano /opt/python-plexlibrary/recipes/movies_1001_movies_you_must_see_before_you_die.yml` (fill out details)
6. `python plexlibrary movies_1001_movies_you_must_see_before_you_die`
7. Navigate to Plex Web.
8. Wait till you see the new library appear.
9. Quickly edit the library and turn off `Include in Dashboard` + `Enable video preview thumbnails` + set `Collections = Disabled`.
***
**Tip #1:** 

You can run the command `plexlibrary` from anywhere to run through each recipe you have in `/opt/python-plexlibrary/recipes/`
***
**Tip #2:** 

Set `"--skip-links": null` in your `/opt/cloudplow/config.json` to ignore the symlink warnings and stop `cloudplow` triggering unnecessarily.
```
"rclone_extras": {
    "--checkers": 16,
    "--drive-chunk-size": "64M",
    "--stats": "60s",
    "--transfers": 8,
    "--verbose": 1,
    "--skip-links": null
  },
```
***
**Tip #3:** 

Set the path in the recipes for the source_libraries as follows:

```
# Source library details
source_libraries:
    # [Cloudbox] 'name' = Plex library name.
  - name: 'Filme'
    # [Cloudbox] 'folders' = Plex library path (i.e '/data/...').
    folders:
      - '/data/Movies/Movies/'
```

The plex docker container has set "/mnt/unionfs/Media/" to "/data/" . Keep that in mind when setting the path.
***
**Tip #4:** 

If you've deleted a library after creating one with a recipe, make sure to delete the corresponding folder in Google Drive to ensure you can make it again in the future without issue. For example, one could be found in `Media\Movies\Movies-1001_Must_See`


***
**Tip #5:**

Formatting for multiple source libraries.

```yaml
source_libraries:
  - name: 'Library1' # as set in Plex
    folders:
      - '/path/inside/library' # as set in Plex
      - '/another/path/inside/the/same/library' # only if the plex library also has another path listed under it.
  - name: 'A completely different Library' # as set in Plex
    folders:
      - '/path/within/this/different/library' # as set in Plex
```