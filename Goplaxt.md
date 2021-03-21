## Goplaxt -- https://github.com/XanderStrike/goplaxt

1. Create an API application through Trakt [here](https://trakt.tv/oauth/applications). The Redirect URI should be your 
   goplaxt.domain + `/authorize`, so it reads as: `https://goplaxt.domain.com/authorize`. 

2. Edit `settings.yml` and add the trakt api info:

   ```
   goplaxt:
      trakt_id: IDHERE
      trakt_secret: SECRETHERE
   ```

3. Run the role as a normal community role.
   ```bash
   cd ~/community
   sudo ansible-playbook community.yml --tags goplaxt
   ```

4. Visit the goplaxt site at `https://goplaxt.domain.com`. Enter your Plex Username and Authorize, and add the Webhook in 
   Plex Settings. Make sure under your server Settings > Network that Webhooks is enabled.