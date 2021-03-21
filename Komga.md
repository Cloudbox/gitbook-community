# Installation
1. `cd ~/community`
2. `sudo ansible-playbook community.yml --tags komga`

# Setup
## Create User Account
1. Navigate to https://komga.yourdomain.com
2. You will be asked to create a user account. Choose an email and password, then click on Create User Account.
## Storage
* Komga expects comics to be stored in `/mnt/unionfs/Media/Comics` which is `/comics` on the container. 
* `/mnt` is accessible to the container as well. 
# Further Documentation
* Please see the projects website for further documentation at https://komga.org/guides/#an-introduction 
# Source Code
* https://github.com/gotson/komga