---
title: "Learning Devops (Day 02): Ansible"
date: 2024-07-08T22:01:56-05:00
description: ""
draft: false
type: "post"
tags: ["series", "devops", "ansible"]
showTableOfContents: true
---

![Cover Image](/images/posts/series/learning-devops/day-02/cover.png)

## Introduction

Hey everyone, welcome back to the Learning Devops Series. For this *"day"* we will be looking at Ansible, an open-source automation platform used for provisioning, configuration management, and application deployment. Ansible is used pretty much everywhere you look now-a-days in the IT field as it is so multifaceted. You can use ansible to install software on servers, setup user access permissions, and even setup your development environment on your local machines. If you are going into this field then you are going to at least need to know about Ansible as it will make your day-to-day workings a lot easier. 

This post will cover a basic introduction into Ansible and a few of the add ons that come with it. Also, near the end of the post, we will be testing the knowledge we've learned by putting it to use in a lab. This lab will integrate our Ansible playbooks into a Terraform script that will deploy some Ubuntu Server VMs on Azure. If you haven't read my previous [post on Terraform](/posts/series/learning-devops/day-01-terraform), I recommend you do so to get you up to speed.  

## Ansible

As already stated previously, Ansible is an open-source automation platform used for provisioning, configuration management, and application deployment. The automation is done using a few files: the inventory file and what are known as *"playbooks"*.

### Inventory file
The inventory file plays a crutial role in the automation of systems as it tells ansible where to apply the playbooks and allow grouping of systems into there own blocks. Inventory files can come in two flavors: static inventory files or dynamic inventory files. The dynamic inventory file is use when you will not know what the IP address or the domain name of the server will be when you apply the playbooks. This is useful for IaC testing setups as you more than likely won't know what the public IP address will be when you run the code. We'll take a more in-depth look at dynamic inventory files later in the post.

The other type of inventory files is the static inventory file. This is pretty much what you think it is. The inventory file contains the IP address or domain name of the servers you know and already have access to. An example of the static inventory file is shown below:

**inventory**
```inventory.toml
[webserver]
wb1 ansible_host=192.168.0.34 ansible_user=wbuser
wb2 ansible_host=webserver2.example.com ansible_user=mario
wb3 ansible_host=192.168.0.36 ansible_user=peach

[database]
db1 ansible_host=192.168.0.60 
db2 ansible_host=192.168.0.65
db3 ansible_host=192.168.0.67

[prod]
wb1
db2

[qa]
wb2
db3

[testing]
wb3
db1
```

In this file, you can see it is written in the TOML format and it has been grouped in a few different ways. The first is the inventory file has grouped 3 webservers and 3 database servers under their respective blocks. This allows for a clean and easy to read inventory. Next under both the webserver and database groups, you have an alias of the servers. These basically allow the user to logically name servers and to place them under other blocks like the `prod`, `qa` or `testing` blocks. After that, there is the `ansible_host` option which is assigned the actual IP address or even the domain name of those servers. Finally, under the `webserver` block, the `ansible_user` option assigns the user for the specific server which ansible should connect to.  

### Playbooks
Next up are playbook files. These playbooks are written in YAML, an easy to read format used in a ton of automation software. An example of YAML is shown below:

**playbook.yml**
```playbook.yml
---
- hosts: webserver
  become: true

  tasks:
  - name: install latest version of Nginx
    apt:
     name:
       - nginx
    state: latest
  - name: start nginx service
    service:
      name: nginx
      state: started
```

In this example you can see that YAML uses dashes and spaces to indicate the different hierarchies of the code. To break this playbook down a bit more, lets start at the top. The `hosts` property tells ansible on which hosts to run this playbook on. In this case, `webserver` means only the webserver hosts defined in the `inventory` file. The `become` property tells ansible to become another user. With it being set to `true`, ansible will try to become root. The `tasks` property is where we starting defining the tasks that need to get completed in the playbook. In this example there are two tasks that need to get completed. 

The first is the task labeled *"install latest version of Nginx"* using the `name` property. This uses the `apt` property to install a list of packages using the apt package manager. In this case it is the `nginx` package, displayed in a YAML list. The `state` property tells ansible to install the latest version of the package.   

The second task *"start nginx service"* does exactly that. Using the `service` property, the nginx package's `state` is set to started. 

### Running the playbook

To run the playbook above, you can do so like:
```
ansible-playbook -i inventory playbook.yml
```

This will then produce output like below:
```
PLAY [webserver] ***************************************************************************************************************************

TASK [Gathering Facts] *********************************************************************************************************************
ok: [wb2]
ok: [wb1]

TASK [Install latest version of Nginx] *****************************************************************************************************
ok: [wb2]
ok: [wb1]

TASK [start nginx service] *****************************************************************************************************************
ok: [wb1]
ok: [wb2]

PLAY RECAP *********************************************************************************************************************************
wb1                        : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
wb2                        : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
```

As you can see, when running the playbook ansible gathers the information about what servers it should look at, then it moves on to the first task on installing Nginx and then finishes off with starting the Nginx service. The *PLAY RECAP* shows a listing of all of the items that have succeeded, changed items, unreachable servers, and if any of the tasks failed, got skipped, rescued or ignored. 

### Roles

Now that we've written and run our first playbook, what if I told you that there is a better way to write them? This new way of writing playbooks are called *roles*. Roles allow the author of the playbooks to write them in such a way as to decrease the amount of repetition normally found in stand alone playbooks. The structure of a role is as such:

```
myplaybook
|_ inventory
|_ playbook.yml
|_ roles
   |_ nginx
      |_ tasks
         |_ main.yml

```

As you can see, the main ansible items are still present but the task of installing and starting nginx have been decouple from the main playbook and placed in its own file called `main.yml`. This makes the role reusable and more consise. The code inside the `main.yml` file is as such:

```main.yml
- name: install and check nginx latest version
  apt:
    name:
      - nginx
    state: latest
- name: start nginx
  service:
    name: nginx
    state: started
```

The playbook also has to be rewritten to be able to use the role. The playbook should look like this:

```playbook.yml
---
- hosts: webserver
  roles:
    - nginx
```

### Ansible Vault 

Now that we have inventory files, playbooks, and roles covered, lets look at Ansible Vault. Ansible Vault is used to encrypt sensive data like passwords and API keys so that they are unreadable to unwanted eyes. This is useful for when you need to have a playbook in a public git repository and you need to have the sensitive data in order for the playbook to work. 

To see Ansible Vault in action, lets create another role for mysql. Create the directores `mysql/tasks`. The directory structure should look like this:

```
myplaybook
|_ inventory
|_ playbook.yml
|_ roles
   |_ nginx
   |_ mysql
      |_ tasks
         |_ main.yml

```

Next, in the `roles/mysql/tasks/main.yml` write this:

```main.yml
---
- name: Update apt cache
  apt: update_cache=yes cache_valid_time=3600
- name: Install required software
  apt: name="{{ packages }}" state=present
  vars:
    packages:
    - python3-mysqldb
    - mysql-server 
- name: Create mysql user
  mysql_user: 
    name={{ mysql_user }} 
    password={{ mysql_password }} 
    priv=*.*:ALL
    state=present
```

What this playbook will do is update the apt repository, install the specified packages for mysql to work, then create a mysql user with a password. Anything within the double curly braces `{{ }}` are variables within ansible. You can see there is one for `packages` and the `mysql_user` and `mysql_password`. As we want to keep the username and the password private, we then need to create a new directory at the root of our project called `group_vars`. Inside `group_vars` we need to create a directory that matches a block within our inventory file so that ansible knows where the variables belong. In this project the directory would be called `database`. Inside the `database` directory, create another `main.yml`. Inside the `main.yml` you can then place the variables we will be using for the database setup:

```main.yml
---
mysql_user: mysql_username
mysql_password: SuP3rSecurePassw0rd
```

To encrypt the mysql username and password, you just need to run:
```
ansible-vault encrypt group_vars/database/main.yml
```

> NOTE: If you ever need to decrypt this file for whatever reason, you can run: `ansible-vault decrypt group_vars/database/main.yml`

Ansible Vault will then prompt you for a password, just enter something memorable and then take a peak at the `group_vars/database/main.yml` file again. The contents should look like this:

```
$ANSIBLE_VAULT;1.1;AES256
36396265323436373135393534646666373166346462633736323066646133653634396364666337
6432666633333662366236343762343363316436613738610a646234616465386666623433376362
31376565666336323332306536306631616663376331626239633864363533663762323661633862
3534623063613166330a306364626464396639613138613662366464663533623663613732646533
35343435393738306135303036393436326436316361656463366239643133376238393961323631
33313565656430623861333664323066333035303631373532383364336665396237633139306131
663266363537343430346166643664326438
```

Pretty neat right! Now before you try to run your playbook, just note that ansible itself won't be able to read the `group_vars/database/main.yml` without the password you entered. To be able to run your playbook, you can run:

```
ansible-playbook -i inventory playbook.yml --ask-vault-pass
```

However, if you are trying to add your playbook to a CI/CD pipeline, it wouldn't be able to function. To solve this, you can place the password you used to encrypt `group_vars/database/main.yml` in a `vault_pass.txt` file. Then just run:
```
ansible-playbook -i inventory playbook.yml --vault-password-file vault_pass.txt
```

Just make sure to place the `vault_pass.txt` file into your `.gitignore` file before pushing this project to Github or the like.

## Lab

Now that we've covered everything you need to know about how to start using ansible, let's try this in a lab. To start, go to this [link](https://github.com/weiseguy1/learning-devops/) to my repostory on the matter. Then pull the repo down using git and go into the ch3 directory:
```
git clone https://github.com/weiseguy1/learning-devops.git
cd ch3
```

This directory will be full of a lot of files that we've just talked about along with some Terraform files and an inventory-gen.sh bash script. Also, within this lab is the `README.md` which has all of the instructions you will need to get it to work.

If you remember at the beginning of the post I talked about how there are two different types of inventory files. Well, the `inventory-gen.sh` helps to create a dynamic inventory file. Let's look at it:

```bash
#!/bin/sh

# DESCRIPTION: Automatically generate inventory file for ansible

database=$(az vm list --resource-group rg-ansible-vm-lab --show-details --query "[*].{TAGS:tags.role, PIP:publicIps}" -o tsv | grep database | awk '{print $2}')

webserver=$(az vm list --resource-group rg-ansible-vm-lab --show-details --query "[*].{TAGS:tags.role, PIP:publicIps}" -o tsv | grep webserver | awk '{print $2}')
echo "[databases] $database " | tr ' ' '\n' >> inventory
echo "[webservers] $webserver" | tr ' ' '\n' >> inventory
```

This script uses the az cli command to find the Public IP adddress information based on the tags, then place the output into a newly created `inventory` file. This way is not the only way, of generating dynamic inventory files. In the book, it talks about using the Azure collection available through Ansible Galaxy. However, at the time of this writing, the Azure collection has some [issues](https://github.com/ansible-collections/azure/issues/1067) when generating a dynamic inventory file.  

## Wrapping it up

All and all, I think this chapter on ansible was pretty interesting as it showed me how to setup systems differently. What is nice about ansible is that once you have the playbooks written, you basically never have to do that process manually ever again. The only thing that I did have an issue on was the part on Azure Collections, which I spent literal days trying to get working to no avail. That is the reason I created the AZ CLI script which works without a hitch. Also, I really wanted to start using AZ CLI as I'm starting to study for that AZ-104 and I thought it would be good to get more experience with that tool as well. With that said, I plan to start writing a lot more ansible playbooks in the future as it is such a handy tool to have in the Systems Administrator toolbelt.

Next up in the series, I’ll be going over Packer and how to generate easily deployable images which you can use in your own Azure infrastructure. Stay tuned and thanks for reading!
