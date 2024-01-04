---
title: "How to Harden SSH"
date: 2024-01-03T12:29:20-06:00
description: "Making the Secure Shell even more secure ...shell"
draft: true
type: "post"
tags: ["blueteam", "linux", "security", "ex200"]
showTableOfContents: true
---

## Intro

If you are studying for your Red Hat Linux Certified System Administrator (RHCSA) Exam like I am,
then knowing how to secure SSH is a requirement that is guaranteed to show up. Even if you are not,
knowing how to harden SSH is really important to know. In this guide, I'll go over and explain:

- How to generate Public/Private SSH keys
- How to securely move the new generated public key to the server
- How to harden SSH configuration

With this in mind, let's get started.

## Generating SSH Keys

When using ssh to connect to servers, it can be quite annoying having to enter a password every single 
time. This can be amplified when you have 20, 40 or more servers to administer. To solve this issue, the 
ssh public/private key pair was created. Normally by default, ssh will generate the RSA key pair at 2048-bit.
This can be a problem as a 2048-bit RSA key is not quite safe anymore to use. Thankfully this can be changed! 

In this section, we'll generate the ed25519 ssh key pair type *(I know, rolls of the tongue, right?!)*. This key 
pair is the most secure type of key pair and is the most recommended key pair one can generate at the time of this 
writing. 

To generate the public/private key pair, run in your terminal:
```
ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/id_ed25519 -C "Super Secure Key"
```

To break the flags in this command down:
- `-o` - Specify a key/value option.
- `-a` - Specifies the number of KDF (key derivation function) rounds used.
- `-t` - Specifies the type of key  to  create.
- `-f` - Specifies the filename of the key file. 
- `-C` - To add a comment to the key. 

### Test the key

To test your ssh keys, you are going to need to copy your public key to the servers `~/.ssh/authorized_keys` file. To do this, run the command:
```
ssh-copy-id -i ~/.ssh/id_ed25519 username@server
```

Next, to test connecting to the server, run this command on the client (Laptop/Desktop):
```
ssh -i ~/.ssh/id_ed25519 username@server
```

You should be able to connect to the server without a password now! 

## Hardening SSH

Now that you can ssh with public/private key pairs, its now time to harden ssh itself. To do this, we'll need to edit 
`/etc/ssh/ssh_config`. You'll need root access to edit this file so run:
```
sudo vim /etc/ssh/ssh_config
```
### Configure Idle Timeout
### Disable Root Login
### Disable Empty Passwords
### Limit User SSH Access
### Using a Different Port
### Specifying SSH Keys


