---
title: "How to setup Bind in Docker"
date: 2024-08-03T15:59:24-05:00
description: "The Docker Name Service"
draft: false
type: "post"
tags: ["docker", "bind", "devops"]
showTableOfContents: true
---

![Bind in Docker](/images/posts/how-to/setup/bind-in-docker/cover.png)

## Introduction

Domain Name System or more commonly known as DNS, is a way for computers to translate an IP address to a Fully Qualified Domain Name (FQDN). In simple terms, if you wanted to go to say `kernel.org`, you would just need to type that into your browser instead of typing `139.178.84.217` for the IPv4 address. Or if you wanted to be a bit more extra, here is `kernel.org`'s IPv6 address: `2604:1380:4641:c500::1`. Commonly referred to as the internets dictionary, DNS is extremely helpful by giving meaningful names to otherwise complicated output.   

It is important to have a cursory knowledge on DNS and how it works. The best way to truely learn is to actually set up a DNS server and test it out. For most business networks, DNS is a crucial part of the daily functionings as it is used not only for easily allowing customers to find their sites, but it also is used in other programs like Active Directory or LDAP.  

In this guide, I'll be showing how to manually setup bind9 servers (a primary and secondary) in Docker. *I may in another article write how to setup bind9 using Ansible in the future. Keep a lookout for that :)*

### Prerequisites

To follow along with this guide, you'll need:

- 2x Debian Servers VMs (4GB of RAM and 2 CPU per)
- The first three octets to your local network.

For me, I'm going to be using 2 Raspberry Pi 4's with 4GB of RAM. You can easily get by with less resources as Bind doesn't use that much in the first place.

For the network octets, you can find that by running `ipconfig` if you are on Windows or `ip a` if you run Linux or Mac. When you do so, it should show you output about your local network. If you look at the IP address of your computer, you will see something like this:
```
192.168.1.X
```
Where `X` is some number ranging between `1-254`. However, the numbers that we need are `192.168.1` as this will be used for reverse lookup in out network (More on this later).

## Installing Docker on Raspberry Pi OS

If you are using a local VM running Debian, then you can follow the [official guide](https://docs.docker.com/engine/install/debian/) for Debian. 
If you have some Raspberry Pi's lying around like me, then to start you will need to update the system:
```
sudo apt update && sudo apt upgrade -y
```

Next, we'll run the official installation script from Docker:
```
sudo curl -sSL https://get.docker.com | sh
```
> NOTE: If you are unsure about randomly running a script script from the internet (as you should), feel free to read the script at the provided URL

After the installation script finishes, check to see if Docker is running on the Pi:
```
sudo systemctl status docker
```

If the service is up and healthy, you need to add the local user account to the `docker` group. Run the `usermod` command to add the group to your user:
```
usermod -aG docker pi
```

Once you have the group added, you need to logout and log back in for the group to be connected to your account. You can check by running the `group` command after you log back in. You should see the `docker` group in the output.

To see if docker works as expected, run this command:
```
docker run hello-world
```

This will download and run the `hello-world` container without having to use the `sudo` command.

## Bind setup

To make the organization easier, on both Raspberry Pi's run these commands to create the same directory structure in `/home/pi`.

```bash
touch compose.yml
mkdir -p etc/bind/
```

### Primary Name Server

Lets start by configuring the primary dns server. Just choose one of the raspberry pi's for this. In the `compose.yml` file you will need to add the following:

*compose.yml*
```compose.yml
services:
  bind9:
    container_name: dns1
    image: ubuntu/bind9:latest
    environment:
      - BIND9_USER=root
      - TZ=America/Chicago
    network_mode: host
    volumes:
      - ./etc/bind/named.conf.local:/etc/bind/named.conf.local 
      - ./etc/bind/named.conf.options:/etc/bind/named.conf.options
      - ./etc/bind/db.local.example.com:/etc/bind/db.local.example.com
      - ./etc/bind/db.192.168.1:/etc/bind/db.192.168.1 
    restart: always
```

What this compose file will do is use the latest version of bind9 from Canonical. It will also name the container as dns1, set the user as root and set the time zone to `America/Chicago`. For the primary server it will need a few files to fully configure bind.
What each file each file does is as such:
- named.conf.local - This config file designates the server as a master DNS server along with a pointer to the secondary server to transfer any changes.
- named.conf.options - This config file will set options like an ACL, forwarders, and what the DNS server is able to query.
- db.local.example.com -  This is your forward lookup zone and contains the normal DNS entries like CNAME, MX records, or A records.
- db.192.168.1 - This is your reverse look up file and will allow you to lookup the server by IP address.

With that said let's create them
```
touch etc/bind/{named.conf.options,named.conf.local,db.local.example.com,db.192.168.1}
```

### Configuring named.conf.local

We'll start configuring the `named.conf.local` first. As stated above, this file configures what zones the DNS server is reponsible for. In this case, the server would be responsible for `local.example.com`.
You will need to change this to a domain name that you own. For example, if you own `coolgolfclubs.com` then you could create a subdomain like `home.coolgolfclubs.com` by changing anywhere it says `local.example.com`.
You will also need to know the IP address of your other Pi to configure the secondary DNS server. In this case its `192.168.1.3` for the secondary DNS server and `192.168.1.2` for the primary DNS server. 

```named.conf.local
zone "local.example.com" {
	type master;
	file "/etc/bind/db.local.example.com";
	allow-transfer { 192.168.1.3; };
	also-notify { 192.168.1.3; };
};

zone "1.168.192.in-addr.arpa" {
	type master;
	file "/etc/bind/db.192.168.1";
	allow-transfer { 192.168.1.3; };
	also-notify { 192.168.1.3; };
};
```

### Configuring named.conf.options

Next, lets configure the `named.conf.options` file. The first part of the file creates an ACL called `trustedclients` that only allows the the localhost, localnet, and the local network.
After the ACL, we configure the options for the DNS server. We start with pointing to where the cache should be placed. The option after that allows for recursion and ACLs.
The next option allows querying the trustedclients list for Domain Names. The `allow-query-cache` option allows the DNS server to query any DNS information that was cached.
The next option allows for recursion only on the ACL. Next we configure the forwarders, which are the Cloudflare DNS server that block malware. The `dnssec-validation` has caused issues 
with querying responses so I've disabled it. Finally, we tell the DNS server to query itself for IPv4 and IPv6.

```named.conf.options
acl trustedclients {
        localhost;
        localnets;
        192.168.1.0/24;
};

options {
        directory "/var/cache/bind";

        recursion yes;
        allow-query { trustedclients; };
        allow-query-cache { trustedclients; };
        allow-recursion { trustedclients; };

        forwarders {
                1.1.1.2;
                1.0.0.2;
        };

        dnssec-validation no;

        listen-on-v6 port 53 { ::1; };
        listen-on port 53 { 127.0.0.1; 192.168.1.2; };
};
```

### Configuring db.local.example.com

Now we can finally configure the meat and potatoes of DNS, which are the records. In this file, I set up the basic information that is needed Bind to work with this zone.
The first true line after the comments details how long the Bind Time To Live, or TTL for short, is. In this case, it is 24 hours. Next defines that this zone file is the 
origin of the `local.example.com` subdomain. The next line defines the Source Of Authority record, which is `ns1.local.example.com` followed by an email address of `mail.example.com`. 
If that were a real email address, it would be send to `mail@example.com` as the `@` is a special character in bind so it is replaced here with a period `.`. 

The next few lines define basic configuration options for this zone specifically, including the serial number of the zone. This number needs to be updated every time a change is done in this file. 
So, if I were to add a new A record to this file, then the serial number needs to go up by 1. The next line with the `@` special character, defines this file for `ns1.local.weiseguy.net` and can be 
changes to your actual domain name. Finally we have 2 A records pointing to `ns1` and `ns2` respectively.

```db.local.example.com
;
;  BIND data file for local.example.com zone
;
$TTL 24h
$ORIGIN local.example.com.
@	IN	SOA	ns1.local.example.com. mail.example.com. (
			      1		; Serial
			    24h		; Refresh
			     2h		; Retry
			  1000h		; Expire
			     2d )	; Negative Cache TTL
;
@	IN	NS	ns1.local.example.com.

ns1	IN	A	192.168.1.2
ns2	IN	A	192.168.1.3
```

This file mimics the zone file for `db.local.example.com` except the records are in reverse. This is so bind can look up your query by IP Address. It is quite helpful if you know the IP Address of a service 
you are running locally. It also just is much nicer to have so why not. 

```db.192.168.1
;
;  BIND reverse data file for local.example.com zone
;
$TTL 24h
$ORIGIN 1.168.192.in-addr.arpa.
@	IN	SOA	ns1.local.example.com. mail.example.com. (
			      1		; Serial
			    24h		; Refresh
			     2h		; Retry
			  1000h		; Expire
			     2d )	; Negative Cache TTL
;
@	IN	NS	ns1.local.example.com.

2	IN	PTR	ns1.local.example.com
3	IN	PTR	ns2.local.example.com
```

### Secondary Name Server

Finally, for the secondary server. To set it up in docker compose is very similar to the primary, but with only one volume instead of four.

```compose.yml
services:
  bind9:
    container_name: dns2
    image: ubuntu/bind9:latest
    environment:
      - BIND9_USER=root
      - TZ=America/Chicago
    network_mode: host
    volumes:
      - ./etc/bind/named.conf.local:/etc/bind/named.conf.local 
    restart: always
```

Inside of the `named.conf.local` is also varily similar to the primary except that it defines itself as a secondary DNS server and pulls down the specific zones 
that it is responsible for. In this case it is the `local.example.com` subdomain as well as the reverse lookup table `1.168.192.in-addr.arpa`.

```named.conf.local
zone "local.example.com" {
	type secondary;
	file "/etc/bind/db.local.example.com";
	masters { 192.168.1.2; };
};

zone "1.168.192.in-addr.arpa" {
	type secondary;
	file "/etc/bind/db.192.168.1";
	masters { 192.168.1.2; };
};
```

With all of that done, the secondary server will sync up with the primary server when turned on with a `docker compose up -d` and store a copy of any of the zones.
When the primary DNS server is not available for what ever reason, the secondary server will activate as a mirror and server up the content that was sync. However, please 
note that the secondary server as configured cannot serve new content to the systems on the network. If you wanted to add a new domain, but the primary server is not on, 
the secondary server has no means to serve that new domain.

If you want to check that the DNS servers are working correctly, they you can try some nslookup commands as shown below.

```bash
nslookup ns1.local.example.com <primary DNS Server IP>
nslookup gnu.org <secondary DNS Server IP>
nslookup 192.168.1.3 <primary DNS Server IP>
```

## Wrapping it up

With this tutorial done, you can now have your own internal DNS server running. Just make sure to add the DNS server IP addresses to your router. You may also need to reboot any machine that was turned on before 
you added the DNS servers to be able to get to the domains that you wish to get to. I believe that by having your own DNS server at home, it makes it much easier to access machines and provides a nice little project 
you can get done in a few hours. I have been using this setup for years without any issues. This has included moving a few times, I just needed to make sure the network was the correct subnet, added the DNS servers and 
BOOM, all of my services were good to go. I hope that you found this post helpful and infomative! Until next time, thank you for reading!

