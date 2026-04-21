# Ansible / AWX skeleton

Kleine, nette starter voor AWX of lokale Ansible-runs.

## Inhoud
- `playbooks/base.yml` – basispackages + timezone
- `playbooks/users_ssh.yml` – users, groups en authorized keys
- `playbooks/docker.yml` – officiële Docker CE installatie via Docker apt repo
- `playbooks/node_exporter.yml` – Prometheus node_exporter als systemd service
- `playbooks/updates.yml` – apt update/upgrade/autoremove/autoclean

## Snel starten
1. Pas inventory aan in `inventories/test/hosts.ini`
2. Zet je SSH public key in `files/ssh/bart_id_ed25519.pub`
3. Pas variabelen aan in `inventories/test/group_vars/*.yml`
4. Test eerst op de test inventory

Voorbeelden:
```bash
ansible-playbook -i inventories/test/hosts.ini playbooks/base.yml
ansible-playbook -i inventories/test/hosts.ini playbooks/users_ssh.yml
ansible-playbook -i inventories/test/hosts.ini playbooks/docker.yml
ansible-playbook -i inventories/test/hosts.ini playbooks/node_exporter.yml
ansible-playbook -i inventories/test/hosts.ini playbooks/updates.yml
```

## AWX tip
- Maak 1 Project aan op basis van deze repo
- Maak 2 inventories: `Test` en `Production`
- Maak per playbook een apart Job Template
- Gebruik in het begin eventueel een `Limit` op 1 host
