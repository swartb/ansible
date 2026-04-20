# Ansible SSH key rollout

## Layout
- `inventory.ini` — known hosts, using `bart` on the targets
- `group_vars/all.yml` — user/key settings
- `playbooks/authorized_keys.yml` — creates users, installs keys and configures passwordless sudo
- `playbooks/bootstrap_ansible_key.yml` — installs the dedicated Ansible management key first
- `files/ssh-keys/` — public keys used by the playbooks

## Run on the control node
The control node user is `ansible`.
Use that account on the Ansible server and run from:
```bash
cd /home/ansible/ansible
```

### 1) Bootstrap the Ansible management key
Use the already working SSH key first:
```bash
ansible-playbook -i inventory.ini playbooks/bootstrap_ansible_key.yml
```

### 2) Run the normal user/key playbook
```bash
ansible-playbook -i inventory.ini playbooks/authorized_keys.yml
```
