## Space filling up in `/mnt/local/` but not uploading?

**Check for any _unpack/ incomplete / broken download files using ncdu:**

`ncdu /mnt/local/downloads/nzbs/nzbget/complete` 

`ncdu /mnt/local/downloads/nzbs/nzbget/incomplete`

`ncdu /mnt/local/downloads/nzbs/sabnzbd/complete` 

`ncdu /mnt/local/downloads/nzbs/sabnzbd/incomplete`

Side note: if you're having consistent failed imports with Sonarr / Radarr due to poorly named files, consider using the cloudbox tag `scripts` to install a bunch of useful NZBGet extension scripts that help get your files in order. See the [[NZBGet]] section for more information on this.
***

**Check you are over the 200GB default upload amount:**

`ncdu /mnt/local/Media`
***

If all checks out...

**Quick solution:**
* `sudo systemctl restart cloudplow`
* Wait for next upload check to pass.

This option clears up lock-files located in `/opt/cloudplow/locks/`

**Manual solution:**
* `rm -rf /opt/cloudplow/locks/*`
* Optional step (start a manual upload to free up space) `cloudplow upload`
