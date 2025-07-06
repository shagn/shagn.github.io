---
title: "VPS setup"
date: "2025-01-14"
tags: ["stub"]
draft: true
---

## Secure SSH login

### Switch from password to public key authentication

Prerequisite: a key-pair (use `ssh-keygen` to create one if necessary), for this example `id_vps.pub`

1. Copy public key to server with `ssh-copy-id -i id_vps.pub user@123.45.678.9`

1. Test connection via puplic key authentication: `ssh user@123.45.678.9 -i ~/.ssh/id_vps`

1. Disable password authentication in the configuration

   - Make sure in _/etc/ssh/sshd_config_ `PasswordAuthentication no` is set
   - Additionally see if other configuration files are included which potentially can overwrite parameters

1. Restart the ssh daemon: `sudo service ssh restart`

1. Test connection via password does not work

### Prevent Brute-Force attacks

#### Failban

https://github.com/fail2ban/fail2ban/wiki/How-to-install-fail2ban-packages

##### Installation

```bash
# on Ubuntu
sudo apt update
sudo apt install fail2ban
```

##### (Auto)Start

```bash
sudo systemctl start fail2ban
# enable start with system:
sudo systemctl enable fail2ban
```

##### Configuration

The default configuration is stored at `/etc/fail2ban/jail.conf` and can be overwritten by a `/etc/fail2ban/jail.local` configuration, e.g. increasing the default bantime:

```
[DEFAULT]
bantime = 2h
```

Restart fail2ban to load configuration: `systemctl restart fail2ban`

##### Checking status/logs

```bash
# checking current jails
fail2ban-client status

# checking logs
less /var/log/fail2ban.log
```

Source: [IONOS Guide (German)](https://www.ionos.de/hilfe/sicherheit/dedicated-server/server-absichern-mit-fail2ban/)

## Security updates

### unattended-upgrades

```bash
# install it
sudo apt install unattended-upgrades

# main configuration lives at, check if security updates are not commented out
/etc/apt/apt.conf.d/50unattended-upgrades

# there are two configs
# config for periodic updates
cat /etc/apt/apt.conf.d/20auto-upgrades

# both configs will be merged, so to check the outcome use `sudo apt-config dump | grep Periodic`

## how to check if the setup is correct
    1. check config for APT::Periodic::Unattended-Upgrade "1";
    2. check /etc/apt/apt.conf.d/50unattended-upgrades shows allowed origins
    3. check systemctl status apt-daily-upgrade.timer shows something like `Active: active (waiting)`
    4. check logs e.g. with `journalctl -u unattended-upgrades.service`if it has been executed

    Hierzu muss die Datei /etc/apt/apt.conf.d/50unattended-upgrades um folgenden Inhalt ergänzt werden.
Unattended-Upgrade::Origins-Pattern {
    "origin=*";
};
Dies sorgt dafür, dass alle Pakete aus allen Quellen (auch Fremdquellen und PPAs) automatisch installiert werden.
(see https://wiki.ubuntuusers.de/Aktualisierungen/Konfiguration/#unattended-upgrades)
```

## Containers applications

<!-- - docker
- portainer
- watchtower -->

...
