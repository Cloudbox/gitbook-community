# _NOTE: changes at Google have led to this no longer being a viable setup.  Page left up for historical review_

# This is a quick guide to setting up strm with emby

Log onto your server and do the following

`cd ~/community`

`sudo ansible-playbook community.yml --tags drive_strm`

Once installed you need to edit the config file to match your setup

I suggest creating a new google project and keys for this

`sudo nano /opt/drive_strm/config.json`


```
{
"google": {
"allowed": {
"file_paths": [
"teamdrive/Media/Movies/Movies/", 
"teamdrive/Media/TV/",
"teamdrive2/Media/TV4K/"
],
"file_extensions": false,
"file_extensions_list":[
"webm","mkv","flv","vob","ogv","ogg","drc","gif",
"gifv","mng","avi","mov","qt","wmv","yuv","rm",
"rmvb","asf","amv","mp4","m4p","m4v","mpg","mp2",
"mpeg","mpe","mpv","m2v","m4v","svi","3gp","3g2",
"mxf","roq","nsv","f4v","f4p","f4a","f4b","mp3",
"flac","ts"
],
"mime_types": true,
"mime_types_list": ["video"]
},
"client_id": "googleusercontent.com",
"client_secret": "irJcfsecret",
"maindrive": false, if using normal drive or not
"teamdrive": true,
"teamdrives": ["data","data2"],
"poll_interval": 120
},
"server": {
"listen_ip": "0.0.0.0",
"listen_port": 7294,
"direct_streams": true 
},
"strm": {
"access_url": "https://strm.com/",
"root_path": "/strm",
"remove_empty_dirs": true,
"empty_dir_depth": 4,
"show_transcodes": true, 
"chunk_size": 250000
}
}

```

Save the config. 

Restart the docker for your config to kick in

`sudo docker restart drive_strm`

Now leave this to run for a while can take hrs depending on the size of library and if you are choosing to make transcoded
options

Check the status with

`tail -F /opt/drive_strm/activity.log`

Load emby and point your media directories at `mnt/strm/Media/movies` etc

Now for client side of emby to utilise the whole purpose of this

### Android app hack
Your going to need to install vlc or mx player (this is down to the emby internal player passes it to your server) open the
emby app go to settings /playback scroll down to advanced and choose enable external players.

Once done go back and choose somthing to play you should get a pop up asking which player to use here you want to
choose your vlc or mx player and set to default.

You should now be playing the stream direct from google enjoy

### Samsung tizen app
Probably not worth using as its very slow loading images if you have a large library you're going to struggle