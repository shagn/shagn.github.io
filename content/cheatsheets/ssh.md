---
title: "SSH"
date: "2025-07-06"
tags: ["stub"]
draft: true
---

### ssh config

```bash
Host vps
    HostName 123.45.678.9
    User root
    IdentityFile ~/.ssh/id_vps # 
    AddKeysToAgent yes  # automatically adds the key to the running agent
    UseKeychain yes # stores the passphrase in the macOS Keychain
```

## ssh-keygen

### Generating new key pair

```bash
# ed25519 more secure elliptic curve
# -C: allows to give a comment to identify key
ssh-keygen -t ed25519  -C "<comment>" 
```

### Removing  known host entries

```bash
ssh-keygen -f ~/.ssh/known_hosts -R 123.45.678.9
```

## Copy public key to server

```bash
ssh-copy-id -i <public key> <user>@<ip_address>
# e.g. ssh-copy-id -i ~/.ssh/id_vps.pub user@123.45.678.9
```
