# ansible_update

![download](https://user-images.githubusercontent.com/5633085/45217044-a1fc8e80-b2dd-11e8-9b97-4e2fce0932fc.jpg)


I think it is awkward to update the vulnerability detected by Vuls by logging in to the server every time. So I registered servers managed by ansible and updated it with one shot.


## OS

CentOS/Amazon Linux   
Ubuntu  

## Vulnerability Update Method

1.u have to write hosts 

```
$ vim hosts/project1/dev
[web]
dev-web01

[dev:children]
web

```

2.Describe the package name you want to update to group_vars / all   

```
$ vim group_vars/all
UPDATE_TARGETS:
  - "python27"
  - "kernel"

```

3.fix update.yml


When a vulnerability is detected, first of all middleware is written in group_vars / all. In main.yml, with_items is being used and assigned.

## Caution
If there is a blank value, yum update - y /apt-get upgrade will be executed and all will be updated.  
Please delete unnecessary [- ""] and then let it flow.  

## Dryrun/Run

The part of updates is skiping, but do not worry as it is the shell module specification.  

When specifying a host, you need to specify it from the hosts directory when you enter a command.  
You can specify only one host that you want to update with [-l host name].  

```
$ ansible-playbook -i hosts/project1/dev update.yml -kKD -C
```
```
$ ansible-playbook -i hosts/project1/dev update.yml -kKD 
```
