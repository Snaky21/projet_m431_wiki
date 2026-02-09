# 📅 Planification du Projet M431

Voici le déroulement prévisionnel de notre projet, de la conception à la livraison finale.

## 📌 Diagramme de Gantt

```mermaid
gantt
    title Roadmap du Projet Infrastructure Étudiant
    dateFormat  YYYY-MM-DD
    axisFormat  %d/%m

    section 🧠 Conception
    Brainstorming & Idée        :done,    des1, 2026-02-01, 2d
    Choix de la Stack Tech      :done,    des2, after des1, 2d
    Architecture Réseau         :active,  des3, after des2, 3d

    section 🏗️ Infrastructure
    Installation Docker/OS      :         inf1, after des3, 2d
    Config Traefik & DuckDNS    :         inf2, after inf1, 3d
    Sécurisation SSL            :         inf3, after inf2, 2d

    section 📦 Services
    Mise en place Homepage      :         serv1, after inf3, 2d
    Déploiement Wiki (Zensical) :         serv2, after serv1, 2d
    Config Portainer            :         serv3, after serv1, 1d

    section 📝 Documentation
    Rédaction Guides (Markdown) :         doc1, after serv2, 5d
    Peaufinage & Tests          :         doc2, after doc1, 3d

    section 🚀 Rendu
    Préparation Présentation    :crit,    rendu, 2026-02-25, 3d
    Rendu Final                 :milestone, 2026-02-28, 0d

```

## 📋 Répartition des tâches

| Phase | Responsable(s) | Statut |
| --- | --- | --- |
| **Architecture** | Gabriel | ✅ Terminé |
| **Traefik & Réseau** | X | 🔄 En cours |
| **Homepage & Design** | X | ⏳ À faire |
| **Documentation** | X| ⏳ À faire |

---

> *Note : Ce planning est susceptible d'évoluer en fonction des contraintes techniques rencontrées.*