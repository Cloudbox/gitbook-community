# Contributing a new role:

## Preparatory work:

Start by making your own fork of the community repo by clicking on the "Fork" button up and to the right.

This will take you to your own copy of the community repo.

On your development machine [which should probably be a machine running cloudbox, as it makes things easier with regard to testing]:

1. clone your community fork:

     `git clone https://github.com/YOURNAMEHERE/Community.git community`
1. go into that local community dir:

     `cd community`
1. switch to develop branch:

     `git checkout develop`
1. make sure your local repo is up-to-date:

     `git pull`
1. create your feature branch:

     `git checkout -b my-cool-role`

You switch to develop branch before creating your branch because you want it based on develop, not master.

## Creating a role:

Now you're ready to start work on your new role.

A good starting point is to find a role that is similar to the one you want to add and use it as a starting point.  For example, if your container requires mariadb and you want to create a database during setup, bookstack does that.

1. copy the "starting point" role to your role:

     `cp -R roles/bookstack roles/my-cool-role`

[of course, substitute whatever role you're using as your prototype for "bookstack"]
 
Next step is to create the role.  At a minimum, you will need to modify:

```
roles/my-cool-role/tasks/main.yml
appveyor.yml
community.yml
```

There may be other things required; there may be templates or sub-tasks or what have you.  Those three files are the **absolute bare minimum** that would need to be created to add a new role.

## Editing an existing role:

If you want to make a change to an existing role [for example, changing the docker image it uses], you don't have [or want to] to create a new role.  You just need to edit the existing role file.  There are no changes required in `appveyor.yml` or `community.yml`.

### What are those things?

```
roles/my-cool-role/tasks/main.yml
```

This is the file that drives the install of your role.  The stuff in there should be self-explanatory or understandable with comparisons to existing roles; if it's not, then with all respect you probably shouldn't be creating a role right now.

There is a wiki article on adding new containers [here](https://github.com/Cloudbox/Cloudbox/wiki/Add-Your-Own-Docker-Container-Into-Cloudbox); this may be of some use.

Don't forget the header:

```
#########################################################################
# Title:            Community: MY COOL ROLE                             #
# Author(s):        YOUR NAME HERE                                      #
# URL:              https://github.com/Cloudbox/Community               #
# Docker Image(s):  SOMEBODY/IMAGENAME                                  #
# --                                                                    #
#         Part of the Cloudbox project: https://cloudbox.works          #
#########################################################################
#                   GNU General Public License v3.0                     #
#########################################################################
```

Be sure you edit this to reflect your role, name, and image

```
appveyor.yml
```

This file drives the automated testing system.  It's a simple file, and again, it should be glaringly obvious what needs to be added for a new role.

```
community.yml
```

This file drives the ansible install system by providing the valid tags that you can use with:

`cd ~/community && sudo ansible-playbook community.yml --tags "TAG"`

Again, it's a simple file, and it should be quite apparent what needs to be added for a new role.

**BE SURE TO TEST YOUR ROLE.**

You want to make sure that your role works, so be sure you run it several times.  Run it on fresh installs, reinstalls, enlist someone else to run it for you.  The point of doing this is to add something to community for others to use; if you don't verify that it works, why are you doing it?

## Creating the Pull Request:

Now it's complete, and tested, and you want it to be added to community for other users to enjoy.

First, commit your changes to your fork.

**BE SURE YOU DO NOT COMMIT FILES CONTAINING SECRETS LIKE API KEYS OR TOKENS.**

This will involve adding the files you changed or added and doing a `git commit` and `git push`.

This is standard git stuff, and again, with all respect, if you don't know these git basics you probably shouldn't be creating a role right now.

### Pull Request:

Back at github.com, create a pull request against the "develop" branch of the community repo.

You do this by switching to your feature branch in your repo and clicking "Pull request" at the top where it says something like:
`This branch is 2 commits ahead of Cloudbox:develop.`

This is a request for the Cloudbox team to "pull" your changes into their repo.  New roles like this should be created against `develop`, not `master`.

If there are special instructions or details that your role needs, add them to the pull request comments.  If needed, create a wiki page for the role.

**BE SURE YOU DO NOT COMMIT FILES CONTAINING SECRETS LIKE API KEYS OR TOKENS.**

Your pull request will be reviewed eventually, and may generate comments or change requests.

You can address those change requests by making further commits to your feature branch; they will automatically be added to this pull request.

Eventually, if deemed a good or just reasonable fit, your pull request will be accepted and it will appear in the source community repo.  Some time after that, it may get merged over to the `master` branch.