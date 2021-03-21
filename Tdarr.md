# Tdarr Beta - Audio/Video Library Analytics & Transcode/Remux Automation

> Tdarr is a self hosted web-app for automating media library transcode/remux management and making sure your files are exactly how you need them to be in terms of codecs/streams/containers etc. Designed to work alongside Sonarr/Radarr and built with the aim of modularisation, parallelisation and scalability, each library you add has its own transcode settings, filters and schedule. Workers can be fired up and closed down as necessary, and are split into 3 types - 'general', 'transcode' and 'health check'. Worker limits can be managed by the scheduler as well as manually.

_Ref: https://github.com/HaveAGitGat/Tdarr_

# Tdarr on Cloudbox
To utilize tdarr on Cloudbox you need the [community repo](https://github.com/Cloudbox/Community/wiki/Install). 
Once this is installed you may install tdarr by doing: 
```
cd ~/community
sudo ansible-playbook community.yml --tags tdarr
```

Tdarr can utilize transcoding to RAM by having the `/dev/shm/` inside the docker to be able to use. You may also utilize the mounts created by Cloudbox by `/mnt/` being mapped in side the docker as well.

# Any further questions.
For any further questions, comments or concerns you may utilize the Tdarr [Github](https://github.com/HaveAGitGat/Tdarr) or [Discord](https://discord.gg/GF8X8cq).


