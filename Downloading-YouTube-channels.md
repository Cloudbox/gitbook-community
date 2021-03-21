From Stupifier - Discord

https://discordapp.com/channels/381077432285003776/486759605024587776/561901347629301790


***

The gist of the process is:

1. Install youtube-dl and ffmpeg

2. Create a youtube-dl config file in `/opt/youtube-dl/youtube-dl.conf`

3. Create a script that performs youtube-dl into a temporary folder, then moves the downloaded files from that folder to a cloudplow managed directory (such as _/mnt/local/Media/Youtube_)

4. Install Plex Metadata Agents and configure Plex Library

### Install youtube-dl and ffmpeg:
youtube-dl:
```
curl https://yt-dl.org/latest/youtube-dl -Lo /usr/local/bin/youtube-dl
chmod a+rx /usr/local/bin/youtube-dl
```
ffmpeg:
```
sudo apt update
sudo apt install ffmpeg
```
These are the bare minimum install methods; there are of course other versions and install methods, which are left as an exercise for the reader.
Some places to start:

[youtube-dl install](https://www.tecmint.com/install-youtube-dl-command-line-video-download-tool/)

[ffmpeg install](https://linuxize.com/post/how-to-install-ffmpeg-on-ubuntu-18-04/)

Once you've installed youtube-dl, you will want to keep it up to date.  If you installed it using the method above, `sudo youtube-dl -U` will update in place.

### Contents of `/opt/youtube-dl/youtube-dl.conf`:

All the shorthand flags have been expanded to their long versions for a little more clarity here.

Feel free to alter these as you require or see fit, but be sure you understand why you are making changes.
```
# ignore errors, like missing videos in playlists; if this isn't here youtube-dl will quit with the first "Not available in your country" or whatever
--ignore-errors

# download incomplete files from the beginning; none of these files are very big, so not much is lost by ignoring incomplete downloads
--no-continue

# output filename
--output "/mnt/local/downloads/YouTube/%(uploader)s/%(playlist)s (%(uploader)s)/%(playlist)s - S01E%(playlist_index)s - %(title)s [%(id)s].%(ext)s"

# reverse the playlist, so newer videos are at the end of the list
# the filename above has a season and episode in it.  If you don't reverse the playlist, then as new videos get added, the "episode number" of each video will be "1"
--playlist-reverse

# Archive Settings
# This keeps track of the videos you've downloaded
--download-archive /opt/youtube-dl/youtube-dl-archive.txt
# This is the list of channels/playlists you will scan/download
--batch-file /opt/youtube-dl/youtube-dl-channels.txt

# Uniform Format
# Grab the best MP4 if one exists, best available if not.
--format 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]/best'
# prefer ffmpeg for any media conversion
--prefer-ffmpeg
--ffmpeg-location /usr/bin/ffmpeg

# final file is an MKV container
--merge-output-format mkv

# Get All Subs to SRT
--write-sub
--all-subs
--convert-subs srt

# Get metadata
--add-metadata
--write-description
--write-thumbnail
--write-annotations
--write-info-json

# This flag may be necessary if you are getting a HTTP Error 429: Too Many Requests Error. 
# This flag will force youtube-dl to use ipv4 instead of ipv6.
--force-ipv4

# another option for a 429 is to run through a proxy
#--proxy https://111.222.333.444:5555
	
# Debug
--verbose
```
### Contents of `/opt/youtube-dl/script.sh`:

Of course, adjust those paths if required

```
#!/bin/bash

youtube-dl --config-location /opt/youtube-dl/youtube-dl.conf
sudo rsync -a /mnt/local/downloads/YouTube/ /mnt/local/Media/YouTube/ --remove-source-files
# Using rsync instead of mv to avoid "Directory not empty" error
exit 0
```

Make the script executable:
`sudo chmod +x /opt/youtube-dl/script.sh`

If you're planning to use this in a cron job, as detailed below, you may want to set the full path to youtube-dl:

```
/usr/local/bin/youtube-dl --config-location /opt/youtube-dl/youtube-dl.conf
```

### Example Contents of `/opt/youtube-dl/youtube-dl-channels.txt`:

[it is just a listing of the channels you want to download, or the individual videos]

```
# SPACE INVADER ONE UNRAID TUTORIAL CHANNEL
 https://www.youtube.com/channel/UCZDfnUn74N0WeAPvMqTOrtA
# Frog Leap Studios:
https://www.youtube.com/channel/UC98tcedR6gULv8_b70WJKyw
# Lock-Picking Lawyer
https://www.youtube.com/channel/UCm9K6rby98W8JigLoZOh6FQ
# Dubious Engineering
https://www.youtube.com/channel/UCie3bR_WnRg4f5y107accnQ
# Jelle's Marble Runs
https://www.youtube.com/channel/UCYJdpnjuSWVOLgGT9fIzL0g
# Engineer Guy Videos
https://www.youtube.com/user/engineerguyvideo

# TysyTube Restoration
https://www.youtube.com/channel/UCIGEtjevANE0Nqain3EqNSg
# my mechanics
https://www.youtube.com/channel/UCMrMVIBtqFW6O0-MWq26gqw
# Rescue & Restore
https://www.youtube.com/channel/UChzhFNSV-OuHQiYpwDMImsw
# Hand Tool Rescue
https://www.youtube.com/channel/UCasG9kJWi1eVxM0QkyqKVJQ
# Mark Rober
https://www.youtube.com/channel/UCY1kMZp36IQSyNx_9h4mpCg
# CoderJourney
https://www.youtube.com/channel/UCwgYv9lmioF0uR7dnsINFKw
# RetroHax
https://www.youtube.com/channel/UC8YUNeTvbq__XfSabNvKz3g
# retrorestore
https://www.youtube.com/channel/UC2tV98P91AgqOycQccMTG1g
```

### Add this command to your crontab running once a day:

```
/opt/youtube-dl/script.sh  #command to initiate
```
For example:

```
@daily /opt/youtube-dl/script.sh
```

### Install the Plex Metadata Agent for Youtube:

[Plex Forum Link](https://forums.plex.tv/t/rel-youtube-metadata-agent/44574)

[gitub repo](https://github.com/ZeroQI/YouTube-Agent.bundle)

```
[REL] YouTube Metadata Agent
This is a Metadata Agent for downloaded YouTube videos. 
It works by looking up metadata on YouTube using the YouTube video id. 
It is important to have this id in the filename, otherwise this agent can’t do the lookup. 
You can change the way the id is found in your filenames.
```

### Assign that agent to the Plex Library that contains these downloaded videos.