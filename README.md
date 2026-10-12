# ais_pfsense_OpenVPN
Mise en place d'un accès distant sécurisé par VPN SSL/TLS sous pfSense avec cloisonnement des réseaux

# 🔒 Sécurisation des Accès Distants par OpenVPN sous pfSense

## 📋 Présentation du projet
Ce projet réalisé dans le cadre de ma formation consiste à mettre en place une infrastructure d'accès distant sécurisé pour des collaborateurs en télétravail. 

L'objectif est de garantir l'interconnexion chiffrée entre un poste client et les ressources internes d'une entreprise via un pare-feu pfSense, en respectant un cloisonnement strict entre les réseaux WAN (externe) et LAN (interne).

## 🏗️ Architecture & Environnement technique
* **Pare-feu / Routeur :** pfSense (Interface WAN : `192.168.100.10` / Interface LAN : `192.168.172.254`).
* **Serveur Interne :** Serveur Web Apache sous Debian (`192.168.172.20`).
* **Client distant :** Poste Windows 10 simulé sur le réseau WAN (`192.168.100.201`) avec l'application *OpenVPN Connect*.
* **Outil de virtualisation :** VMware Workstation.

## ⚙️ Étapes de mise en œuvre

1. **Cloisonnement Réseau (WAN / LAN) :**
   * Isolation stricte des zones : le client externe ne peut pas joindre directement le serveur interne tant que le tunnel n'est pas établi.

2. **Mise en place de l'Infrastructure à Clés Publiques (PKI) sur pfSense :**
   * Génération d'une Autorité de Certification interne (`MonLab-CA`).
   * Création d'un certificat serveur OpenVPN et d'un certificat utilisateur dédié.

3. **Configuration du Service OpenVPN (SSL/TLS + User Auth) :**
   * Activation du service sur le port UDP `1194`.
   * Définition de la plage d'adresses IP virtuelles du tunnel (`10.0.80.0/24`).
   * Configuration du routage automatique vers le sous-réseau LAN (`192.168.172.0/24`).

4. **Tests de validation et d'étanchéité :**
   * **Phase 1 (Sans VPN) :** Échec des requêtes ping et de l'accès web vers le serveur interne, confirmant l'efficacité du filtrage pfSense.
   * **Phase 2 (Avec VPN) :** Obtention d'une IP virtuelle dans le tunnel, réussite du ping et affichage immédiat de la page web d'entreprise de manière totalement chiffrée (AES-256-GCM).

---
📁 *Projet documenté et validé dans le cadre de mon parcours technique.*
