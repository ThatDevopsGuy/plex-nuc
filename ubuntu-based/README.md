# plex-nuc
Ansible configuration Management for Plex Home Theater on the Intel NUC, with an Apple remote.

## Execution

To use this, complete the following:

1. Install Ansible on a machine which can connect to the NUC.
2. Install Ubuntu Trusty server minimal install to the NUC (just need SSH and Python).
  * Ensure / is sda1
3. Checkout this repository on your Ansible machine (from step 1), and modify the 'user' variable in the playbook.
4. Ensure your NUC is addressable by 'nuc' (i.e. place it in /etc/hosts).
5. Run the playbook as follows:
  * `ansible-playbook -i hosts nuc-ubuntu1404.yml --ask-sudo-pass`

## What this does

This script will do the following:

* Mount point to use TRIM commands (`noatime,discard`)
* Write `bashrc` and `vimrc` files, and symlink them for 'root'
* Set the `sources.list` file to use Lease Web (a fast mirror) in a concise manner
* Add the PlexHT PPA repository
* Add the Intel graphics driver repository
* Upgrade all the installed packages
* Install a series of "basic" pacakges and `plexhometheater` (`vim`, `xorg`, `alsa`, etc...)
* Install some configuration files:
  * Apple remote `rc_keymap`
  * Intel graphics force VSYNC Xorg config
  * Modprobe for 'nuvotron' IR subsystem (so it starts)
  * IR-Keytable init script
  * A tty1 config to auto-login and start X
  * An `xinitrc` file to auto-start Plex when X starts
* Starts and enables the NTP and ir-keytable services

## What this does NOT do

This script does not:

* Configure passwords
* Set up Plex's preferences or logins
* Configures any firewall
* Configures updating