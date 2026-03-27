# projet-ota
présentation d'un projet 

OTA — OpenSource Tenant Architecture
Script Bash d'administration d'hébergement web mutualisé — Projet BTS SIO

Architecture du projet
ota/ ├── main.sh ← Point d'entrée — menu principal ├── lib/ │ └── colors.sh ← Couleurs ANSI & fonctions utilitaires partagées └── modules/ ├── check_deps.sh ← Vérification & installation des dépendances ├── user_management.sh ← Créer / Supprimer / Modifier / Lister les hébergements ├── database.sh ← Gestion des bases de données MariaDB/MySQL ├── ftp.sh ← Gestion des accès FTP (vsftpd) ├── web_files.sh ← Fichiers web + installation automatique de WordPress └── server_info.sh ← Tableau de bord et infos serveur

Installation & lancement
```bash

Cloner le projet
git clone https://github.com/votre-user/ota.git cd ota

Rendre les scripts exécutables
chmod +x main.sh modules/.sh lib/.sh

Lancer en tant que root
sudo bash main.sh ```

Note : Le script doit être exécuté en tant que root (ou via sudo). Au premier lancement, la vérification des dépendances s'effectue automatiquement.

Fonctionnalités
Vérification des dépendances (check_deps.sh)
Vérifie la présence de tous les paquets nécessaires : Apache2, MariaDB, vsftpd, PHP, quota, curl, wget, unzip, UFW
Installe automatiquement les paquets manquants via apt
Configure les services après installation (activation, démarrage, règles UFW)
S'exécute automatiquement au premier lancement
Gestion des hébergements (user_management.sh)
Créer : utilisateur Linux, arborescence /home/user/www, mot de passe, quota, VirtualHost Apache, accès FTP, base de données optionnelle
Supprimer : utilisateur, dossier home, VirtualHost, base de données, accès FTP
Modifier : mot de passe, quota, SSH on/off, base de données
Lister : tableau récapitulatif + détails par utilisateur
Bases de données (database.sh)
Création avec utilisateur dédié et mot de passe généré
Credentials sauvegardés dans /home/user/.db_credentials
Suppression propre (base + utilisateur MySQL)
Listing avec taille et nombre de tables
FTP (ftp.sh)
Activation/désactivation par utilisateur via /etc/vsftpd.userlist
Affichage des comptes actifs
Configuration vsftpd (mode passif, chroot)
Fichiers web (web_files.sh)
Visualisation de l'arborescence d'un site
Tableau récapitulatif de tous les sites
Installation automatique de WordPress : téléchargement, extraction, configuration wp-config.php, salts, permissions
Informations serveur (server_info.sh)
Système : hostname, OS, kernel, uptime, CPU, RAM
Stockage : utilisation des partitions
Hébergements : liste avec espace et URL
Services : état de Apache, MariaDB, vsftpd, UFW, SSH
Réseau : IP, ports ouverts
Charge : load average, top processus
Paquets gérés automatiquement
Paquet	Rôle
apache2	Serveur web
mariadb-server	Base de données
vsftpd	Serveur FTP
php + php-mysql	Interpréteur PHP
quota + quotatool	Gestion des quotas disque
curl + wget	Téléchargements
unzip	Décompression
ufw	Pare-feu
Arborescence générée par OTA
/home/ ├── client1/ │ ├── www/ │ │ └── index.html ← Page d'accueil générée automatiquement │ └── .db_credentials ← Identifiants DB (chmod 600) ├── client2/ │ └── www/ │ ├── wp-config.php ← Si WordPress installé │ └── ... /etc/apache2/sites-available/ ├── client1.conf ← VirtualHost Apache └── client2.conf /etc/vsftpd.userlist ← Whitelist FTP

Contraintes techniques respectées
Script 100% Bash
Utilisation de fonctions organisées par module
Menu interactif principal + sous-menus
Vérification des erreurs à chaque étape
Commentaires dans tout le code
Arborescence serveur conforme au cahier des charges
