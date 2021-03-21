# Welcome to the Community Wiki!

A place for crowd-sourced cloudbox apps and guides. 
* Community apps are [provided](https://github.com/Cloudbox/Community/wiki/Contribute) by Cloudbox members. They are not part of the standard Cloudbox install, but they are intended to work on a Cloudbox system.  
* Community Guides are also written by Cloudbox users to help others make the most of their system. 

# How to Install Community Apps 

Install the Community repo following these [directions](Install "An install guide for the Cloubox/Community repository.").  

Once you have the Repo installed, you can install any Community app with this command: 

```cd ~/community && sudo ansible-playbook community.yml --tags "TAG"```

## Apps

The list below is probably out of date.  You can always get the most up-to-date list of apps available by looking at the roles in the code section. Click on a role name, look at the code, and you can see what docker image is used, the subdomain that will be setup, and what volumes are mounted to the docker (/mnt, etc). 
* Master: https://github.com/Cloudbox/Community/tree/master/roles
* Develop: https://github.com/Cloudbox/Community/tree/develop/roles

The `--list-tags` command will also list all available tags.
```
cd ~/community && sudo ansible-playbook community.yml --list-tags
```

| Tag         | Wiki                                                     | Official                                                     | Description                                                  |
| ---------------- | -------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| airdcpp          | [Setup](https://github.com/Cloudbox/Community/wiki/airdcpp) | [gangefors/airdcpp-webclient](https://hub.docker.com/r/gangefors/airdcpp-webclient) | AirDC++ Web Client Docker image                              |
| airsonic         | | [linuxserver/airsonic](https://hub.docker.com/r/linuxserver/airsonic) | web-based media streamer                                     |
| alltube          | [Setup](https://github.com/Cloudbox/Community/wiki/alltube) | [rudloff/alltube](https://hub.docker.com/r/rudloff/alltube)  | HTML GUI for youtube-dl                                      |
| alternatrr         | | [theultimatecoder/alternatrr](https://hub.docker.com/r/theultimatecoder/alternatrr) | Alternatrr Lets you add alternative titles to your sonarr instance by editing the sonarr.db file directly via a simple UI.                                     |
| alternatrrx         | | [theultimatecoder/alternatrr](https://hub.docker.com/r/theultimatecoder/alternatrr) | Multiple instances Version                                     |
| amongus         | | [denverquane/amongusdiscord](https://hub.docker.com/r/denverquane/amongusdiscord) | Discord Bot to harness Among Us game data, and automatically mute/unmute players during games!                                     |
| apprise         | | [caronc/apprise](https://hub.docker.com/r/caronc/apprise) | Apprise API was designed to easily fit into existing (and new) eco-systems that are looking for a simple notification solution.                                     |
| archivebox         | | [archivebox/archivebox](https://hub.docker.com/r/archivebox/archivebox) | ArchiveBox is a powerful self-hosted internet archiving solution written in Python. You feed it URLs of pages you want to archive, and it saves them to disk in a variety of formats depending on setup and content within.                                     |
| asshama          | [Setup](https://github.com/Cloudbox/Community/wiki/Plex-Scanners-and-Agents) | [ZeroQI/Hama.bundle](https://github.com/ZeroQI/Hama.bundle)  | HTTP Anidb Metadata Agent                                    |
| autoscan         | | [cloudb0x/autoscan](https://github.com/Cloudbox/autoscan) | Autoscan replaces the default Plex and Emby behaviour for picking up file changes on the file system. Autoscan integrates with Sonarr, Radarr, Lidarr and Google Drive to fetch changes in near real-time without relying on the file system.                                     |
| bazarrx          | [Setup](https://github.com/Cloudbox/Community/wiki/Bazarrx) | [linuxserver/bazarr](https://hub.docker.com/r/linuxserver/bazarr) | Companion application to Sonarr and Radarr to manage and download subtitles |
| beets            | [Setup](https://github.com/Cloudbox/Community/wiki/Beets) | [linuxserver/beets](https://hub.docker.com/r/linuxserver/beets) | Music library manager                                        |
| bitwarden        | [Setup](https://github.com/Cloudbox/Community/wiki/Bitwarden) | [bitwardenrs/server](https://hub.docker.com/r/bitwardenrs/server) | Bitwarden server API implementation written in Rust          |
| booksonic        |  | [linuxserver/booksonic](https://hub.docker.com/r/linuxserver/booksonic) | Subsonic compatible app to stream your audiobooks to any pc or android phone |
| bookstack        | [Setup](https://github.com/Cloudbox/Community/wiki/Bookstack) | [linuxserver/bookstack](https://hub.docker.com/r/linuxserver/bookstack) | Wiki designed for creating beautiful documentation           |
| btrfsmaintenance         | | [GitHub](https://github.com/kdave/btrfsmaintenance) | This is a set of scripts supplementing the btrfs filesystem and aims to automate a few maintenance tasks. This means the scrub, balance, trim or defragmentation.                                     |
| calibre          | [Setup](https://github.com/Cloudbox/Community/wiki/eBooks:-Calibre-and-Calibre-web-(new)) | [linuxserver/calibre](https://docs.linuxserver.io/images/docker-calibre) | Calibre Server using a Guacamole interface                         |
| calibre-web      | [Setup](https://github.com/Cloudbox/Community/wiki/eBooks:-Calibre-and-Calibre-web-(new)) | [linuxserver/calibre-web](https://hub.docker.com/r/linuxserver/calibre-web) | Web interface for browsing, reading and downloading eBooks using an existing Calibre database |
| cloudflare-dns         | |  | ### Needs update. ###                                   |
| coder            |  | [cdr/code-server](https://github.com/cdr/code-server)        | VS Code running on a remote server, accessible through the browser. |
| comicstreamer         | | [kalinon/comicstreamer](https://hub.docker.com/r/kalinon/comicstreamer) | Media server app for sharing a library of comic files.                                      |
| comixed         | | [comixed/comixed](https://github.com/comixed/comixed) | An application for managing digital comics.                                     |
| conreq         | | [roxedus/conreq](https://github.com/Archmonger/Conreq) | Conreq, a Content Requesting platform.                                     |
| couchpotato      |  | [linuxserver/couchpotato](https://hub.docker.com/r/linuxserver/couchpotato) | Automatic movie NZB and torrent downloader                   |
| deemix         | | [bockiii/deemix-docker](https://gitlab.com/Bockiii/deemix-docker) | More about it on the link.                                     |
| deemixrr         | | [theultimatecoder/deemixrr](https://hub.docker.com/r/theultimatecoder/deemixrr) |  Deemixrr manages your artists and playlists completely automated. You add your favorite artists and playlists, and Deemixrr does the rest for you.                                    |
| deezloader-remix |  | [bocki/deezloaderrmx](https://hub.docker.com/r/bocki/deezloaderrmx) | Download songs, playlists and albums directly from Deezer's Server |
| deluge           | [Setup](https://github.com/Cloudbox/Community/wiki/Deluge) | [linuxserver/deluge](https://hub.docker.com/r/linuxserver/deluge) | Lightweight BitTorrent client                                |
| delugevpn        | [Setup](https://github.com/Cloudbox/Community/wiki/DelugeVPN) | [binhex/arch-delugevpn](https://hub.docker.com/r/binhex/arch-delugevpn) | Arch Linux base running Deluge, OpenVPN and Privoxy          |
| drive_strm         | | [cloudb0x/drive_strm](https://hub.docker.com/r/cloudb0x/drive_strm) | ### Needs update ###                                     |
| emby2         | | [emby/embyserver](https://hub.docker.com/r/emby/embyserver) | Emby Server is a home media server built on top of other popular open source technologies such as Service Stack, jQuery, jQuery mobile, and .NET Core.                                     |
| embystat         |  | [uping/embystat](https://hub.docker.com/r/uping/embystat)    | Standalone Emby statistics server                            |
| epms             |  | [mjarends/extendedpersonalmedia-agent](https://bitbucket.org/mjarends/extendedpersonalmedia-agent.bundle.git) | Advanced Metadata Agent for personal media files             |
| filebot          | [Setup](https://github.com/Cloudbox/Community/wiki/Filebot) | [jlesage/filebot](https://hub.docker.com/r/jlesage/filebot)  | Tool for organizing and renaming your movies, tv shows or anime, and music well as downloading subtitles and artwork |
| filebrowser      | [Setup](https://github.com/Cloudbox/Community/wiki/Filebrowser)                                                          | [filebrowser/filebrowser](https://hub.docker.com/r/filebrowser/filebrowser) | File management web interface to upload, delete, preview, rename and edit your files |
| filezilla        |  | [jlesage/filezilla](https://hub.docker.com/r/jlesage/filezilla) | FileZilla is a cross-platform graphical FTP, SFTP, and FTPS file management tool with a vast list of features |
| flaresolverr     | [Setup](https://github.com/Cloudbox/Community/wiki/FlareSolverr) | [flaresolverr/flaresolverr](https://hub.docker.com/r/flaresolverr/flaresolverr) | FlareSolverr is a proxy server to bypass Cloudflare protection |
| funkwhale        | [Setup](https://github.com/Cloudbox/Community/wiki/Funkwhale) | [thetarkus/funkwhale](https://hub.docker.com/r/thetarkus/funkwhale) | Modern, self-hosted, free and open-source music server       |
| gazee            |  | [linuxserver/gazee](https://hub.docker.com/r/linuxserver/gazee) | WebApp Comic Reader for your favorite digital comics         |
| gitea            |  | [gitea/gitea](https://hub.docker.com/r/gitea/gitea)          | Community managed painless self-hosted Git service           |
| glances          |  | [satzisa/glances](https://hub.docker.com/r/satzisa/glances)  | monitoring tool which aims to present a large amount of monitoring information through a curses or Web based interface |
| goplaxt          | [Setup](https://github.com/Cloudbox/Community/wiki/Goplaxt) | [xanderstrike/goplaxt](https://hub.docker.com/r/xanderstrike/goplaxt) | Alternative way to log Plex media playback to a Trackt account |
| gotify           |  | [gotify/server](https://hub.docker.com/r/gotify/server)      | simple server for sending and receiving messages using web sockets |
| grafana         | | [grafana/grafana](https://hub.docker.com/r/grafana/grafana/) | Grafana has become the world’s most popular technology used to compose observability dashboards with everything from Prometheus & Graphite metrics, to logs and application data to power plants and beehives.                                     |
| guacamole        |  | [jasonbean/guacamole](https://hub.docker.com/r/jasonbean/guacamole) | Clientless remote desktop gateway that supports standard protocols like VNC and RDP |
| handbrake        |  | [jlesage/handbrake](https://hub.docker.com/r/jlesage/handbrake) | Tool for converting video from nearly any format to a selection of modern, widely supported codecs |
| healthchecks         | | [linuxserver/healthchecks](https://image.url) | Healthchecks is a watchdog for your cron jobs. It's a web server that listens for pings from your cron jobs, plus a web interface.                                     |
| heimdall         |  | [linuxserver/heimdall](https://hub.docker.com/r/linuxserver/heimdall) | a way to organize all the links to your most used web sites and web applications in a simple way |
| hetzner_nfs         | |  | Connect 2+ servers hosted on Hetzner using NFS and VLAN.                                     |
| influxdb         | | [influxdb](https://hub.docker.com/_/influxdb) | InfluxDB is a time series database designed to handle high write and query loads.                                     |
| invoiceninja     | [Setup](https://github.com/Cloudbox/Community/wiki/InvoiceNinja) | [rxwatcher/docker-invoiceninja-nginx](https://hub.docker.com/r/rxwatcher/docker-invoiceninja-nginx) | open-source invoicing and time-tracking app                  |
| jdownloader2     | [Setup](https://github.com/Cloudbox/Community/wiki/JDownloader2) | [jlesage/jdownloader-2](https://hub.docker.com/r/jlesage/jdownloader-2) | Download management tool that makes downloading as easy and fast as it should be. |
| jellyfin         | [Setup](https://github.com/Cloudbox/Community/wiki/Jellyfin) | [linuxserver/jellyfin](https://hub.docker.com/r/linuxserver/jellyfin) | Alternative to the proprietary Emby and Plex, to provide media from a dedicated server to end-user devices via multiple apps |
| jirafeau         |  | [jgeusebroek/jirafeau](https://hub.docker.com/r/jgeusebroek/jirafeau) | Allows you to easily upload a file and generate an unique link to it |
| kcptun-client    |  | [horjulf/kcptun](https://hub.docker.com/r/horjulf/kcptun)    | A Stable & Secure Tunnel based on KCP. Fast, reliable and reduces tunnel latency by up to 40% by using just a little bit more bandwidth. |
| kcptun-server    |  | [horjulf/kcptun](https://hub.docker.com/r/horjulf/kcptun)    | A Stable & Secure Tunnel based on KCP. Fast, reliable and reduces tunnel latency by up to 40% by using just a little bit more bandwidth. |
| kitana           |  | [pannal/kitana](https://github.com/pannal/Kitana)            | Responsive Plex plugin web frontend                          |
| komga         | | [gotson/komga](https://hub.docker.com/r/gotson/komga) | A comics/mangas server to serve/stream pages via API                                      |
| lazylibrarian    |  | [thraxis/lazylibrarian-calibre](https://hub.docker.com/r/thraxis/lazylibrarian-calibre) | follow authors and grab ebooks and associated metadata       |
| lidarrx         | | [hotio/lidarr](https://hub.docker.com/r/hotio/lidarr) | Lidarr is a music collection manager for Usenet and BitTorrent users. It can monitor multiple RSS feeds for new tracks from your favorite artists and will grab, sort and rename them. It can also be configured to automatically upgrade the quality of files already downloaded when a better quality format becomes available. Role to create multiple roles (default is one).                                     |
| logarr           |  | [monitorr/logarr-alpha](https://hub.docker.com/r/monitorr/logarr-alpha) | Self-hosted, single-page, log consolidation tool written in PHP |
| mariadb          |  | [linuxserver/mariadb](https://hub.docker.com/r/linuxserver/mariadb) | one of the most popular database servers. Made by the original developers of MySQL |
| mediabutler      | [Setup](https://github.com/Cloudbox/Community/wiki/Mediabutler) | [mediabutler/server](https://hub.docker.com/r/mediabutler/server) | personal media companion, providing a unified experience for several applications that you may be using |
| medusa           |  | [linuxserver/medusa](https://hub.docker.com/r/linuxserver/medusa) | Automatic TV show downloader                                 |
| minecraft        |  | [itzg/minecraft-server](https://hub.docker.com/r/itzg/minecraft-server) | Minecraft Server that will automatically download the latest stable version at startup |
| mongodb          |  | [mongo](https://hub.docker.com/_/mongo)                      | MongoDB document databases provide high availability and easy scalability |
| monitorr         |  | [monitorr/monitorr](https://hub.docker.com/r/monitorr/monitorr) | Webfront to live display the status of any webapp or service |
| mylar            | [Setup](https://github.com/Cloudbox/Community/wiki/Mylar) | [linuxserver/mylar](https://hub.docker.com/r/linuxserver/mylar) | automated Comic Book downloader (cbr/cbz) for use with SABnzbd, NZBGet and torrents |
| mylar3         | | [linuxserver/mylar](https://hub.docker.com/r/linuxserver/mylar) | Version                                    |
| navidrome         | | [deluan/navidrome](https://hub.docker.com/r/deluan/navidrome) | Navidrome is an open source web-based music collection server and streamer. It gives you freedom to listen to your music collection from any browser or mobile device. It's like your personal Spotify!                                     |
| nextcloud        |  | [linuxserver/nextcloud](https://hub.docker.com/r/linuxserver/nextcloud) | self-hosted productivity platform that keeps you in control  |
| nowshowing       |  | [ninthwalker/nowshowing](https://hub.docker.com/r/ninthwalker/nowshowing) | provides a summary of new media that has recently been added to Plex |
| nzbhydra         |  | [linuxserver/hydra](https://hub.docker.com/r/linuxserver/hydra) | meta search for NZB indexers                                 |
| ombix            |  | [hotio/ombi](https://hub.docker.com/r/hotio/ombi)            | Automatically gives your shared Plex or Emby users the ability to request content by themselves. Role to create multiple roles (default is one). |
| organizrv1       |  | [lsiocommunity/organizr](https://hub.docker.com/r/lsiocommunity/organizr) | one stop shop for your Servers Frontend                      |
| ouroboros        | [Setup](https://github.com/Cloudbox/Community/wiki/Ouroboros) | [pyouroboros/ouroboros](https://hub.docker.com/r/pyouroboros/ouroboros) | Ouroboros will monitor (all or specified) running docker containers and  update them to the (latest or tagged) available image in the remote  registry |
| overseerr        |  | [sctx/overseerr](https://hub.docker.com/r/sctx/overseerr) | Plex request management and media discovery tool
| overseerrx       |  | [sctx/overseerr](https://hub.docker.com/r/sctx/overseerr) | Role to create multiple roles (default is one).
| plex2            |  | [cloudb0x/plex](https://hub.docker.com/r/cloudb0x/plex)      | Enhanced version of the [plexinc/pms-docker](https://github.com/plexinc/pms-docker) Docker image |
| pyload           |  | [cobraeti/pyload](https://hub.docker.com/r/cobraeti/pyload)  | Download Manager written in pure Python                      |
| qbittorrent      | [Setup](https://github.com/Cloudbox/Community/wiki/qBittorrent) | [linuxserver/qbittorrent](https://hub.docker.com/r/linuxserver/qbittorrent) | Torrent client                                               |
| qbittorrentvpn         | | [linuxserver/qbittorrent](https://hub.docker.com/r/linuxserver/qbittorrent) | Torrent client with VPN support                                    |
| quassel          |  | [linuxserver/quassel-core](https://hub.docker.com/r/linuxserver/quassel-core) | modern, cross-platform, distributed IRC client, meaning that one (or  multiple) client(s) can attach to and detach from a central core |
| radarrx          | [Setup](https://github.com/Cloudbox/Community/wiki/RadarrX) | [hotio/radarr](https://hub.docker.com/r/hotio/radarr)        |
Automatically downloads movies via Usenet and BitTorrent. Role to create multiple roles (default is one).     |
| redbot         | | [phasecorex/red-discordbot](https://github.com/PhasecoreX/docker-red-discordbot) | Red is a fully modular bot – meaning all features and commands can be enabled/disabled to your liking, making it completely customizable. This is a self-hosted bot – meaning you will need to host and maintain your own instance. You can turn Red into an admin bot, music bot, trivia bot, new best friend or all of these together!                                     |
| requestrr         | | [darkalfx/requestrr](https://hub.docker.com/r/darkalfx/requestrr) | Requestrr is a chatbot used to simplify using services like Sonarr/Radarr/Ombi via the use of chat!                                     |
| requestrrx         | | [darkalfx/requestrr](https://hub.docker.com/r/darkalfx/requestrr) | Role to create multiple roles (default is one).                                     |
| resilio-sync     |  | [resilio/sync](https://hub.docker.com/r/resilio/sync)        | Fast, private file sharing for teams and individuals         |
| rocketchat       |  | [rocketchat/rocket.chat](https://hub.docker.com/r/rocketchat/rocket.chat) | Ultimate Open Source WebChat Platform                        |
| sickchill        |  | [linuxserver/sickchill](https://hub.docker.com/r/linuxserver/sickchill) | Automatic Video Library Manager and Downloader for TV Shows  |
| smokeping         | [Setup](https://github.com/Cloudbox/Community/wiki/Smokeping) | [linuxserver/smokeping](https://hub.docker.com/r/linuxserver/smokeping) | Smokeping keeps track of your network latency.                                     |
| sonarrx          | [Setup](https://github.com/Cloudbox/Community/wiki/SonarrX) | [hotio/sonarr](https://hub.docker.com/r/hotio/sonarr)        | Automatic Video Library Manager and Downloader for TV Shows. Role to create multiple roles (default is one).  |
| speedtest        |  | [satzisa/html5-speedtest](https://hub.docker.com/r/satzisa/html5-speedtest) | very lightweight Speedtest implemented in Javascript, using XMLHttpRequest and Web Workers |
| sshwifty         |  | [niruix/sshwifty](https://hub.docker.com/r/niruix/sshwifty)  | SSH and Telnet connector made for the Web                    |
| stash         | | [stashapp/stash](https://github.com/stashapp/stash) | Stash is a locally hosted web-based app written in Go which organizes and serves your p*rn.                                     |
| subsonic         |  | [theultimatecoder/subsonic](https://hub.docker.com/r/theultimatecoder/subsonic) | Subsonic music streamer                                      |
| synclounge       | [Setup](https://github.com/Cloudbox/Community/wiki/SyncLounge) | [starbix/synclounge](https://hub.docker.com/r/starbix/synclounge) | Enjoy Plex with your friends. In Sync. Together.             |
| tdarr            | [Setup](https://github.com/Cloudbox/Community/wiki/Tdarr) | [haveagitgat/tdarr_aio](https://hub.docker.com/r/haveagitgat/tdarr_aio) | Audio/Video library analytics + transcode automation using FFmpeg/HandBrake + video health checking |
| telegraf         | | [telegraf](https://hub.docker.com/_/telegraf) | Telegraf is an agent for collecting metrics and writing them to InfluxDB or other outputs.                                     |
| telly            | [Setup](https://github.com/Cloudbox/Community/wiki/Telly) | [tellytv/telly](https://hub.docker.com/r/tellytv/telly)      | IPTV proxy for Plex Live written in Golang. Makes IPTV appear as a TV tuner for Plex LiveTV and DVR functions. |
| thelounge        |  | [linuxserver/thelounge](https://hub.docker.com/r/linuxserver/thelounge) | web IRC client that you host on your own server              |
| transmissionvpn  |  | [haugene/transmission-openvpn](https://hub.docker.com/r/haugene/transmission-openvpn) | Torrent client with integrated VPN capabilities              |
| transmissionx    | [Setup](https://github.com/Cloudbox/Community/wiki/transmissionx) | [linuxserver/transmission](https://hub.docker.com/r/linuxserver/transmission) | lightweight torrent client - role to create multiple roles (default is one)               |
| ubooquity         | | [linuxserver/ubooquity](https://image.url) | Ubooquity is a free, lightweight and easy-to-use home server for your comics and ebooks. Use it to access your files from anywhere, with a tablet, an e-reader, a phone or a computer.                                     |
| unifi            |  | [linuxserver/unifi-controller](https://hub.docker.com/r/linuxserver/unifi-controller) | Software is a powerful, enterprise wireless software engine  ideal for high-density WiFi client deployments requiring low latency and high uptime performance |
| unmanic          |  | [josh5/unmanic](https://hub.docker.com/r/josh5/unmanic)      | Simple tool for optimising your video library to a single format |
| varken         | | [boerderij/varken](https://hub.docker.com/r/boerderij/varken) | Varken is a standalone command-line utility to aggregate data from the Plex ecosystem into InfluxDB                                     |
| vnstat           |  | [amarston/vnstat-dashboard](https://hub.docker.com/r/amarston/vnstat-dashboard) | Provides beautiful hourly, daily, and monthly network activity statistics |
| wallabag         | | [wallabag/wallabag](https://hub.docker.com/r/wallabag/wallabag) | Wallabag is a self hostable application for saving web pages. Unlike other services, wallabag is free (as in freedom) and open source.                                     |
| watchtower       |  | [containrrr/watchtower](https://hub.docker.com/r/containrrr/watchtower) | process for automating Docker container base image updates   |
| wordpress        | [Setup](https://github.com/Cloudbox/Community/wiki/Wordpress) | [wordpress](https://hub.docker.com/_/wordpress)              | The WordPress rich content management system can utilize plugins, widgets, and themes |
| xteve            |  | [dnsforge/xteve](https://hub.docker.com/r/dnsforge/xteve)    | xTeVe emulates a SiliconDust HDHomeRun OTA tuner, which allows it to  expose IPTV style channels to software, which would not normally support it |
| znc              | [Setup](https://github.com/Cloudbox/Community/wiki/ZNC) | [horjulf/docker-znc](https://hub.docker.com/r/horjulf/docker-znc) | IRC network bouncer or BNC                                   |


# Misc Guides

## General Stuff
- [Multiple Radarr/Sonarr/Lidarr/etc](/Cloudbox/Community/wiki/arrX "")
- [IPTV](/Cloudbox/Community/wiki/IPTV "")
- [NZBGet](/Cloudbox/Community/wiki/NZBGet "")
- [Varken](/Cloudbox/Community/wiki/Varken "")
- [Handy command list](/Cloudbox/Community/wiki/Handy-command-list "")
- [[Traktarr Tips]]

## Linux Stuff
- [Cloudbox Aliases](/Cloudbox/Community/wiki/Cloudbox-Aliases "")
- [User crontab example](/Cloudbox/Community/wiki/User-crontab-example "")

## Plex
- [Custom python plexlibrary libraries](/Cloudbox/Community/wiki/Custom-python-plexlibrary-libraries "")
- [Speed up Plex / Emby / Jellyfin](/Cloudbox/Community/wiki/Speed-up-Plex---Emby---Jellyfin "")
- [Tautulli Custom Scripts](/Cloudbox/Community/wiki/Tautulli-Custom-Scripts "")
- [Plex Scanners and Agents](/Cloudbox/Community/wiki/Plex-Scanners-and-Agents "")

## Organizr
- [[Organizr Auth for Nginx Proxy Apps|Organizr Auth for Nginx Proxy Apps]]

## Downloading
- [AMZN Release Method](/Cloudbox/Community/wiki/AMZN-Release-Method "")
- [Hardlinking Guide](/Cloudbox/Community/wiki/Hardlinking-Guide "")
- [Quality Release Groups](/Cloudbox/Community/wiki/Quality-Release-Groups "")
- [Silent's Naming Convention](/Cloudbox/Community/wiki/Silent's-Naming-Convention "")
- [Simple Renaming](/Cloudbox/Community/wiki/Simple-Renaming "")
- [Trakt Lists](/Cloudbox/Community/wiki/Trakt-Lists "")
- [YouTube Channels](/Cloudbox/Community/wiki/Downloading-YouTube-channels "")

## STRM
- [[Drive Strm]]