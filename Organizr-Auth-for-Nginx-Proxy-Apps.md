_You search to secure your applications without configure them one by one and use a central method ?_

If you use Organizr, you can add instructions to nginx-proxy config to use authentication of Organizr app.

> More information about ServerAuth feature provided by Organizr: https://docs.organizr.app/books/setup-features/page/serverauth

## Create a new file within the following directory:

`cd /opt/nginx-proxy/vhost.d`

## Name the file according the following by replacing domain & app name:

`nano appname.my-domain.com_location`

_e.g. sonarr.my-domain.com_location_

## Add these block in content of file just created

_e.g. for Sonarr app_

**Update 11/16/2020 for v2**

```
## Auth block - Organizr ##
location ~ ^/auth-(.*) {
    ## Has to be local ip or local DNS name
    proxy_pass http://organizr:80/api/v2/auth?group=$1;
    proxy_pass_request_body off;
    proxy_set_header Content-Length "";

}

## Auth request for app  - Sonarr ##
auth_request /auth-0; # 0 mean admin level minimum to access
location /api { # We know that sonarr's api-endpoint is /api, so we are gonna open that up.
    auth_request off; # The line that actually opens it up
    proxy_pass http://sonarr:8989/api; # We need to tell nginx where to send the request
}
```

> You can retrieve more examples of nginx-proxy block for many apps here: https://github.com/organizrTools/Config-Collections-for-Nginx/tree/master/Apps if you want optimisation :)

_**NB:** Don't forget to remove "/appname" in location directive as it's directly under a subdomain with Cloudbox._

## Apply modifications ##

You need now to restart nginx-proxy & your app container to apply these modifications.

`docker restart nginx-proxy appname`

e.g. `docker restart nginx-proxy sonarr`

_You can now test it by using private browsing, access your app directly, you will be denied by a forbidden message, login in organizr and return to your app, access will now be allowed._

**Enjoy it :)**

## Bypass Internal App Authentication ##

For any apps that have their own authentication using HTTP Basic Auth (username/password popup in browser, not in form) you can configure nginx-proxy to inject authorization headers. This allows the app itself to be secured behind a username/password if somehow it were to be accessed directly and not through the reverse proxy while avoiding double authentication annoyances.

In `/opt/nginx-proxy/vhost.d/sub.domain.tld_location`
```
proxy_set_header Authorization "Basic <encodedtoken>";
proxy_pass_header Authorization;
```
Where `<encodedtoken>` is Base64 encoded `user:pass`. i.e. for `seed:seed` the token would be `c2VlZDpzZWVk`.