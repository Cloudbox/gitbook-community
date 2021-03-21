# **Ouroboros**
https://github.com/pyouroboros/ouroboros

Ouroboros will monitor (all or specified) running docker containers and update them to the (latest or tagged) available image in the remote registry.

## Install the role via:

`cd ~/community && sudo ansible-playbook community.yml --tags ouroboros`

The Ouroboros role will import ouroboros.env into /opt/ouroboros for persistent configuration via ENV variables. See https://github.com/pyouroboros/ouroboros/wiki/Usage for available variables. Default values populated by the role are:

```
SELF_UPDATE=true
CLEANUP=true
```