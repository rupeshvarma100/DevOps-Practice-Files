Problem :


Solution :

thor@jumphost ~$ ssh natasha@172.16.238.15

[natasha@ststor01 ~]$ cd /usr/src/kodekloudrepos/apps

[natasha@ststor01 apps]$ git status
fatal: detected dubious ownership in repository at '/usr/src/kodekloudrepos/apps'
To add an exception for this directory, call:

        git config --global --add safe.directory /usr/src/kodekloudrepos/apps

[natasha@ststor01 apps]$ git config --global --add safe.directory /usr/src/kodekloudrepos/apps

[natasha@ststor01 apps]$ git statusOn branch xfusioncorp_apps
nothing to commit, working tree clean

[natasha@ststor01 apps]$ git branch -a
  master
* xfusioncorp_apps
  remotes/origin/master

[natasha@ststor01 apps]$ sudo git switch master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

[natasha@ststor01 apps]$ git branch -a
* master
  xfusioncorp_apps
  remotes/origin/master

[natasha@ststor01 apps]$ sudo git branch -D xfusioncorp_apps

Deleted branch xfusioncorp_apps (was e6fa606).

[natasha@ststor01 apps]$ git branch -a
* master
  remotes/origin/master
