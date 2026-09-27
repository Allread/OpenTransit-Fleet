# OpenTransit Fleet

Socle open source pour créer rapidement un site de documentation et de suivi d'un parc de transport public.

La première version est une démo statique : elle montre l'interface cible et des données fictives. Les données réelles ne sont pas encore connectées à une base de données.

## Objectif du projet

OpenTransit Fleet doit permettre à une association, un passionné ou un exploitant de publier son propre inventaire :

- véhicules, modèles et constructeurs ;
- réseaux, exploitants, dépôts et lignes ;
- historique des affectations, immatriculations et numéros de parc ;
- photos, mouvements et statuts ;
- recherche publique et espace d'administration ;
- import/export CSV puis API.

## Démarrer la démo

La démo ne nécessite ni serveur ni dépendance : ouvrir `dist/index.html` dans un navigateur ou servir le dossier `dist/` avec n'importe quel serveur statique.

## Feuille de route V1

1. Modèle de données historisé et base SQLite/PostgreSQL.
2. Assistant d'installation et configuration du réseau.
3. Authentification et rôles contributeur/administrateur.
4. CRUD véhicules, lignes, dépôts, exploitants et affectations.
5. Import CSV avec correspondance des colonnes.
6. Pages publiques indexables et API JSON.
7. Photos, modération des signalements et exports.

## Licence

MIT — voir `LICENSE`.
