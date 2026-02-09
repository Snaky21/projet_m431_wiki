# 👋 Bienvenue sur le Portail Étudiant M431

Ce site est votre point de repère pour tous les outils informatiques du cours. Vous y trouverez votre emploi du temps, des commandes pratiques, et la documentation de notre infrastructure.

---

## 🚀 Accès Rapides

<div class="grid cards" markdown>

-   :material-clock-outline: **Mon Emploi du Temps**
    ---
    Consultez les horaires de cours, les pauses et les salles.
    [:arrow_right: Voir les horaires](schedule.md)

-   :material-console: **Commandes Utiles**
    ---
    Trouver son IP, nettoyer son cache, vérifier le réseau...
    [:arrow_right: Les commandes PC](commands.md)

-   :material-server-network: **Infrastructure**
    ---
    Comprendre comment fonctionne le serveur (Docker, Traefik).
    [:arrow_right: Voir l'architecture](#3-architecture-du-systeme)

</div>

---

## 📑 Rapport de Projet : Infrastructure Automatisée

**Sujet :** Automatisation du routage et sécurisation SSL pour services auto-hébergés.
**Objectif :** Créer une plateforme capable d'accueillir n'importe quel projet Docker en garantissant sécurité et accessibilité. 🛠️

---

### 1. 🛠️ Méthodologie de Projet (6 Étapes)

Pour mener à bien ce projet, nous avons suivi une méthode rigoureuse :

1.  **🔍 Informer :** Analyse du besoin d'un portail centralisé pour les étudiants.
2.  **📅 Planifier :** Utilisation d'un Gantt pour séquencer l'installation (OS -> Docker -> Services).
3.  **🧠 Décider :** Choix de **Traefik** pour son automatisation et de **DuckDNS** pour le SSL gratuit.
4.  **⚙️ Réaliser :** Configuration du `docker-compose.yml`, du réseau `proxy-net` et rédaction de la doc.
5.  **🕹️ Contrôler :** Tests d'accès externes (4G) et vérification du renouvellement des certificats.
6.  **📝 Évaluer :** Rédaction de ce Wiki et préparation de la soutenance.

---

### 2. 🎯 Présentation du Concept Technique

Ce projet vise à mettre en place un environnement serveur moderne où chaque application est isolée dans un **conteneur Docker**. L'intelligence du système réside dans sa capacité à :
* Identifier les nouveaux services sans intervention humaine. 🤖
* Attribuer des adresses web claires (ex: `wiki.ton-domaine.duckdns.org`).
* Sécuriser les échanges via le protocole **HTTPS** (certificats SSL). 🔒

---

### 3. 🏗️ Architecture du Système

#### A. Le Nom de Domaine (DuckDNS) 🦆
Plutôt que d'acheter un domaine coûteux, nous utilisons **DuckDNS**.
* **Le rôle :** Il fournit une adresse fixe et gratuite.
* **La magie SSL :** Grâce à l'API DuckDNS, notre serveur prouve son identité à l'autorité **Let's Encrypt** via un "DNS Challenge".

#### B. L'Aiguilleur : Le Reverse Proxy 🚦
C'est le composant central qui distribue les requêtes aux bons conteneurs.

| Solution | Style | Atout Majeur |
| :--- | :--- | :--- |
| **Traefik Proxy** | ⚙️ Automatique | Détection des services par "labels". C'est le standard industriel. |

---

### 4. 🧠 Les Fondations (Prérequis)

Pour aller plus loin, cliquez sur les liens pour voir les détails techniques :

* **Docker & Docker Compose :** La base de la conteneurisation. [👉 Voir l'explication](explication_prerequis/docker_explication.md)
* **Syntaxe YAML :** Pour rédiger les configurations. [👉 Voir l'explication](explication_prerequis/syntaxe_yaml_explication.md)
* **Réseautage virtuel :** Comprendre le réseau `proxy-net`. [👉 Voir l'explication](explication_prerequis/reseautage_virtuel_explication.md)
* **Gestion DNS :** Comprendre le lien IP <-> Domaine. [👉 Voir l'explication](explication_prerequis/gestion_dns_explication.md)

---

## ❓ À propos de ce projet

Ce projet a été conçu par l'équipe suivante dans le cadre du module M431 :

<div class="grid cards" markdown>

-   :fontawesome-solid-user: **Gabriel**

-   :fontawesome-solid-user: **Jonathan**

-   :fontawesome-solid-user: **Kévin**

-   :fontawesome-solid-user: **Rafael**

</div>

Si vous trouvez une erreur ou souhaitez ajouter une commande, n'hésitez pas à nous le signaler sur GitHub !

!!! tip "Le saviez-vous ?"
    Vous pouvez utiliser la barre de recherche en haut à droite pour trouver rapidement une commande spécifique (ex: "ip config").