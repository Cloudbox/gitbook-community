[docker-rdp-calibre](https://github.com/aptalca/docker-rdp-calibre) (by aptalca) is an app that runs a calibre instance and makes it accessible in a web browser. We will be using a fork created by cgspeck (https://github.com/cgspeck/docker-rdp-calibre) to provide us with a specific library path and proper permissions with User/Group IDs.

[docker-calibre-web](https://github.com/janeczku/calibre-web) (by janeczku) is a web app providing a clean interface for browsing, reading and downloading eBooks using an existing Calibre database.

# **Installing Calibre RDP**
1.  Check the **Books Folder** Exists at Media/Books - create this prior to running the script. You can either transfer 
    your existing calibre library to Media/Books (the book folders and metadata.db) or start with a new one.
1. `cd ~/community`

1. The Role has the below values pre-configured, change as needed:
   (`nano ~/community/roles/calibre-rdp/tasks/main.yml`)

   - **Subdomain Record** `"calibrerdp.{{domain}}"` - Default will be accessible via calibrerdp.yourdomain.com

   - **Time Zone Locale** `TZ: "America/New_York"`

   - **Automatic Calibre Updates** Change the Edge Variable from 0 to 1 and latest version of calibre is installed on restart.

     ```
     EDGE: "1"
     ```

   - **Content Server** If you want to use the Calibre Content Server, expose port 8081 (will access via yourip:8081) by 
     changing the published ports to 
    
     ```
     published_ports:
       - "127.0.0.1:8080:8080"
       - "0.0.0.0:8081:8081"
     ```

3. Run the following command: 

   ```
   sudo ansible-playbook community.yml --tags calibre-rdp
   ```


4. Go to your domain (calibrerdp.yourdomain.com), and login with your htpasswd if used.

5. On the initial screen, click 'OK'

    [![](https://i.imgur.com/I9INcyx.png)](https://i.imgur.com/I9INcyx.png)

6. If you moved over an existing calibre library to Media/Books, on the next screen click cancel, and your library should load. You are done! If creating a new library, click next.

    [![](https://i.imgur.com/Irf57NT.png)](https://i.imgur.com/Irf57NT.png)

7. You can select your e-book device, and click next.

    [![](https://i.imgur.com/Y1jADl4.png)](https://i.imgur.com/Y1jADl4.png)

8. If using a Kindle or Amazon device you can then set the calibre email settings, click next once done:

    [![](https://i.imgur.com/18Cr2gQ.png)](https://i.imgur.com/18Cr2gQ.png)

    If you don't know your Kindle Email:

    1. Go to [Manage Your Content and Devices](https://www.amazon.com/mycd).

    1. From **Settings**, scroll down to **Personal Document Settings**.

    1. Under **Send-to-Kindle Email Settings**, your Send to Kindle email address will be listed.

9. You are done! You should now see this screen, and can click finish:

    [![](https://i.imgur.com/F8YOMFE.png)](https://i.imgur.com/F8YOMFE.png)

10. If you wanted to use the Content Server, go to Preferences > Sharing Over the Net and change the port to 8081 and apply - will need a restart via `docker restart calibrerdp`

    [![](https://i.imgur.com/rAgSMWg.png)](https://i.imgur.com/rAgSMWg.png)
    
11. If you want to install Calibre Web, `cd ~/community`
12. `sudo ansible-playbook community.yml --tags calibre-web
`
22. Go to your domain (books.yourdomain.com) and set your calibre database location to /books
    [![](https://i.imgur.com/AsVfRNA.png)](https://i.imgur.com/AsVfRNA.png)

23. Under "External Binaries" set the Location of Unrar binary to `/usr/bin/unrar` 

24. For converting e-books [Untested currently]:

    -For the option **Use Kindlegen** set the Path to convertertool to `/calibre-web/app/vendor/kindlegen`
      and at About you will see then kindlegen Amazon kindlegen(Linux) V2.9 build 1028-0897292

    -For the option **Use calibre's ebook converter** ([recommended](https://github.com/janeczku/calibre-web/issues/730)) set the Path to convertertool to `/usr/bin/ebook-convert`

    [![](https://i.ibb.co/4YF3LCW/image.png)](https://i.ibb.co/4YF3LCW/image.png)

25. Hit Submit then Login.
    Default admin login:
    ```
    Username: admin
    Password: admin123
    ```
    After successful login change the default password and set the email address.

