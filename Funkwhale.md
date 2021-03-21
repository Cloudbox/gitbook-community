### **Funkwhale** is a modern, self-hosted, free and open-source music server

### **Install Funkwhale**
* `cd ~/community`
* `sudo ansible-playbook community.yml --tags funkwhale`

* `docker exec -it funkwhale manage createsuperuser` (for ease of access, set it as your CloudBox username and password.)
* Go into funkwhale at https://funkwhale.domain.com with your just created user and password.
* Go into Music->Add Content->Create a new Library and fill out the information.
* Go into your new Library and Details. There will be a sharing link such as:
`https://funkwhale.domain.com/federation/music/libraries/da8bd97b-3c3f-4e7b-92cb-6ba45721837b`
* Copy out the last portion: `da8bd97b-3c3f-4e7b-92cb-6ba45721837b`
* Go back into your shell and do the music import:
  * `docker exec -it funkwhale /usr/bin/python3 /app/api/manage.py import_files da8bd97b-3c3f-4e7b-92cb-6ba45721837b "/music/Media/Audio/Music/**/**/*.flac" --in-place --async --recursive`

The above line explained:
  * `docker exec -it funkwhale /usr/bin/python3 /app/api/manage.py import_files` tells funkwhale to import music.
  * `da8bd97b-3c3f-4e7b-92cb-6ba45721837b` is your library id
  * `"/music/Media/Audio/Music/**/**/*.flac"` is the path to your media.
  * `--in-place` means do not copy the media into Funkwhale and leave it where it is.
  * `--async` means it will import the music first and then pull the metadata`
  * `--recursive` will recursively scan the folders

If everything goes as planned you'll get prompted like this:

> Checking imported paths against settings.MUSIC_DIRECTORY_PATH
> Import summary:
> - 149828 files found matching this pattern: ['/music/Media/Audio/Music/**/**/*.flac']

> - 0 files already found in database
> - 149828 new files
> Selected options: in place
> Are you sure you want to do this?
> Type 'yes' to continue, or 'no' to cancel:

 * Answer yes at the prompt and the import will begin.

Useful URLs
Libraries URL: https://funkwhale.domain.com/content/libraries/

Admin Account Edit Page: https://funkwhale.domain.com/api/admin/users/user/1/change/

If you want to use subsonic clients then you'll need to set a password here: https://funkwhale.domain.com/settings
(subsonic protocol requires storing password in cleartext, so to avoid compromising your Funkwhale account, we use a different password).

Additional documentation: [Funkwhale Docs](https://docs.funkwhale.audio/users/index.html)
