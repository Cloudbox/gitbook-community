You can add some handy Cloudbox or Community ansible playbook aliases to your Shell.
# Cloudbox:
Check your shell type by typing `echo $SHELL`. 

## Bash

Edit .bashrc with `nano ~/.bashrc` and add the following:

```shell
# cloudbox aliases
cloudbox() {
  cd ~/cloudbox/;
  sudo ansible-playbook cloudbox.yml --tags $1;
  cd -;
}
cloudbox-list() {
  cd ~/cloudbox/;
  sudo ansible-playbook cloudbox.yml --list-tags;
  cd -;
}
cloudbox-update() {
  curl -s https://cloudbox.works/scripts/dep.sh | sudo -H sh; 
  curl -s https://cloudbox.works/scripts/repo.sh | bash;
  cd ~/cloudbox/;
  sudo ansible-playbook cloudbox.yml --tags cloudbox;
  cd -;
}
```

Save and exit nano by pressing Ctrl+X, and then run `source ~/.bashrc` to make the aliases available.

Now you can run `cloudbox-list` to see a list of all available tags or you can run `cloudbox radarr` to install or update radarr.


## Zsh

Edit .zshrc with `nano ~/.zshrc` and add the following:

```shell
# cloudbox aliases
cloudbox() {
  cd ~/cloudbox/;
  sudo ansible-playbook cloudbox.yml --tags $1;
  cd -;
}
cloudbox-list() {
  cd ~/cloudbox/;
  sudo ansible-playbook cloudbox.yml --list-tags;
  cd -;
}
cloudbox-update() {
  curl -s https://cloudbox.works/scripts/dep.sh | sudo -H sh; 
  curl -s https://cloudbox.works/scripts/repo.sh | bash;
  cd ~/cloudbox/;
  sudo ansible-playbook cloudbox.yml --tags cloudbox;
  cd -;
}
```

Save and exit nano by pressing Ctrl+X, and then run `source ~/.zshrc` to make the aliases available.

Now you can run `cloudbox-list` to see a list of all available tags or you can run `cloudbox radarr` to install or update Radarr.

# Community:
Check your shell type by typing `echo $SHELL`. 
## Bash

Edit .bashrc with `nano ~/.bashrc` and add the following:

```shell
# community aliases
community() {
  cd ~/community/;
  sudo ansible-playbook community.yml --tags $1;
  cd -;
}
community-list() {
  cd ~/community/;
  sudo ansible-playbook community.yml --list-tags;
  cd -;
}
community-update() {
  curl -s https://cloudbox.works/scripts/dep.sh | sudo -H sh;
  curl -s https://cloudbox.works/scripts/repo.sh | bash;
  cd ~/cloudbox/;
  sudo ansible-playbook cloudbox.yml --tags community;
  cd -;
}
```
Save and exit nano by pressing Ctrl+X, and then run `source ~/.bashrc` to make the aliases available.

Now you can run `community-list` to see a list of all available tags or you can run `community radarrx` to install or update radarrx.

## Zsh

Edit .zshrc with `nano ~/.zshrc` and add the following:

```shell
# community aliases
community() {
  cd ~/community/;
  sudo ansible-playbook community.yml --tags $1;
  cd -;
}
community-list() {
  cd ~/community/;
  sudo ansible-playbook community.yml --list-tags;
  cd -;
}
community-update() {
  curl -s https://cloudbox.works/scripts/dep.sh | sudo -H sh;
  curl -s https://cloudbox.works/scripts/repo.sh | bash;
  cd ~/cloudbox/;
  sudo ansible-playbook cloudbox.yml --tags community;
  cd -;
}
```
Save and exit nano by pressing Ctrl+X, and then run `source ~/.zshrc` to make the aliases available.

Now you can run `community-list` to see a list of all available tags or you can run `community radarrx` to install or update RadarrX.

## Other useful aliases

To edit/add; `nano ~/.bash_aliases` followed by Ctrl+X to save and exit.

```shell
#mkcd
mkcd ()
{
  mkdir -p -- "$1" && cd -P -- "$1"
}

#fail2ban log summary
f2blog() {
  sudo awk '($(NF-1) = /Ban/){print $NF,"("$NF")"}' /var/log/fail2ban.log* | sort | logresolve | uniq -c | sort -n
}

#lets encrypt docker domain certificates
lehosts() {
  docker inspect $(docker ps -q)  | grep -e "LETSENCRYPT_HOST" | sed 's/ *"LETSENCRYPT_HOST=\(.*\)",/\1/' | sort | uniq
}

#docker status
alias dstatus="docker ps -a --format=\"table {{.Names}}\t{{.Image}}\t{{.Status}}\t{{.Ports}}\" | sed -r 's/(127|0)\.0\.0\.[01]:[0-9\-]+->//g'"

#local disk usage excluding gdrive
alias dusage="ncdu -x / --exclude /mnt/remote/ --exclude /mnt/unifonfs/ --exclude /lost+found"

#general cloudbox aliases
alias cplog="tail -n 50 -F /opt/cloudplow/cloudplow.log | awk '{\$3=\$4=\$5=\$6=\$7=\$8=\$9=\"\"; print \$0}'"
alias paslog="tail /opt/plex_autoscan/plex_autoscan.log -f -n 50"
alias lerenew="docker exec letsencrypt /app/force_renew"

alias bulog="tail -n 22 ~/logs/cloudbox_backup.log"
```

To enable this you will have to perform a `source ~/.bashrc`.
Edit as required to suite your needs.
