---
title: "How to Setup NFS"
date: 2024-01-05T08:30:40-06:00
description: "Sharing drives between Linux/Unix systems"
draft: true
type: "post"
tags: ["linux", "ex200", "storage"]
showTableOfContents: true
---

To share drives between Unix-like systems, the best way to do that is through Network File Share 
or NFS for short. As one of the objectives for the Red Hat Certified System Administrator (RHCSA) 
Exam, it is important to know how to do so. Even if you are not studying for the EX200 exam it's 
still important for any Systems Administrator to know.

In this guide, we'll go over how to:
- install NFS on RHEL based systems
- configure NFS on the server
- configure NFS on the client
- configure firewalld for NFS

With that said, let's get started

## Installing NFS

To start, make sure both the server's packages and the client's packages are up-to-date by running:
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

Once those items have been installed, make sure to enabled these items on the server:
```
sudo systemctl enable rpcbind
sudo systemctl enable nfs-server
sudo systemctl start rpcbind
sudo systemctl start nfs-server
sudo systemctl start rpc-statd
sudo systemctl start nfs-idmapd
```

On the client, make sure this item is enabled:
```
sudo systemctl start rpcbind
```

## Configuring the NFS Server

On the server, make sure the directory you are going to use for the NFS share is created and has the correct 
permissions. In this case, we'll use the directory `nfs-share` and set the permissions to read-write-executable 
to the whole system.
```
mkdir /nfs-share
chmod a+rwx /nfs-share
```

Next, we need to edit the file `/etc/exports` to tell the NFS server what directory the nfs share is located, what 
server to send the share, and the permissions the share should have. In this example, enter the information below 
into the file.
```
/nfs-share 192.168.0.5(rw,sync,no_root_squash)
```

Lets break down the content above. 
- `/nfs-share` - The directory where the NFS exists
- `192.168.0.5` - The IP where to send the NFS share

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
exportfs -rv
```

The flags in the command mean as such:
- `-r` - Reexports all directories, synchronizing `/var/lib/nfs/etab` with `/etc/exports` and files under `/etc/exports.d/`.
- `-v` - Be verbose 

## Configuring the NFS Client

## Setup FirewallD for NFS

## Conclusion

In this article, you've been shown how to setup NFS on a server/client stack and how to secure NFS with FirewallD. If you have 
any questions, please feel free to reach out to me.
