---
title: "Shell"
date: "2025-01-14"
tags: ["stub"]
draft: true
---

## Operators

- `|`: pipes the standard output (__stdout__) of the left command into the standard input of the right one
- `|&`: pipes __stdout__ and __stderr__ in the standard input of the right command
- `&&`: executes the right command if the left one succeeded
- `||`: executes the right command if the left one failed

## General

Find out linux version

```bash
cat /etc/os-release
```

Find out current user and its groups:

```bash
whoami  # shows current user
groups <user>  # shows groups user belongs to
```

## Commands

- TODO: key generation

- __chmod__: changing rights

  3 numbers: _ _ _ -> permission for **user, group, others**

  - parameters:

    | **permission** | **symbol** | **number** |
    | :------------: | :--------: | :--------: |
    |      read      |     r      |     4      |
    |     write      |     w      |     6      |
    |    execute     |     x      |     1      |

    permissions add up: 6 = 4 + 2: read and write access

    ```bash
    chmod 400 private-key-file.pem # restricting file access (read) to yourself
    ```

## Custom function 
```bash 
# in .zshrc
start_ec2() {
  export AWS_DEFAULT_REGION=eu-central-1
  export AWS_PROFILE=<AWS profile name>
  aws ec2 start-instances --instance-ids <instance id>
}

# use the command
start_ec2
```
