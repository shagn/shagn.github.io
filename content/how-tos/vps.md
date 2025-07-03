---
title: "VPS setup"
date: "2025-01-14"
tags: ["stub"]
draft: true
---

<!-- ## Secure SSH login

### Switch from password to public key authentication -->

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

...
