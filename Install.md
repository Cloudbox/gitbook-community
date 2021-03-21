Installs the Cloudbox Community repository for extended functionality.

**NOTE: It is assumed that you already have Cloudbox installed and configured.**

## Install / Update Community Repo

Run the following commands:

```bash
cd ~/cloudbox; git fetch &> /dev/null; git reset --hard @{u} &> /dev/null; sudo ansible-playbook cloudbox.yml --tags community
```

This will clone the repo into `/opt/community`, symlink the folder to `~/community`, and add the necessary `vault_password_file` line to `/opt/community/ansible.cfg`.  

## Change / Update branches

### master branch

```bash
cd ~/community; git fetch &> /dev/null; git checkout master &> /dev/null; git reset --hard @{u} &> /dev/null
```

### develop branch


```bash
cd ~/community; git fetch &> /dev/null; git checkout develop &> /dev/null; git reset --hard @{u} &> /dev/null
```
You can use the Develop branch of Community even if you are using the Master branch of Cloudbox.  The Develop branch will have the latest new additions and edits, but some roles could be untested.


## Installing individual apps, or "tags"

Once the setup has been done as described above, This works in the same way as Cloudbox itself:

```bash
cd ~/community && sudo ansible-playbook community.yml --tags "TAG"
```