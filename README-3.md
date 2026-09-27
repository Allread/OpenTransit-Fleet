# OpenTransit Fleet

![Version](https://img.shields.io/badge/version-v0.52.9-blue)
![Build](https://img.shields.io/badge/build-062-informational)
![PHP](https://img.shields.io/badge/PHP-8.1%2B-777BB4?logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL%20%2F%20MariaDB-supported-4479A1?logo=mysql&logoColor=white)
![License](https://img.shields.io/badge/license-TBD-lightgrey)

**OpenTransit Fleet** est une application web PHP/MySQL de documentation collaborative des réseaux de transport en commun : réseaux, exploitants, lignes, dépôts et véhicules, avec leur historique.

Le projet est pensé pour un déploiement simple sur hébergement mutualisé — envoi par FTP, aucun framework, aucune étape de compilation — tout en restant capable d'importer automatiquement les données ouvertes du [Point d'Accès National (PAN)](https://transport.data.gouv.fr).

## Sommaire

- [Ce qui différencie OpenTransit Fleet](#ce-qui-différencie-opentransit-fleet)
- [Fonctionnalités](#fonctionnalités)
- [Rôles utilisateurs](#rôles-utilisateurs)
- [Pré-requis](#pré-requis)
- [Installation](#installation)
- [Mise à jour](#mise-à-jour)
- [Structure du projet](#structure-du-projet)
- [Sécurité](#sécurité)
- [Contribuer](#contribuer)
- [Historique des versions](#historique-des-versions)
- [Licence](#licence)

## Ce qui différencie OpenTransit Fleet

- **Import national automatisé** — synchronisation des réseaux, exploitants et lignes depuis le catalogue GTFS du PAN, avec correspondance approximative et validation manuelle avant écriture.
- **Sourcing par champ et historique public** — chaque donnée technique peut être rattachée à une source vérifiable, et les modifications approuvées sont visibles publiquement, façon wiki.
- **Provenance inter-réseaux** — suivi des transferts et cessions de véhicules d'un réseau à l'autre, pas seulement des affectations internes.
- **Thèmes importables** — palette, typographies et rayons de bordure pilotés par un jeu de tokens CSS, modifiable depuis l'administration sans toucher au code.
- **Déploiement FTP classique** — aucune dépendance, aucun build ; PHP et MySQL suffisent.

## Fonctionnalités

### Site public

- Recherche dédiée (véhicules, réseaux, exploitants, lignes).
- Fiches détaillées par véhicule, réseau, exploitant et ligne.
- Historique des affectations et des transferts de véhicules entre réseaux.
- Photothèque par véhicule.
- Annuaires des réseaux, exploitants et lignes, avec couleur officielle par ligne.
- Articles publiés depuis l'administration.
- Espace membre public (inscription, connexion, page de compte).
- Formulaire de contribution/signalement avec catégorie, priorité et source.
- Interface responsive, URLs propres, compatible sous-dossier.

### Fiches véhicules

Numéro de parc, constructeur, modèle, immatriculation, date de mise en circulation, numéro de série, longueur, places assises/debout/UFR, statut, destination, énergie, norme Euro, moteur, boîte de vitesses, nombre de portes, livrée, girouette, climatisation, informations complémentaires.

### Administration

- Tableau de bord avec compteurs, gestion paginée des réseaux/exploitants/dépôts/lignes/véhicules (suppression individuelle et groupée).
- Ajout rapide de véhicule avec autocomplétion (constructeur, énergie, norme Euro, boîte de vitesses) et vérification des correspondances réseau/exploitant/ligne/dépôt.
- Import CSV de véhicules et import GTFS national depuis le PAN (mode test disponible).
- Médiathèque, gestion des utilisateurs, modération des contributions, journal d'activité.
- Sources vérifiées par champ et historique des modifications, avec validation admin.
- Pied de page public éditable, gestion de thème (palette et typographies).
- Réglages du site et du référencement.

## Rôles utilisateurs

| Rôle | Accès |
|---|---|
| `admin` | Accès complet à l'administration et aux réglages sensibles |
| `contributor` | Création et modification des contenus autorisés |
| `member` | Compte utilisateur public, sans accès à l'administration |

Les comptes peuvent être activés ou suspendus ; les changements importants sont journalisés.

## Pré-requis

- PHP 8.1 ou supérieur, extension PDO MySQL activée.
- MySQL 5.7+ ou MariaDB 10.4+.
- Apache avec `mod_rewrite` (le `.htaccess` fourni gère la réécriture d'URL et le blocage des fichiers sensibles).
- Accès FTP ou gestionnaire de fichiers.
- HTTPS recommandé.

## Installation

1. Cloner ou télécharger le dépôt.
2. Envoyer le contenu du dossier sur l'hébergement (à la racine ou dans un sous-dossier).
3. Ouvrir `install.php` depuis un navigateur.
4. Renseigner les identifiants MySQL, le nom du site, et créer le premier compte administrateur.
5. Se connecter à l'administration.
6. **Supprimer `install.php` après l'installation.**

Le chemin d'installation est détecté automatiquement — le projet fonctionne aussi bien à la racine d'un domaine que dans un sous-dossier.

## Mise à jour

1. Sauvegarder les fichiers et la base de données.
2. Envoyer les nouveaux fichiers par FTP.
3. Se connecter en tant qu'administrateur.
4. Ouvrir `upgrade.php` une seule fois, vérifier que la migration s'est terminée sans erreur.
5. **Supprimer `upgrade.php`.**

La migration ajoute les nouvelles colonnes/tables nécessaires sans supprimer les données existantes.

## Structure du projet

```text
admin/          Administration (gestion de contenu, import GTFS, thème, utilisateurs...)
assets/         Feuilles de style publiques et admin
uploads/        Images téléversées (classées par année/mois)
examples/       Exemples de fichiers CSV
storage/        Fichiers temporaires (imports GTFS, cache PAN) — protégés par .htaccess
bootstrap.php   Initialisation, base de données, sessions, thème
functions.php   Fonctions publiques, SEO, gabarits d'en-tête/pied de page
index.php       Page d'accueil
entity.php      Fiches publiques (réseau, exploitant, ligne, véhicule, article)
install.php     Installation initiale
upgrade.php     Migration d'une installation existante
schema.sql      Schéma complet de la base
VERSION         Numéro de version du build
```

## Sécurité

- Requêtes SQL exclusivement préparées (PDO).
- Protection CSRF sur tous les formulaires, échappement HTML systématique en sortie.
- Mots de passe hashés (`password_hash()`), limitation des tentatives de connexion par IP et par compte.
- Sessions renforcées (`HttpOnly`, `SameSite`, régénération d'identifiant).
- Contrôle MIME réel des images téléversées (SVG non autorisé), protection contre l'exécution de fichiers dans `uploads/`.
- Connexions sortantes du PAN restreintes aux hôtes publics (IP privées/réservées refusées, redirections revalidées).
- Fichiers sensibles (`config.php`, `schema.sql`, `.installed`) bloqués par `.htaccess`.
- Journalisation des actions d'administration.

Une revue de sécurité a lieu à chaque version ; les retours sont bienvenus via les issues.

## Contribuer

- Le formulaire public **Signaler une information** permet à n'importe quel visiteur de proposer une correction, avec catégorie, priorité et source.
- Les comptes `contributor` peuvent créer et modifier directement les contenus (réseaux, exploitants, lignes, véhicules, articles) ; leurs modifications techniques passent par le circuit de sources/historique modérable.
- Pour contribuer au code : ouvrir une issue avant une pull request importante, garder les correctifs ciblés sur un fichier ou une fonctionnalité, et vérifier `php -l` sur les fichiers modifiés avant de proposer un correctif.

## Historique des versions

Voici les grandes lignes des dernières versions ; le détail complet peut être tenu dans un `CHANGELOG.md` séparé si le suivi devient trop long pour ce fichier.

**v0.52.9 — Build 062** — Page d'administration « Listes » pour les valeurs d'autocomplétion des véhicules ; correctifs de fiabilité sur `upgrade.php`.

**v0.52.6 — Build 059** — Espace membre public (inscription/connexion unifiées), page de recherche dédiée `/recherche`, navigation mobile, suppression groupée des lignes.

**v0.51 – v0.49** — Import national paginé depuis le PAN avec validation manuelle, sources vérifiées par champ et historique public modérable, photothèque et provenance inter-réseaux des véhicules, durcissement des connexions sortantes du PAN (SSRF), imports/suppressions transactionnels.

## Licence

Projet open source. La licence précise reste à définir dans un fichier `LICENSE` séparé.
