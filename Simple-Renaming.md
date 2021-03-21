## A method to save you time when wanting to renaming content for Plex.
**Prerequisites:**

* [Google Drive File Stream](https://support.google.com/a/answer/7491144?hl=en) 
* [Total Commander](https://www.ghisler.com/) [Windows]
* [Double Commander](https://doublecmd.sourceforge.io/) [Windows, Mac OS X, Linux]
* [Plex_Autoscan](https://github.com/l3uddz/plex_autoscan) + Google Drive monitoring enabled.
***

### Google Drive File Stream
Install and enter your credentials into GDFS.\
Wait for initial GDFS cache build to finish, this can take several minutes depending on the amount of files you have.

### Total Commander.
1. Navigate to your Google Drive letter and folder where items you want to rename are located.
2. Click `Show all files in current dir and all subdirs`.
3. Ctrl + A to select all. Use one file to test.
4. Click `Rename multiple files`, or Ctrl + M.
5. Put whatever quality you want to change in the `Search For` section and whatever you want to replace it with in the `Replace with` section. See screenshot below for example.

![](https://i.imgur.com/tgGGsLR.png)

6. Once you are positive you've got the naming right, click `Start`.

### Double Commander
1. Navigate to your Google Drive letter and folder where items you want to rename are located.
2. Press Ctrl + B to flatten all directories; this will show all files in subdirectories.
3. Press Ctrl + A to select all files.
4. Press Ctrl + M to open Multi Rename Tool.
5. Put whatever quality you want to change in the `Find...` section and whatever you want to replace it with in the `Replace...` section. See screenshot below for example.
![](https://i.imgur.com/Z5DnlvD.jpg)
6. Once you are positive you've got the naming right, click `Rename`.

### Plex_Autoscan
1. Wait for changes to sync to Google Drive. Click the GDFS icon to see what stage you are at. It will say `Syncing X files...` 8K files took around 10 minutes.
2. Plexdrive will update its cache on it's own automatically
3. Gdrive monitoring in PAS will start adding scans to the queue automatically.
4. Done! 