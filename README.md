# Déployer Nautobot via Ansible + Docker

## Lancer rapidement
1) Éditer `inventory.ini` (IP + user SSH).
2) Chiffrer les secrets :
   ```bash
   echo "TonMotDePasseVault" > .vault_pass.txt
   chmod 600 .vault_pass.txt
   ansible-vault encrypt group_vars/all/vault.yml
   ```
3) Installer la collection Docker et lancer :
   ```bash
   ansible-galaxy collection install community.docker
   ansible-playbook playbooks/deploy_nautobot.yml
   ```
4) Accéder à `http://<IP>:8080`.

## Ce que fait le playbook
- Installe Docker sur la cible (Ubuntu/Debian)
- Déploie Postgres, Redis, Nautobot (docker-compose)
- Crée via API (module `uri`) : un **Site**, un **Device**, un **VLAN** et une **IP** affectée à l'interface

## Variables
- `group_vars/all/main.yml` : variables non sensibles
- `group_vars/all/vault.yml` : secrets (à chiffrer Ansible Vault)

## GitHub (méthode rapide via interface web)
- Créer un repo vide sur GitHub (public ou privé), nom recommandé : `nautobot-ansible`
- Upload **tout le dossier** (ou le ZIP fourni) _sans_ modifier l’arborescence
- Le lien du repo est ce que vous soumettrez sur la plateforme
