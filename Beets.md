Beets is a music tagger and library manager. It uses the MusicBrainz database and has many options for tagging and sorting music. It is used via the command line but does have a web interface for browsing your music library.

# **Install Beets**

1. `cd ~/community`
2. `sudo ansible-playbook community.yml --tags beets`
# **Accessing Beets Web**

To access Beets at https://beets.yourdomain.com

The password and username should be automatically set to the ones used for Cloudbox.

# **Auto Import**

When the role is run, a cron job is set to automatically import any music found at `/mnt/local/downloads/music` every hour. If a match is under 95% beets will skip the file and it will need manual importing.

# **Manual Import**

To run a manual import (which will help correct any matches under 95%) run the following command:

    rm /opt/beets/state.pickle && docker exec -it beets /bin/bash -c 'beet import /downloads'

# **Folder Structure Change**

If you want to change the folder structure you should do so in the config file located at /opt/beets/config.yaml

[This link details the allowed options ](https://beets.readthedocs.io/en/v1.4.7/reference/config.html#path-format-configuration)

If you already have imported music you will need to run an import using the following command:

    docker exec -it beets /bin/bash -c 'beet import /music'




