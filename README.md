# ansible-collector

Ansible playbook for collecting output from Cisco devices via SSH.

Used for show commands in exec mode, can also be used for other exec mode commands (e.g. clear).

Not intended for configuration mode commands.

## Usage
```
ansible-playbook /path_to_playbooks/collect.yaml --vault-id user@password_file
```

## Ansible Vault

Create a password file containing a secret - this will be used for encryption of actual device credentials.

Use the ansible vault command below to encrypt the actual device credentials using any username.
```
ansible-vault encrypt_string --vault-id user@password_file 'actual_device_credential' --name 'ansible_variable_name'
```

This process should be repeated for username, password, and enable password - by assigning the encrypted output to the ansible variables below:

- ansible_user
- ansible_ssh_pass
- ansible_become_password

Paste the output of the ansible vault command in the devices.yaml file in the /group_vars directory

## ansible.cfg changes
- gathering=explicit
- inventory=/etc/ansible/hosts
- transport=ssh
- host_key_checking=False
