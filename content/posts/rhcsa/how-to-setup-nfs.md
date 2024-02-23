---
title: "How to Setup NFS"
date: 2024-01-05T08:30:40-06:00
description: "Sharing drives between Linux/Unix systems"
draft: false
type: "post"
tags: ["linux", "ex200", "storage"]
showTableOfContents: true
---

![setup NFS Image](/images/posts/rhcsa/setup-nfs/setup-nfs.png)

To share drives between Unix-like systems, the best way to do that is through Network File Share 
or NFS for short. As one of the objectives for the Red Hat Certified System Administrator (RHCSA) 
Exam, it is important to know how to do so. Even if you are not studying for the EX200 exam, it's 
still important for any Systems Administrator to know.

In this guide, we'll go over how to:
- install NFS on RHEL based systems
- configure NFS on the server
- configure NFS on the client
- configure firewalld for NFS

For this exercise, you are going to need 2 Linux VMs that are RHEL based (Fedora, Rocky Linux, Alma Linux) and get the IP addresses from both instances. In this example, the server's IP will be `192.168.0.4/24` and the client's IP will be `192.168.0.5/24`. With that said, let's get started

## Installing NFS

To start, make sure both the server's repos and the client's repos are up-to-date by running:
```
sudo dnf update
```

To install NFS, run this command on the server:
```
sudo dnf install nfs-utils libnfsidmap
```

On the client, run this command:
```
sudo dnf install nfs-utils rpcbind
```

Once those items have been installed, make sure to enabled and start these items on the server:
```
sudo systemctl enable rpcbind
sudo systemctl enable nfs-server
sudo systemctl start rpcbind
sudo systemctl start nfs-server
sudo systemctl start rpc-statd
sudo systemctl start nfs-idmapd
```

On the client, make sure `rpcbind` item is enabled:
```
sudo systemctl start rpcbind
sudo systemctl enable rpcbind
```

Also, for initial testing, disable the firewall on the server by running
```
sudo systemctl stop firewalld
sudo systemctl disable firewalld
```

If the above command does not work, you may have a different firewall than FirewallD. To check out what firewall you are using, run the following command 
```
ps –ef | egrep “firewall|iptable|nftables”
```

Otherwise, if this command fails to find your firewall, you may wish to check online to see what firewall your distro is running by default. 

## Configuring the NFS Server

On the server, make sure the directory you are going to use for the NFS share is created and has the correct 
permissions. In this case, we'll use the directory `nfs-share` and set the permissions to read-write-executable 
to the whole system.
```
sudo mkdir /nfs-share
sudo chmod a+rwx /nfs-share
```

Next, we need to edit the file `/etc/exports` to tell the NFS server what directory the nfs share is located, what 
server to send the share, and the permissions the share should have. In this example, enter the information below 
into the file with your favorite text editor as root.
```
/nfs-share 192.168.0.5(rw,sync,no_root_squash)
```

Lets break down the content above. 
- `/nfs-share` - The directory where the NFS exists
- `192.168.0.5` - The IP where to send the NFS share (aka, the client)

The last part is the permissions to the specific server(s). Here is a table of the options:
| Option | Description |
| ----------- | ----------- |
| rw | Share as read-write |
| ro | Share as read-only |
| sync | File data changes are made to disk immediately. Has some impact on performance, but less likely to have data loss |
| async | File data changes are made initially to memory. Speeds up performance, but more likely to result in data loss |
| root_squash | Map root user and group account from NFS client to anonymous accounts, either the nobody or nfsnobody account |
| no_root_squash | Map root user and group from NFS client to the local root and group accounts |

After you save the `/etc/exports` file, you need to let NFS know there are changes to be added. To do this, run the command: 
```
sudo exportfs -rv
```

The flags in the command mean as such:
- `-r` - Reexports all directories, synchronizing `/var/lib/nfs/etab` with `/etc/exports` and files under `/etc/exports.d/`.
- `-v` - Be verbose 

For more information about the `exportfs` command, check out its man page buy running `man exportfs`.

## Configuring the NFS Client

Now with our NFS share setup on the server, its time to configure the client. On the client, create a directory where you would like to mount the NFS share. In this example, we'll go with `external-share` as the name of the directory.  
```
sudo mkdir /external-share
```

Next, you can check the mount information from the NFS server on the client by running
```
showmount -e 192.168.0.4 
```
The flag for the command mean as such:
- `-e` - Show the NFS server's export list.

For more information about the `showmount` command, check out its man page buy running `man showmount`.

Finally, its time to test to see if we can mount the NFS share. To do so, run
```
sudo mount 192.168.0.4:/nfs-share /external-share
```

To verify if it mounted, run 
```
df -h
```

## Setup FirewallD for NFS

Now that we've confirmed that the nfs share works, its time to configure the firewall to allow clients to access nfs shares on the server. To do this, we need to first bring back up the firewall on the server. 
```
sudo systemctl start firewalld
sudo systemctl enable firewalld
```

To confirm that the firewall is up, you have 2 options
```
sudo systemctl status firewalld
-- OR --
sudo firewall-cmd --state
```

Next, we need to allow NFS on the firewall, which runs on `2049/tcp` and reload the firewall to allow the changes to take affect. We do this by running
```
sudo firewall-cmd --permanent --add-port=2049/tcp
sudo firewall-cmd --reload
```

To verify that the rule was added correctly
```
sudo firewall-cmd --permanent --list-ports
```

Finally, to test to see if the connection works, go back on the client and run this command
```
sudo mount 192.168.0.4:/nfs-share /external-share
```

You should be able to now create files in the `/external-share` directory from the client and view the files on the server at `/nfs-share`! 

## Conclusion

In this article, you've been shown how to:
- Setup NFS on a server/client stack, and 
- How to secure NFS with FirewallD.

If you have any questions, please feel free to reach out to me. If this article interested you, please check out the other articles I have on my site!
