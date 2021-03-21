# Apprise
Based on the https://hub.docker.com/r/caronc/apprise apprise API image.

As configured, the instance runs on the Docker network accessible to other containers at `http://apprise:8000` as well as via the reverse proxy at `http://apprise.domain.tld`. The configured username/password are taken from your Cloudbox `accounts.yml` file.