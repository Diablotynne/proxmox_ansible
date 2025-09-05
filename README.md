# Mise en situation DevOps – Automatisation Proxmox & Ansible

** Dates :** 1er au 5 septembre 2025  
** Projet pédagogique **

##  Objectif

Développer l’automatisation du déploiement et de la gestion d’un cluster **Proxmox VE** à l’aide d’**Ansible**, dans un environnement virtualisé “Proxmox-in-Proxmox”.

---

##  Déroulé du projet

### Phase 1 – Provisionnement automatisé des nœuds Proxmox

- Création d’un **script shell** générant 3 ISOs d’installation automatique de Proxmox
- Paramétrage dynamique : FQDN, IP, mot de passe root, clés SSH, DNS, stockage ext4
- Création des **VMs Proxmox** avec configuration complète :
  - RAM, CPU, disques (ZFS + Ceph), contrôleurs, cartes réseau
  - ISO d’autoinstall, ordre de boot, désactivation du périphérique tablet

### Phase 2 – Configuration via Ansible

- Configuration réseau et dépôts :
  - Proxy APT, désactivation des dépôts entreprise, ponts vmbr1/vmbr2
- Mise en place du **cluster Proxmox** :
  - Création sur le nœud principal, jonction via SSH ou API
- Configuration du **stockage** :
  - Pool ZFS, ajout NFS, installation et configuration de Ceph
- Administration :
  - Création d’un utilisateur `admin` avec rôle `Administrator`

### Phase 3 – Gestion avancée avec Ansible

- **Gestion des conteneurs LXC** (Aurélie, Fabrice) :
  - Création, configuration, templates, instantanés

---

##  Environnement de travail

Hyperviseur Proxmox hébergeant le cluster virtuel.  
Connexion via machine de rebond et tunnel SOCKS :

---

##  Structure du dépôt

- `scripts/` : script shell de génération des ISOs
- `playbooks/` : playbooks Ansible pour la configuration des nœuds
- `group_vars/` : variables spécifiques aux machines (non versionnées)
- `roles/` : rôles Ansible pour cluster, stockage, réseau, etc.

---

##  Sécurité

Les fichiers contenant des variables sensibles (`group_vars/*.yml`) sont exclus du dépôt via `.gitignore`.  

---

##  Notes

- Le projet est réalisé dans un cadre pédagogique.
- Toute contribution ou amélioration est bienvenue via pull request.
