Parfait. Voici **le cahier des charges COMPLET, consolidé et mis à jour**, intégrant **eShop**, **AWS**, **PostgreSQL**, **Redis** et **l’ensemble de votre stack DevOps**.  
Il est **clé‑en‑main**, conforme aux attentes **DataScientest + jury RNCP**, et prêt à être déposé tel quel dans ton dépôt Git.

***

# 📘 Cahier des charges

## Projet Fil Rouge DevOps – Formation Ingénieur DevOps DataScientest

***

## 1. Contexte du projet

Ce projet fil rouge est réalisé dans le cadre de la formation **Ingénieur DevOps – DataScientest**, ayant pour objectif la validation du titre professionnel RNCP **Administrateur Système DevOps (RNCP36061)**.

Le projet s’appuie sur une application existante, **eShop**, projet open source maintenu par Microsoft, représentant une **application e‑commerce basée sur une architecture microservices en .NET**.

Bien que l’application soit fonctionnelle, elle **ne respecte pas nativement les principes DevOps** attendus dans un environnement de production moderne (automatisation, scalabilité, observabilité, sécurité, etc.).  
Le projet vise donc à **industrialiser l’application eShop** en mettant en œuvre une **chaîne DevOps complète**, reposant sur des technologies cloud et open‑source.

***

## 2. Objectifs du projet

### 2.1 Objectif principal

Mettre en place une **architecture DevOps complète, automatisée, sécurisée et scalable** autour de l’application eShop, couvrant l’ensemble de son cycle de vie :

*   développement
*   déploiement
*   exploitation
*   supervision

### 2.2 Objectifs secondaires

*   Déployer l’application sur une infrastructure **Cloud AWS**
*   Automatiser les déploiements via une **pipeline CI/CD**
*   Mettre en place des environnements **Développement** et **Production** distincts
*   Garantir la **haute disponibilité** des services
*   Assurer la **sécurité et la persistance des données**
*   Superviser l’application et l’infrastructure
*   Fournir une documentation technique claire et structurée

***

## 3. Présentation de l’application eShop

### 3.1 Description générale

*   Nom : **eShop**
*   Type : Application e‑commerce
*   Architecture : **Microservices**
*   Langage : **.NET**
*   Communication : REST / HTTP
*   Dépôt officiel : <https://github.com/dotnet/eShop>

### 3.2 Composants applicatifs

*   Front‑end Web
*   Microservices back‑end :
    *   Catalog
    *   Ordering
    *   Basket
    *   Identity
    *   Payment (selon implémentation)
*   Bases de données par service
*   Cache distribué

L’architecture microservices de eShop se prête particulièrement bien à :

*   la conteneurisation
*   l’orchestration Kubernetes
*   la mise en œuvre des principes DevOps

***

## 4. Analyse de l’existant (constat DevOps)

L’analyse de l’application eShop montre les limites suivantes dans son état initial :

*   Déploiements majoritairement manuels ou semi‑automatisés
*   Absence d’Infrastructure as Code complète
*   Pas de pipeline CI/CD orientée production
*   Sécurité insuffisamment formalisée (secrets, réseau)
*   Monitoring non intégré par défaut
*   Environnements peu clairement séparés

Ces limitations motivent la **refonte DevOps de l’architecture** et la mise en place d’une **chaîne d’industrialisation complète**.

***

## 5. Périmètre du projet

### ✅ Inclus dans le périmètre

*   Import et organisation de l’application eShop dans un repository Git dédié
*   Conteneurisation avec Docker
*   Déploiement local/dev via Docker Compose
*   Déploiement production via Kubernetes
*   Provisionnement Cloud AWS avec Terraform
*   Configuration des systèmes avec Ansible
*   Mise en place d’une CI/CD GitLab
*   Gestion des données avec PostgreSQL et Redis
*   Supervision avec Prometheus et Grafana

### ❌ Hors périmètre

*   Développement de nouvelles fonctionnalités métiers
*   Refonte fonctionnelle de l’application eShop

***

## 6. Stack technique retenue

### 6.1 Cloud & infrastructure

*   **AWS**
    *   VPC
    *   EC2 / EKS
    *   Load Balancer
    *   Stockage persistant

### 6.2 Infrastructure as Code & Configuration

*   **Terraform** : provisioning des ressources AWS
*   **Ansible** : configuration des systèmes et services

### 6.3 Conteneurisation & orchestration

*   **Docker**
*   **Docker Compose** (environnement de développement)
*   **Kubernetes** (environnement de production)

### 6.4 CI/CD

*   **GitLab**
*   **GitLab CI/CD**

### 6.5 Données

*   **PostgreSQL** : base relationnelle (données métiers persistantes)
*   **Redis** : cache et données temporaires

### 6.6 Monitoring & observabilité

*   **Prometheus**
*   **Grafana**

***

## 7. Architecture des données

### 7.1 PostgreSQL

Utilisée pour :

*   données transactionnelles
*   données métiers critiques
*   persistance long terme

Exemples :

*   produits
*   commandes
*   utilisateurs

### 7.2 Redis

Utilisée pour :

*   cache applicatif
*   paniers utilisateurs
*   sessions

### 7.3 Vue logique

    Microservices eShop
         |
         |----> Redis (Cache, Panier, Sessions)
         |
         |----> PostgreSQL (Produits, Commandes, Utilisateurs)

***

## 8. Exigences fonctionnelles

*   L’application doit rester fonctionnelle après transformation DevOps
*   Les données doivent être persistantes
*   Les services doivent être accessibles sans interruption majeure
*   Les sauvegardes doivent être restaurables

***

## 9. Exigences techniques DevOps

### 9.1 Gestion du code

*   Un repository Git source unique
*   Organisation claire du code
*   Traçabilité des changements

### 9.2 Déploiement & automatisation

*   Déploiement automatisé via CI/CD
*   Séparation dev / prod
*   Rolling update sur Kubernetes

### 9.3 Sécurité

*   Gestion sécurisée des secrets
*   Isolation réseau
*   Accès contrôlés

### 9.4 Haute disponibilité

*   Réplication des services
*   Load balancing
*   Tolérance aux pannes

### 9.5 Supervision

*   Collecte de métriques applicatives et systèmes
*   Dashboards lisibles
*   Alertes en cas d’incident

***

## 10. Architecture DevOps cible (vue globale)

    Développeur
       ↓
    GitLab Repository
       ↓
    GitLab CI/CD
       ↓
    Docker Registry
       ↓
    Environnement DEV (Docker Compose)
       ↓ validation
       ↓
    Environnement PROD (AWS + Kubernetes)
       ↓
    PostgreSQL / Redis
       ↓
    Prometheus / Grafana

Un schéma détaillé (Draw\.io) complètera cette vue conceptuelle.

***

## 11. Organisation du repository Git

    eshop-devops/
    ├── app/                     # Code applicatif eShop
    ├── docker/                  # Dockerfiles
    ├── docker-compose/          # Environnement dev
    ├── k8s/                     # Manifests Kubernetes
    ├── terraform/               # Infrastructure AWS
    ├── ansible/                 # Configuration
    ├── gitlab-ci/               # Pipelines CI/CD
    ├── monitoring/              # Prometheus / Grafana
    ├── db/
    │   ├── postgres/
    │   └── redis/
    ├── docs/
    │   ├── cahier-des-charges.md
    │   ├── architecture.md
    │   └── schema-devops.drawio
    └── README.md

***

## 12. Livrables – Étape 1

*   ✅ Cahier des charges (ce document)
*   ✅ Application eShop importée et organisée dans Git
*   ✅ Repository structuré et documenté
*   ✅ Schéma d’architecture DevOps cible

***

## 13. Critères de validation

*   Compréhension claire du projet et des enjeux DevOps
*   Cohérence des choix techniques
*   Documentation professionnelle
*   Base technique solide pour la suite des étapes

***

# ✅ Statut

✅ **Étape 1 : VALIDABLE ET COMPLÈTE**

***