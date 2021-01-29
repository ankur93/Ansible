# Ansible Playbook for setting following roles:
1. service account, 
1. Docker
1. NVM

## Running this script on local machine

### Pre-requisites
1. vagrant
2. virtualbox
3. ansible
4. ssh private/public key generated as (~/.ssh/{id_rsa,id_rsa.pub}) if not `ssh-keygen -t rsa -P ""`

### Bring Up VMs
This will bring up two Virtual Machines with CentOS 7.
```
vagrant up
```

### Run Ansible playbook
This will install dependencies on local VM
```
ansible-playbook -i hosts.vagrant site.vagrant.yml
```

## Running this script on cloud machines

### Pre-requisites

1. `ansible` (local machine or jumpbox)
2. Account with remote and sudo access to cloud machines
3. Firewall rules for machines


### Config update

1. **hosts**
> Update `ansible_user` (e.g svc-account-name) and `ansible_ssh_pass` for respective account.
```
[ppe]
10.202.20.5
10.202.20.6
....
....
[prd]
10.202.20.7
10.202.20.8
....
....
```

2. **Plugins**  
   Run following commands on controller/local machine.
```
ansible-galaxy collection install community.general
```


### Run Ansible playbook
This will install dependencies on real cloud machines

```bash
ansible-playbook -i hosts site.yml
```
