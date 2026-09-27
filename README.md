# OpenTransit Fleet

![Version](https://img.shields.io/badge/version-v0.10.0-blue)
![Build](https://img.shields.io/badge/build-010-informational)
![PHP](https://img.shields.io/badge/PHP-8.1%2B-777BB4?logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL%20%2F%20MariaDB-supported-4479A1?logo=mysql&logoColor=white)

OpenTransit Fleet est une application web PHP/MySQL dédiée à la documentation des réseaux de transport et de leurs véhicules.

Le projet est conçu intégralement par l'intelligence artificielle, peut être installé facilement sur un hébergement mutualisé, directement par FTP, sans framework obligatoire ni système de compilation.

## Fonctionnalités

### Site public

- recherche de véhicules, réseaux et exploitants ;
- fiches détaillées des véhicules ;
- historique des affectations par réseau, exploitant, dépôt et ligne ;
- derniers ajouts ;
- statistiques de la base ;
- articles publiés depuis l’administration ;
- interface responsive mobile et ordinateur ;
- URLs propres compatibles avec une installation en sous-dossier.

### Fiches véhicules

Chaque véhicule peut contenir :

- numéro de parc ;
- constructeur et modèle ;
- immatriculation ;
- date de mise en circulation ;
- numéro de série ;
- longueur ;
- places assises, debout et UFR ;
- statut ;
- destination ;
- énergie ;
- norme Euro ;
- moteur ;
- boîte de vitesses ;
- nombre de portes ;
- livrée ;
- girouette ;
- climatisation ;
- informations complémentaires.

### Administration

- tableau de bord avec compteurs ;
- gestion des réseaux ;
- gestion des exploitants ;
- gestion des dépôts ;
- gestion des lignes ;
- gestion des véhicules ;
- import CSV de véhicules ;
- gestion des articles ;
- médiathèque et téléversement d’images ;
- gestion des utilisateurs ;
- modération des contributions ;
- journal d’activité ;
- recherche globale ;
- réglages du site et du référencement.

## Rôles utilisateurs

| Rôle | Accès |
|---|---|
| `admin` | Accès complet à l’administration et aux réglages sensibles |
| `contributor` | Création et modification des contenus autorisés |
| `member` | Compte utilisateur sans accès à l’administration |

Les comptes peuvent être activés ou suspendus. Les changements importants sont enregistrés dans le journal d’activité.

## SEO intégré

- titres et descriptions SEO éditables ;
- balise canonique ;
- Open Graph ;
- Twitter Cards ;
- données structurées JSON-LD ;
- `sitemap.xml` dynamique ;
- `robots.txt` dynamique ;
- slugs propres et uniques ;
- HTML sémantique ;
- compatibilité avec une installation dans un sous-dossier.

## Pré-requis

- PHP 8.1 ou supérieur ;
- MySQL 5.7+ ou MariaDB 10.4+ ;
- extension PDO MySQL activée ;
- Apache avec `mod_rewrite` ;
- accès FTP ou gestionnaire de fichiers ;
- HTTPS recommandé.

## Installation

1. Télécharger ou cloner le projet.
2. Envoyer le contenu du dossier sur l’hébergement, par exemple dans `/opentransit/`.
3. Ouvrir l’URL correspondant au dossier :

   ```text
   https://exemple.fr/opentransit/install.php
   ```

4. Renseigner les identifiants MySQL.
5. Renseigner le nom et la description du site.
6. Créer le premier compte administrateur.
7. Se connecter à l’administration.
8. Supprimer `install.php` après l’installation.

Le chemin d’installation est détecté automatiquement. Le projet fonctionne à la racine d’un domaine comme dans n’importe quel sous-dossier.

## Mise à jour

Pour mettre à jour une installation existante :

1. sauvegarder les fichiers et la base de données ;
2. envoyer les nouveaux fichiers par FTP ;
3. se connecter comme administrateur ;
4. ouvrir `upgrade.php` une seule fois ;
5. vérifier que la mise à niveau est terminée ;
6. supprimer `upgrade.php`.

La migration ajoute les nouvelles colonnes nécessaires sans supprimer les données existantes.

## Images et médiathèque

Les images téléversées sont classées automatiquement dans :

```text
uploads/AAAA/MM/
```

Exemple :

```text
uploads/2026/09/
```

Les uploads sont contrôlés par type MIME réel et protégés contre l’exécution de fichiers PHP.

## Sécurité

- requêtes SQL préparées avec PDO ;
- protection CSRF sur les formulaires ;
- échappement HTML des données affichées ;
- mots de passe hashés avec `password_hash()` ;
- limitation des tentatives de connexion ;
- sessions renforcées ;
- validation stricte des rôles et formulaires ;
- protection des fichiers sensibles ;
- contrôle MIME des images ;
- SVG non autorisés dans les uploads standards ;
- journalisation des actions d’administration.

## Structure principale

```text
admin/          Administration
assets/         Feuilles de style publiques et admin
uploads/        Images téléversées
examples/       Exemples de fichiers CSV
bootstrap.php   Initialisation, base de données et sessions
functions.php   Fonctions publiques, SEO et administration
index.php       Page d’accueil
entity.php      Fiches publiques
install.php     Installation initiale
upgrade.php     Migration d’une installation existante
schema.sql      Schéma complet de la base
VERSION         Numéro de version du build
```

## Version actuelle

**v0.10.0 — Build 010**

Cette version inclut notamment les fiches véhicules détaillées, les statistiques d’accueil, la compatibilité complète avec les sous-dossiers et l’administration responsive mobile.

## Licence

Projet open source. La licence peut être précisée dans un fichier `LICENSE` selon les besoins du projet.
