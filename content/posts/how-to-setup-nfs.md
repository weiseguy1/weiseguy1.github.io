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



## Configuring the NFS Client
## Configuring Firewalld for NFS
## Conclusion
