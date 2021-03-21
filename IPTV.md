Summarizing the steps taken to enable IPTV in Plex via the built in DVR:

### Any IPTV proxy [Telly, xTeve, etc.]:
* Subscribe to an IPTV service that provides an m3u playlist for their streams.  Specifics as to what telly requires are over at the [telly wiki](https://github.com/tellytv/telly/wiki/Prerequisites%3A-IPTV-Account).
* You'll probably need to contact your IPTV provider and ask them to enable VPN access so that you can use it on Hetzner, OVH etc. Some IPTV providers will not enable their version of this feature and will not work from a datacenter server.  
To check if you need to do this, log into your server via SSH and try to retrieve your M3U file: `curl -fLv -o test.m3u <YOUR M3U URL>`. If the transcript that will show up shows an error of some kind rather than downloading an M3U, chances are you need your provider to enable VPN.

### Telly 1.0 or 1.1:
* You'll need to trim down the available channels to 420 or less for use with Plex.  There are paid and free ways to accomplish this. See the [telly wiki on channel count](https://github.com/tellytv/telly/wiki/Channel-number-limit). Telly 1.0 will soldier on with channel counts higher than 420, possibly leading to bad behavior in Plex. Telly 1.1 will quit if your channel count is > 420 to prevent that bad behavior.
* You'll then need to add reliable EPG data to your new filtered channels list.  You can use your provider's EPG or a paid service like IPTV-EPG (500 channels subscription recommended) to add the correct EPG data. Use your m3u from Xtreme Editor with IPTV-EPG if you subscribe to both.
* For IPTV-EPG: you'll need to contact them and ask them to enable VPN access for you to be able to add it to your Cloudbox.
* For IPTV-EPG: With Telly 1.0, you can enable `Display LCN tag in EPG XML` in your account settings to get better channel numbers in Plex.
* Telly reads the EPG when it starts up; if you are using telly-provided EPG, you will want to script a periodic restart of the telly container to refresh the EPG.  The specific period depends on how many days of EPG your provider sends in the EPG file.

Before running the `telly` tag, you'll need to copy the `telly.yml` file in `~/community/`. If you don't already have this file, run the following command: 

```
cp -n ~/community/defaults/telly.yml.default ~/community/telly.yml
```

You specify the version of Telly you want to install in `telly.yml`:

```
nano ~/community/telly.yml
```

```yaml
telly:
  version: 1.1
```

`1.0`, `1.1`, and `1.5` are the available versions.  `1.1` is recommended by Telly team.

### Telly 1.1 [RECOMMENDED]:

Settings:

```yaml
telly11:
  streams: 1
  provider_name: CloudTV
  m3u_url: http://iptv.server:80/get.php?username=USERNAME&password=PASSWORD&type=m3u_plus&output=ts
  epg_url: http://iptv.server:80/xmltv.php?username=USERNAME&password=PASSWORD
  filter: USA
```

Telly 1.1 uses a config file, which will be written to `/opt/telly/telly.config.json`.  Once that config file is created, you can adjust settings by editing that file and restarting the container.  The values here are used in creating that initial config file.  If the file exists when you run this tag, the settings here WILL NOT override the existing ones in the config file.  When you change settings here, delete the existing config file before rerunning the tag.

There are more settings available in the config file; all will be at their defaults except for the four above.  See the telly wiki for [config file details](https://github.com/tellytv/telly/wiki/Running-Telly%3A-Config-File).

 * `streams` is the number of connections you want to use [some IPTV providers offer more than one]
 * `provider_name` is the name of your IPTV provider, and is used only cosmetically for logging.
 * `m3u_url` is a link or path to your m3u playlist; it must be EITHER a URL OR a path, NOT both.
 * `epg_url` is a link or path to your epg xml file; it must be EITHER a URL OR a path, NOT both.
 * `filter` is a regex as in 1.0, but it is always inclusive.

**The filter cannot be empty.**

**Both of the URLs [or paths] need to be specified.**

If you're using a file path, the path needs to be the **inside-the-container** path.  Put your m3u/xml files into `/opt/telly/`, and then in your config file refer to them as `/etc/telly/filename.m3u`.

These URLs or paths need to point **directly** to your M3U file.  Telly won't follow links inside the M3U until it finds a valid M3U.

Defining the filter is beyond the scope of this article.  See the [telly wiki about filtering](https://github.com/tellytv/telly/wiki/Running-Telly%3A-Filtering) for lots of detail and a link to some test scripts you can use to fine-tune your filter.

### NOTE: THIS FILTER WILL ALMOST CERTAINLY NEED TO BE CHANGED FROM THE DEFAULT BEFORE YOU USE TELLY. If you add telly to Plex and see no channels, what's probably happening is that this filter is filtering everything OUT.  If you are using IPTV-EPG.COM to set up your m3u, chances are you don't want it to be filtered any further.  Set the filter to ".*".

**If your filter results in a channel count higher than 420, telly will not load the channel list.  There will be a log entry to this effect.**

### Telly 1.0 [NOT RECOMMENDED]:

The `telly.yml` config file contains all the available telly settings; you will not need to change most of these:

```yaml
telly10:
  TELLY_FILTER_REGEX_MODE: true
  TELLY_FILTER_REGEX: "USA"
  TELLY_IPTV_PLAYLIST: "M3U_URL"
  TELLY_LOG_LEVEL: "Info"
  TELLY_LOG_REQUESTS: false
  TELLY_IPTV_DIRECT: false
  TELLY_IPTV_STARTING_CHANNEL: "10000"
  TELLY_IPTV_STREAMS: "1"
  TELLY_DISCOVERY_DEVICE_ID: "12345678"
  TELLY_DISCOVERY_DEVICE_FRIENDLY_NAME: "telly"
  TELLY_DISCOVERY_DEVICE_AUTH: "telly123"
  TELLY_DISCOVERY_DEVICE_MANUFACTURER: "Silicondust"
  TELLY_DISCOVERY_DEVICE_MODEL_NUMBER: "HDTC-2US"
  TELLY_DISCOVERY_DEVICE_FIRMWARE_NAME: "hdhomeruntc_atsc"
  TELLY_DISCOVERY_DEVICE_FIRMWARE_VERSION: "20150826"
  TELLY_DISCOVERY_SSDP: true
```

The only ones you will likely need to change are:

```yaml
  TELLY_FILTER_REGEX_MODE: true
  TELLY_FILTER_REGEX: "USA"
  TELLY_IPTV_PLAYLIST: "http://iptv.server:80/get.php?username=USERNAME&password=PASSWORD&type=m3u_plus&output=ts"
  TELLY_IPTV_STREAMS: "1"
```

 * `TELLY_FILTER_REGEX` is the regular expression applied to each channel in the M3U
 * `TELLY_FILTER_REGEX_MODE` controls the behavior of the regex; if `true` it's inclusive, if `false` [or missing] it's exclusive.
 * `TELLY_IPTV_PLAYLIST` is a link or path to your m3u playlist.
 * `TELLY_IPTV_STREAMS` is the number of connections you want to use [some IPTV providers offer more than one]

See the [telly wiki](https://github.com/tellytv/telly/wiki) for more details.

### NOTE: THIS FILTER WILL NEED TO BE CHANGED BEFORE YOU USE TELLY. If you add Telly to Plex and see no channels, what's probably happening is that this filter is filtering everything OUT.  If you are using IPTV-EPG.COM to set up your m3u, chances are you don't want it to be filtered any further.  Set the filter to ".*".

With telly 1.0, if you want to adjust settings you will need to change them here and then re-run the role to recreate the docker container.

If your IPTV provider's channel list is pretty static, you may want to consider downloading a copy of the m3u for faster access and configuring telly to access the file rather than the URL.  Remember that in this case the path needs to be internal to the docker container.

Similarly, you may wish to download a copy of your EPG-XML file, whether from provider or another source.  Download it into `/opt/telly`.

### Telly 1.5 [NOT RECOMMENDED]:
telly 1.5 is configured using a web interface and is an early unsupported alpha.  There is no documentation currently available for 1.5.

### Install:
* Install telly in your Cloudbox via the 'telly' tag. `sudo ansible-playbook community.yml --tags telly`.
That command must be run in the `community` directory.

### Adding the DVR to Plex:
* [All together now] The telly wiki covers [adding telly to Plex](https://github.com/tellytv/telly/wiki/Adding-Telly-to-Plex) in great detail.
* Open Plex Web, go to Settings, Server, Live TV & DVR.  If the telly DVR doesn't show up automatically, enter `telly:6077` as your `HDHOMERUN DEVICE ADDRESS`, hit Connect once, then "Continue".
* Choose a region.  Unless you're using Plex' EPG, this setting doesn't really matter.
* for telly 1.0, add the EPG URL or path, then fix any errors as you go through the wizard. Add any missing guide data in the channel mapper. Plex will not let you save a DVR with duplicate channels, so take this slowly and ensure there are no dupes.  Plex will tell you that there is a dupe, but will not identify it.
* for telly 1.1, enter `http://telly:6077/epg.xml` for the EPG.  All the channels will auto-match.  Channels that are disabled have no EPG and will not be usable with Plex.  Leave them disabled.
* Hit save.
* Wait for Plex to load your guide, enjoy DVR via Plex.

### Troubleshooting:

If you can add the telly DVR to Plex, then telly is running.  If you can add it and there are no channels, that is almost certainly a filtering problem.  Typically, telly has read the m3u, then applied the filter which filtered everything OUT.  This can also happen when telly cannot find or read its config file, but that's unlikely in the controlled environment of Cloudbox.  The [telly wiki](https://github.com/tellytv/telly/wiki) has a page that describes how you can know if that is the case.

Another cause of "can add it but there are no channels" is that the M3U telly sees doesn't contain channels, but links to another M3U.

If you cannot add telly to Plex, then telly isn't running; a common cause is a channel list > 420 channels.  Telly 1.1 will quit when your channel list is too big.

If you make changes to your telly config [channel list, etc], those changes may not be picked up by Plex until the Plex docker is restarted (`docker stop plex && docker start plex`).