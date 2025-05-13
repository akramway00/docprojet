---
{"dg-publish":true,"permalink":"/projet3-cyber-city/documentation-page-principal/","tags":["gardenEntry"]}
---

# Introduction au Projet

Bienvenue dans la documentation de CyberCity. Ce projet est une application web complète permettant de créer, gérer et jouer à des jeux de plateau en temps réel. L'application est construite sur une architecture client-serveur moderne, utilisant Angular pour le frontend et Node.js avec TypeScript pour le backend.
# Architecture Globale

L'application est divisée en deux parties principales qui communiquent entre elles :
### Client (Frontend)

- Développé avec **Angular**
- Interface utilisateur interactive et réactive
- Communication en temps réel via Socket.IO
- Animations et transitions fluides entre les différentes vues

### Serveur (Backend)

- Développé avec **Node.js** et **TypeScript**
- Architecture orientée services avec injection de dépendances (TypeDI)
- Communication en temps réel via Socket.IO
- Persistance des données avec MongoDB
- Logique de jeu complexe (déplacement, combat, IA)

## Flux de données et Communication

La communication entre le client et le serveur se fait principalement de deux manières :

1. **API REST** : Utilisée pour les opérations CRUD sur les jeux (Create, Read, Update, Delete)
    - Endpoints exposés par le `GameManagerController`
    - Utilisée principalement pour la gestion administrative des jeux
    
2. **WebSockets (Socket IO)** : Communication bidirectionnelle en temps réel
    - Utilisée pour toutes les interactions de jeu (déplacements, combats, chat)
    - Mise à jour instantanée de l'état du jeu pour tous les joueurs
    - Système d'événements et de salles pour isoler les communications par partie

Le diagramme (à venir tkt ...)  suivant illustre le **flux typique** d'une partie :

1. Le joueur se connecte à l'application
2. Il crée une partie ou rejoint une partie existante via un code
3. Les joueurs se retrouvent dans une salle d'attente
4. La partie commence, le serveur gère l'état du jeu et les tours
5. Les joueurs interagissent via l'interface, envoyant des commandes au serveur
6. Le serveur traite les commandes, met à jour l'état du jeu et diffuse les mises à jour
7. À la fin de la partie, les statistiques sont calculées et affichées
# Organisation de la Documentation

La documentation est organisée en trois sections principales pour faciliter la navigation et la compréhension du projet :

### 1. Documentation Principale (Vous êtes ici)

- Vue d'ensemble du projet
- Architecture globale
- Organisation de la documentation
- Guide de démarrage

### 2. [[Projet3-CyberCity/Documentation Coté Client\|Documentation Coté Client]]

La documentation côté client est organisée par pages et fonctionnalités principales :

- **Pages** : Documentation détaillée des 9 principales pages de l'application
    - Page d'Accueil
    - Administration des Jeux
    - Édition de Jeu
    - Création de Partie
    - Création de Personnage
    - Salle d'Attente
    - Vue de Jeu
    - Statistiques
    - Application Principale
- **Services et Composants** : Explications des services et composants réutilisables
    - Services de communication avec le serveur
    - Composants d'interface utilisateur
    - Gestion des états et animations

### 3. [[Projet3-CyberCity/Documentation Coté Serveur\|Documentation Coté Serveur]]

La documentation côté serveur est organisée par domaines fonctionnels :

- **Infrastructure et Configuration** : Mise en place du serveur
- **Gestion des WebSockets** : Communication en temps réel
- **Gestion des Parties** : Logique de jeu principale
- **Système de Combat** : Mécanique des combats
- **Gestion des Items** : Objets et interactions
- **Gestion des Joueurs** : Joueurs humains et IA
- **Contrôle de Jeu et Vérification** : Validation et règles
- **Système du Chatbox** : Communication entre joueurs
- **Classes du Jeu** : Structures de données principales
# Par où commencer ?

Si vous découvrez ce projet :

1. **Pour comprendre la structure globale** :
    - Commencez par cette page principale pour avoir une vue d'ensemble
    - Consultez la section "Application Principale" dans la documentation client et “Infrastructure et Configuration” dans la documentation serveur.
2. **Pour comprendre le flux utilisateur** :
    - Explorez les pages dans l'ordre d'utilisation typique :
        - Page d'Accueil → Création de Partie → Création de Personnage → Salle d'Attente → Vue de Jeu → Statistiques
3. **Pour comprendre la logique du jeu** :
    - Consultez la section "Gestion des Parties" dans la documentation serveur
    - Puis explorez le "Système de Combat" et la "Gestion des Joueurs"
4. **Pour comprendre l'interaction en temps réel** :
    - Consultez la section "Gestion des WebSockets" dans la documentation serveur
    - Puis explorez les services de communication dans la documentation client

# Entités Principales du Jeu

Pour mieux comprendre le domaine du jeu, voici les principales entités et leurs relations :

- **Game** : Définition d'un jeu (grille, mode, taille)
- **OnGoingGame** : État d'une partie en cours
- **Player** : Informations sur un joueur
- **Bot** : Extension de Player pour les IA (défensives et agressives)
- **Combat** : État d'un combat entre joueurs
- **Cell** : Cellule de la grille de jeu
- **Item** : Objets que les joueurs peuvent collecter