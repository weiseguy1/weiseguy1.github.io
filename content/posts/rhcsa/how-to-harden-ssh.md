---
title: "How to Harden SSH"
date: 2024-01-03T12:29:20-06:00
description: "Making the Secure Shell even more secure ...shell"
draft: false
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
Once you are in the file, you can enable an option for ssh by removing the `#` next to the item.

### Configure Idle Timeout
Lets start with configuring the idle timer within ssh. In the first option, it is the amount of time in seconds before 
the server will send a null packet to make sure the server is alive. The second option is the number of times the server 
sends a null packet to the client before disconnecting. In this case, the server will wait 600 seconds before sending a null 
packet and will only do so 5 times.

```
ClientAliveInterval 600
ClientAliveCountMax 5
```

### Disable Root Login
This option is pretty self explanitory, but this will disable anyone from connecting to the server as root.

```
PermitRootLogin no
```

### Disable Empty Passwords
This option disabled a user from having an empty password to connect to the server.

```
PermitEmptyPasswords no
```

### Limit User SSH Access
This option limits the users that are able to connect to the server based on the username used to connect. In this case 
the only two users able to connect would be user1 and user2

```
AllowUsers user1 user2
```

### Using a Different Port
Finally, this option changes the default port of SSH from 22 to one of the administrators choosing. In this case, the port 
would be `2024`. 

```
Port 2024
```

To test to see if this option works, open a second terminal on your computer and run this command: 
```
ssh -p 2024 user1@server
```

the `-p` flag allows you to use a different port from the default.

## Saving the configuration

After configuring all of the options listed above, restart the ssh daemon on the server. If you're using SystemD as the init system for the server, run:
```
sudo systemctl restart sshd
```

Next, on the client side in your `~/.ssh` directory, create a file named `config` and place this info:
```
Host serveralias
    HostName server
    User user1
    Port 2024
    IdentifyFile ~/.ssh/id_ed25519
```

Save the file, the run:
```
ssh serveralias
```

## Conclusion

In this article, you've been shown how to create a ssh public/private key pair. How to upload the public key securely, and how to harden SSH against malicous actors.
If you have any questions, please feel free to reach out to me.


