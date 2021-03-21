
Calibre and calibre-web are two different apps.

* [Calibre](https://calibre-ebook.com/) is the gold standard way to manage your ebook library. This is how you manage metadata, get covers, rename and properly organize the files. The database of your books in Calibre is used by Calibre-web.
  * Calibre does not acquire files, it manages files you already have. Look at Readarr or LazyLibrarian for download help.

* [Calibre-web](https://docs.linuxserver.io/images/docker-calibre-web) is the best way to display and serve your ebooks to yourself, friends, and family. Allows you to add users, and each user can set up a Kindle email address to have ebooks automatically sent to their Kindle reader or Kindle app. Users can also simply download epub, pdf, or whatever files you have. Requires an existing Calibre library database.

Calibre and Calibre-web do NOT need to be on the same server. But you do need to have a local copy of the Calibre `metadata.db` and a path to the books for calibre-web to operate (more info below).

> Note: CalibreRDP and Calibre are two different roles found in the Cloudbox Community. CalibreRDP is old, deprecated, and no longer updated. Calibre is the latest version that uses Guacamole as a front-end. If you are using CalibreRDP you should replace it with Calibre.

# Considerations before Install

Running Calibre on a headless server is not very fun. The web-based interface is slow, and there is a lag between every edit and seeing the results. If at all possible, run Calibre on your local, home computer.  Use rclone to sync the files from home to google drive, and then another sync from google drive to your server so that calibre-web can use it.  

A local database file is required.  This means you cannot run either Calibre or Calibre-web from a mounted teamdrive, and this is the biggest pain for many of us.  The easiest solution is to simply have your database and book files all located in `/mnt/local/Media/Books`.

Both Calibre and Calibre-web expect to find your library in `/mnt/unionfs/Media/Books`.  Note that per standard Cloudbox setup, /mnt/local is included inside /mnt/unionfs.  However, both dockers also include access to anything in your `/mnt` directory.

# Install Calibre

If you already have an existing Calibre library, you can copy it into `/mnt/local/Media/Books` before the install begins. If you don't do this before install, then Calibre will create a new, empty database for you.

You need to be on the Community develop branch. Run each line separately:

```shell
cd ~/community
git fetch
git checkout develop
git reset --hard @{u}
```

Install:

```shell
sudo ansible-playbook community.yml --tags calibre
```

When install completes successfully, go to the app:
`calibre.yourdomain.com`

Log-in with your regular cloudbox user name and password.

# Using Calibre

Calibre is ready for use. If you added your pre-existing Calibre library to  `/mnt/local/Media/Books` then you should see your library is ready to go. If not, then you have a blank library ready for you to fill. 

**Handy commands for managing your calibre docker:** 

You can access advanced features of the Guacamole remote desktop using ctrl+alt+shift enabling you to use remote copy/paste and different languages.

Shell access whilst the container is running:
* `docker exec -it calibre /bin/bash`

To monitor the logs of the container in realtime:
* `docker logs -f calibre`

Container version number:
* `docker inspect -f '{{ index .Config.Labels "build_version" }}' calibre`

Image version number:
* `docker inspect -f '{{ index .Config.Labels "build_version" }}' linuxserver/calibre`

# Install Calibre-web

Make sure you have at least one book in your Calibre library before continuing. 

Run this to install:

```shell
cd ~/community && sudo ansible-playbook community.yml --tags calibre-web
```

When install completes successfully, go to the app:
`books.yourdomain.com`

## Calibre-web Set-up

On the initial setup screen, you can either enter as your calibre library location `/books/name_of_library_folder`, replacing `name_of_library_folder` with the actual folder name (`/books` points to `/mnt/unionfs/Media/Books`), or you can use any location under `/mnt`.

**Default admin login:** Username: `admin` Password: `admin123` 
* Don't forget to change this first thing after set-up. 

**Unrar** is included by default and needs to be set in the Calibre-Web admin page (Basic Configuration:External Binaries) with a path of `/usr/bin/unrar`

**Automatic ebook conversion** via Calibre converter is included.  Enable it in the Calibre-Web admin page (Basic Configuration:External Binaries) by setting the Path to Calibre E-Book Converter to `/usr/bin/ebook-convert`

 The **kepubify ebook conversion tool** (MIT License) to convert epub to kepub is included. In the Calibre-Web admin page (Basic Configuration:External Binaries) set the Path to Kepubify E-Book Converter to `/usr/bin/kepubify`

 **Handy commands for managing your calibre-web docker:** 

You can access advanced features of the Guacamole remote desktop using ctrl+alt+shift enabling you to use remote copy/paste and different languages.

Shell access whilst the container is running:
* `docker exec -it calibre-web /bin/bash`

To monitor the logs of the container in realtime:
* `docker logs -f calibre-web`

Container version number:
* `docker inspect -f '{{ index .Config.Labels "build_version" }}' calibre-web`

Image version number:
* `docker inspect -f '{{ index .Config.Labels "build_version" }}' linuxserver/calibre-web`

# SK's Calibre-web Usage Tips

### SMTP Email Server Setup
A useful function of calibre-web is sending ebooks by email.  Therefore, you need to set up SMTP e-mail server settings. 

I am using Google to host the email for mydomain.com.  In my case, after trial and error, I found it most reliable to go into my Google control panel, go to the SMTP settings, and whitelist my server’s IP address without authentication.  Now, I can send email from any cloudbox app that supports it (Ombi, Tautelli, Organizr, and Calibre-web) with no troubles.

```
Hostname: smtp-relay.gmail.com, Port:  25,  SSL: No
```

### Kindle Setup
There is a nice benefit to using a Kindle.  When you send a “personal document” (book) to your Kindle account, it will automatically download to the specific device tied to the email address you use. Even though it’s called a document, it goes into your regular library and looks just like any book you may have purchased, including the cover.  In addition, that book is available on any other device or app tied to your account, so you can read the same book on your phone, a Kindle Paperwhite, and an iPad.  Amazon’s WhisperSync feature will bookmark your most recent page in the background, so if you switch devices it will ask if you want to update to the most recent page read.  

If you (or your users) want to have books sent directly to a Kindle from calibre-web email, then there are additional one-time setup steps for each user. 

* Tell Amazon to accept books sent from your website
    * Go to www.amazon.com
    * On the top navigation bar, go to Account & Lists.  In the dropdown, click on Your Content and Devices. 
    * Towards the top of the white section, in the middle, click on Preferences
    * Scroll down to Personal Document Settings. Click the title to open up that section of the page. 
    * Under Approved Personal Document E-mail List, click the link for "Add a new approved e-mail address"
    * In the popup, add `@yourdomain.com` and save.  Done!


  Before closing the website, you might want to grab your device email address for the next step.  Under the Send-to-Kindle E-Mail Settings, copy the email address where you want the books sent by default. 

* Add your Kindle email address to your profile on books.yourdomain.com
    * Once logged in, on the top ride side, click your name to open your profile
    * Add your kindle email address and save
    * Your Kindle email address will be something like name_79@kindle.com.  Every Kindle device and mobile app has its own unique address, however, you can send to any of your devices and it will still be available on all of them.  You can find this email address either in the Settings of the device/app, or copy it from the Devices page

Enjoy!

## Advanced Method of Library Storage

Since only the `metadata.db` file has to be local, you can keep the metadata.db file in `/mnt/local/Media/Books` as RW and the actual book files in `teamdrive:Books` as RO and mergerfs them together. Use the latest rclone `--vfs-cache-mode=full` and related cloud-seeding settings for your teamdrive mount so that it does not get laggy. Have a script that copies the metadata.db file regularly to the local disk, and leave the books in the cloud.

If this paragraph does not make sense to you, then please do not try it.