# alltube - HTML GUI for youtube-dl 
Currently requires **Develop** branch of community.
![alltube](https://github.com/Rudloff/alltube/raw/master/img/screenshot.png)

## Basic Install 

```
cd ~/community
sudo ansible-playbook community.yml --tags alltube
```

## Custom Domain Install

```
cd ~/community
nano settings.yml
```
Enter your domain name you wish to use with alltube. This will become alltube.youralternatedomain.tld
```
alltube:
  domain: youralternatedomain.tld
```

Then run
```
sudo ansible-playbook community.yml --tags alltube
```
If you wish to use your default CloudBox domain name simply leave this setting empty.

## Configuration

Please note that alltube works directly out of the box without further configurations however there are many options available. If you wish to use a custom configuration you can simply copy the example and change it for your needs and restart the container.

```
cd /opt/alltube
cp config.example.yml config.yml
nano config.yml
```

