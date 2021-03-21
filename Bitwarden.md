## Bitwarden

This community role installs a [Bitwarden](https://bitwarden.com/) server utilizing the [bitwardenrs/server](https://hub.docker.com/r/bitwardenrs/server) docker image.

Run the role as a normal community role.

1. `cd ~/community`

2. `sudo ansible-playbook community.yml --tags bitwarden`

Visit the bitwarden site at https://bitwarden.yourdomain.tld

Sign up with any email address and password.

To access the Admin Panel go to https://bitwarden.yourdomain.ltd/admin.

You will need to enter an authentication key which you can find in /opt/bitwarden/env. Look for ADMIN_TOKEN=. 