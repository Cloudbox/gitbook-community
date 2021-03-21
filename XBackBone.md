https://github.com/SergiX44/XBackBone

https://github.com/Pe46dro/XBackBone-docker

# XBackBone
XBackBone is a simple, self-hosted, lightweight PHP file manager that support the instant sharing tool ShareX and *NIX systems. It supports uploading and displaying images, GIF, video, code, formatted text, and file downloading and uploading. Also have a web UI with multi user management, past uploads history and search support.



# Install

`cd ~/community`

`nano settings.yml`

Set your maxupload and storage location.   
There's currently a bug preventing uploads longer than 30 seconds from completing.  
[XBackBone Issue](https://github.com/SergiX44/XBackBone/issues/157)

`sudo ansible-playbook community.yml --tags xbackbone`

Visit https://xbackbone.yourdomain.tld 

Login info: admin:admin





## Configuring ShareX Uploads

Make sure you have ShareX installed.  Download the config file shown below and it will automatically configure ShareX for you.   
![https://imgur.com/3xVlzdg](https://i.imgur.com/3xVlzdg.png)