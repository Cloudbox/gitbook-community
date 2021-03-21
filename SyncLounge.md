# SyncLounge - Enjoy Plex with your friends. In Sync. Together. 

![SyncLounge](https://camo.githubusercontent.com/a410a18406f6ff94abfd7c527f53a6d6e83384d7/68747470733a2f2f73796e636c6f756e67652e74762f6173736574732f696d672f534c5f4c4f474f5f383030783230305f4441524b2e706e67)

## Basic Install (may require develop branch until merged on master)

```
cd ~/community
sudo ansible-playbook community.yml --tags synclounge
```

## Custom Domain Install

```
cd ~/community
nano settings.yml
```
Enter your subdomain/domain name you wish to use with synclounge. This will become subdomain.youralternatedomain.tld
```
synclounge:
  domain: youralternatedomain.tld
  subdomain: synclounge
```

Then run
```
sudo ansible-playbook community.yml --tags synclounge
```
If you wish to use your default CloudBox domain name simply leave this setting empty.

## Configuration

Please note that synclounge works directly out of the box without further configurations. SyncLounge does support server autojoin however that feature is currently broken upstream and does not work.

## How to use SyncLounge with your server

Visit https://synclounge.yourdomain.tld
Login to your plex account on the screen
On the server selection screen you will be presented with 4 options (AU, EU, US and Custom)
Select Custom and enter the following address https://synclounge.yourdomain.tld/slserver

## Delay
Please note that when SyncLounge first starts up it does take considerable time for it to become available via the web interface. Error 502 will occur if it hasn't loaded fully.

