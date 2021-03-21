[Mylar](https://github.com/evilhero/mylar) is an automated Comic Book downloader (cbr/cbz) for use with SABnzbd, NZBGet and torrents. Also provides an OPDS server distribution.

# **Installing**
To install Mylar, enter the following commands:

1. `cd ~/community`
2. `sudo ansible-playbook community.yml --tags mylar`

# **Configuration**

Access Mylar at https://mylar.yourdomain.com

It's highly unlikely your mylar install is up to date. Press the Update link on the dialog in the bottom right hand corner. Mylar will update and then restart.

## Settings
### Web Interface
1. Enable some authentication. Add a username and password and set your preferred login method.
2. Make sure `Launch Browser on startup` is disabled.
3. You'll need a [ComicVine API](https://comicvine.gamespot.com/api/) Key for Mylar to be useful. [Create an account](https://comicvine.gamespot.com/login-signup/), and your key will be at [the top of this page](https://comicvine.gamespot.com/api/).
4. Set the Comic Location path to `/comics`. It will already be mounted.
5. Uncheck enforce permissions
6. _Optional_: Enable Series-Annual Integration
7. Save and then restart the app

> If you enable to OPDS server, DO NOT ENABLE `OPDS Fetch MetaInfo`. It queries the file system.
### Download settings
(These instructions are for NZBGet. Adapt for other Download Apps)
#### Configure NZBGet
1. Log into https://nzbget._youdomain_.com
1. Go to Settings > Categories
1. Scroll to bottom, click `Add Another Category`
1. Name it `mylar`
#### Configure Mylar
1. Set Usenet client to NZBGet
1. Fill in the server stuff like it would be in sonarr / radarr / etc
1. Set values:
   1. Host: `nzbget`
   1. Port: `6789`
   1. Username:  [[Your NZBGet Username|Install: NZBGet#security]]
   1. Password:  [[Your NZBGet Password|Install: NZBGet#security]]
   1. Category: `mylar`
   1. Use SSL: `No`
   1. NZBGet Download Directory: Leave Blank
   1. Enable Completed Download Handling: `X`
### Search Providers
1. Click Add Indexer (`+`).

1. Select "Newznab".
1. Add the following:
   1. Use Newznab: `X`
   1. NewzNab Name: NZBHydra2
   1. NewzNab Host: `http://nzbhydra2:5076`
   1. Verify SSL: Disabled
   1. API Key: [[Your NZBHydra2 API Key|Install: NZBHydra2#4-api-key]]
   1. Enabled: `X`

### Quality and Post Processing
1. Enable Failed Download Handling: `X`
1. Enable Automatic-Retry for Failed Downloads: `X`
1. Enable Post-Processing: `X`
1. When Post-Processing `move` the files

### Advanced Settings
> These settings are up to the user
1. Rename Files: `X`
1. Folder Format: `$Series ($Year)` _(My recommendation)_
1. File Format: `$Series $Annual $Issue ($Year)` _(My recommendation)_
