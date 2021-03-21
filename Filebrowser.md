![Filebrowser Logo](https://raw.githubusercontent.com/filebrowser/logo/master/banner.png)

### Introduction
[Filebrowser](https://filebrowser.xyz/) provides a file managing interface within a specified directory and it can be used to upload, delete, preview, rename and edit your files. It allows the creation of multiple users and each user can have its own directory. Through this community role, it provides access to the `/mnt/unionfs/` folder via web interface.

### Installation
1. First enter the community folder:
```bash
cd ~/community
```
2. Then run the Filebrowser role.
```bash
sudo ansible-playbook community.yml --tags filebrowser
```
3. Check `https://filebrowser.yourdomain.tld`. If cloudflare credentials are specified in your **cloudbox** `accounts.yml` file, you should see the filebrowser login page as below. If you don't use Cloudflare for DNS, set up the subdomain manually and wait until it propagates.
![Filebrowser Login](https://i.imgur.com/SXZ9y9h.png)
4. Login and change the default password and user.
```
user: admin
pass: admin
```