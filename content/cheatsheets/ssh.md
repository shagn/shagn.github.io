---
title: "ssh" 
date: "2025-07-06" 
tags: ["stub"]
---

### ssh config

```bash
Host vps
    HostName 123.45.678.9
    User root
    IdentityFile ~/.ssh/id_vps # 
    AddKeysToAgent yes  # automatically adds the key to the running agent
    UseKeychain yes # stores the passphrase in the macOS Keychain
    ServerAliveInterval 60 # send keep-alive signal every 60 s (disabled by default)
```

Show the settings for a host

```bash
ssh -G vps
```

## ssh-keygen

### Generating new key pair

```bash
# ed25519 more secure elliptic curve
# -C: allows to give a comment to identify key
ssh-keygen -t ed25519  -C "<comment>" 
```

### Removing known host entries

```bash
ssh-keygen -f ~/.ssh/known_hosts -R 123.45.678.9
```

### Copy public key to server

```bash
ssh-copy-id -i <public key> <user>@<ip_address>
# e.g. ssh-copy-id -i ~/.ssh/id_vps.pub user@123.45.678.9
```

### Checking the passphrase for a private key 
```bash
ssh-keygen -y -f /path/to/your/private_key
```

## ssh agent

```bash
# load key in agent
ssh-add /path/to/your/private_key

# check keys loaded in the agent
ssh-add -l
```
