## Create JDownloader2 role

1. Run the jdownloader2 role as a normal community role.

    ```bash
    cd ~/community
    sudo ansible-playbook community.yml --tags jdownloader2
    ```
1. Go to your domain ( jdownloader2.yourdomain.com ), and login with your `htpasswd` if used, this should be pulled automatically from your preset passwords file.

1. Configure your myjdownloader account (Create at https://my.jdownloader.org/ if needed) and name your instance so you can connect via web or browser extensions. Use clipboard for two step copy and paste if needed. Note that some settings are only accessible via jdownloader2.yourdomain.com. Premium accounts such as mega.nz can be added via web interface.

1. Use manual import from sonarr / radarr and navigate to `/mnt/local/downloads/myjdownloader/output/` to import your files, note they must be already added for import to work.

1. See https://my.jdownloader.org/ for browser extensions and phone apps as desired.