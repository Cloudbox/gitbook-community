### Would you like a personal Discord bot for you and your users to request new content?
Follow these steps...

**DISCLAIMER: Ombi is the only supported platform right now. Sonarr + Radarr + Tautulli support to come later.**

**AS OF JANUARY 31ST, 2020: Sonarr and Radarr are both fully supported for searching and adding new content. Please switch to the new `develop` branch or tag.**

***


1. `cd ~/community`
2. `sudo ansible-playbook community.yml --tags mellow`
3. Navigate to https://mellow.domain.com (username: `mellow` password `default`)
4. Set up administrator username + password.
5. Go to [this link and log into Discord.](https://discordapp.com/developers/applications/)
6. Create a `New Application`.
7. Copy the `Client ID` to Mellow bot settings under `Owner ID`.
7. Go to Bot tab, create a bot.
8. Click on `Reveal Token`. Copy that to Mellow bot settings under `Token`.
9. Under `Bot Settings`, add `!` as the `Command Prefix` 
10. Add Ombi | Tautulli | Sonarr | Radarr host settings as normal. Example below for standard `ombi` role. Please note that the screen shot shows a non standard port, cloudbox default is **3579** if that doesn't work try port **5000**.
  
![](https://i.imgur.com/TrqooB8.png)

11. Open new web browser tab. Replace `Client ID` in the following link with your bot's client ID and click link.
    ```
    https://discordapp.com/oauth2/authorize?client_id=CLIENTID&scope=bot
    ```
12. Invite bot to your Discord server and give the appropriate permissions (select everything under text).
13. Test out bot using `!help` in a public channel (not private message).