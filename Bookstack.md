#Bookstack
1. Edit the `settings.yml` and add:
```
bookstack:
   subdomain: bookstack
```
You can change the subdomain to fit your own needs.

2. Run the role as a normal community role.
```
cd ~/community
sudo ansible-playbook community.yml --tags bookstack
```

3. Visit the bookstack site at `https://bookstack.yourdomain.com` and login with:
```
username: admin@admin.com
password: password
```