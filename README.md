# A template of Ansible Playbook for Nutanix cluster Operetion

## Directory Stucture

```
.
|-- group_vars
|   `-- cluster
|       `-- cluster.yml
|       `-- private.yml
|   `-- cvm
|       `-- private.yml
|-- inventory
|-- README.md
|-- roles
|   |-- cluster
|   |   `-- tasks
|   |       `-- main.yml
|   |-- common
|   |   `-- main.yml
|   `-- cvm
|       |-- files
|       |   `-- fstrim
|       `-- tasks
|           `-- main.yml
`-- site.yml
```

## Run playbook

### Enable sshpass (for mac user)

`brew install http://git.io/sshpass.rb`

### Secret info
```
ansible_connection: ssh 
ansible_ssh_user: xxxxxx
ansible_ssh_pass: "yyyyyyyy"
```

#### Encrypt
```
ansible-vault encrypt group_vars/cluster/private.yml 
ansible-vault encrypt group_vars/cvm/private.yml 
```

#### Decryption

```
ansible-vault decrypt group_vars/cluster/private.yml 
ansible-vault decrypt group_vars/cvm/private.yml 
```

### Run

#### Use ssh instead of sftp
```
export ANSIBLE_HOST_KEY_CHECKING=False
#export ANSIBLE_TRANSPORT=ssh
#export ANSIBLE_SSH_ARGS=""
export ANSIBLE_SCP_IF_SSH=true
```

`ansible-playbook -i inventory site.yml --ask-vault-pass`
