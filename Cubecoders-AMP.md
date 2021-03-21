# Cubecoders AMP

AMP allows you to easily manage most of your game servers. A full list is available [HERE](https://github.com/CubeCoders/AMP/wiki/Supported-Applications-Compatibility)

The following have been tested and confirmed working inside this container. 
* McMyAdmin
* Minecraft Java Edition
* Minecraft Bedrock Edition
* srcds (GMod, TF2, ...)
* StarBound

## Install

* Visit this page: https://miniwebtool.com/mac-address-generator/
* Put 02:42:AC in as the prefix
* Choose the format with colons :
* Generate
* Copy the generated MAC and save it for the next step.


`cd ~/community`

`nano settings.yml`

Fill out `amp_license` and `amp_mac`

`sudo ansible-playbook community.yml --tags amp`

Navigate to https://amp.yourdomain.tld and follow the steps.  (Defaults)

Manually restart AMP
`docker restart amp-dockerized`


You're all set.

