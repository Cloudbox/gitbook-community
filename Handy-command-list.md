## **Future video files**
Do you have video files which show up like they are in the future and therefore never leave the "latest added" list this command should be able to solve it for you, it sets the upload and created dates to the original available date instead of in the future.

**Fix added at wrong**

`sudo sqlite3 "/opt/plex/Library/Application Support/Plex Media Server/Plug-in Support/Databases/com.plexapp.plugins.library.db" "UPDATE metadata_items SET added_at = originally_available_at WHERE DATETIME(added_at) > DATETIME('now');"`

**Fix created at wrong**

`sudo sqlite3 "/opt/plex/Library/Application Support/Plex Media Server/Plug-in Support/Databases/com.plexapp.plugins.library.db" "UPDATE metadata_items SET created_at = originally_available_at WHERE DATETIME(created_at) > DATETIME('now');"`
