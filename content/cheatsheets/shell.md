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
groups # shows groups of current user
groups <user>  # shows groups user belongs to

gentent group # list all groups
getent group <group> # shows members of a group

# add user to an additional group
sudo usermod -aG <group> <user>
# -a: append, otherwise user will be removed from all not listed groups
# -G: takes a comma separated list of groups
```

## Commands

- TODO: df # total used and available disk space

- TODO: key generation

- TODO: nohup

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

- __du__: 
  - get the size of a folder: `du -hs /path/to/directory`
    - `s`: gives only the summary of the folder, not for every folder separately

- __grep__: 
  - use regex: e.g. select the lines that contain either "hook id:" or "duration:":
    ```bash 
    grep -E '(hook id:|duration:)' pre-commit-logs.txt
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
