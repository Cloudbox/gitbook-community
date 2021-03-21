#Invoice Ninja
1. Edit the `settings.yml` and add:
```
invoiceninja:
   subdomain: invoiceninja
```
You can change the subdomain to fit your own needs.

2. Run the role as a normal community role.
```
cd ~/community
sudo ansible-playbook community.yml --tags invoiceninja
```

3. Visit the invoice ninja site at `https://invoiceninja.yourdomain.com` and the setup screen will appear.

Make the following changes on the setup page:
* Check the checkbox that says "HTTPS Required" (this will be automatically checked in future revisions).
* Select the "Test Connection" button under mysql. It should come back with **Success**
* Fill in your email server information **Optional**
* Update the Firstname, Lastname, Email and Password
* Agree to the Terms of Service
* Agree to the Privacy Policy
* Hit **Submit**

***

* Log into Invoice Ninja

***

* You will see an error on the screen:

`Error: APP_KEY is set to a default value, to update it backup your database and then run php artisan ninja:update-key`

* Go to the shell and run this:
`docker exec -ti invoiceninja sh -c "php artisan config:clear && php artisan key:generate && php artisan config:cache && php artisan config:clear"`

* You will be prompted to run the command. Answer 'yes'

* You will see several 'Success' messages.

* Go back to the Invoice Ninja website, refresh the browser.
* Log back in and the error message is gone. You can begin to use Invoice Ninja now.

Cron: It is set to send invoices and reminders daily at 8am server time. There are logs in the /opt/invoiceninja/logs/cron directory.