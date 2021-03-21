# Wordpress Installation
1. Edit the `~/community/settings.yml` and add:
```
wordpress:
  direct_domain: no
  subdomain: wordpress
```
You can change the subdomain to fit your own needs.

If direct_domain is enabled, then subdomain wont be created. 

2. Run the role as a normal community role.
```
cd ~/community
sudo ansible-playbook community.yml --tags wordpress
```

3. Visit the wordpress site at `https://wordpress.yourdomain.com` and the setup screen will appear.

4. No default user is configured until you run through the setup screen, so you should ideally run through setup as soon as wordpress is deployed to secure the site.