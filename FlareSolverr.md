Helps Jackett resolve captchas for the trackers that require it.

https://github.com/FlareSolverr/FlareSolverr

## Setup

1. Run the role as a normal community role.
```
cd ~/community
sudo ansible-playbook community.yml --tags flaresolverr
```
2. In Jackett, locate the _FlareSolverr API URL_ setting, input `http://flaresolverr:8191` and apply the settings.