---
{"dg-publish":true,"permalink":"/projet3-cyber-city/documentation-cote-client/"}
---

# Documentation Coté Client

Cette documentation présente la structure et le fonctionnement du côté client de l'application, organisée autour des principales pages et fonctionnalités de manière globale. Pour consulter la documentation détaillée de chaque page, cliquez sur le titre correspondant.
# Architecture Générale

L'application est développée avec Angular et suit une architecture modulaire. Elle est composée de:

- **Pages**: 9 pages principales qui constituent les vues de l'application
- **Composants**: Éléments réutilisables qui composent les pages
- **Services**: Logique métier et communication avec le serveur
- **Classes**: Modèles de données et entités
- **Interfaces**: Contrats de données

L'application utilise principalement Socket.IO pour les communications en temps réel avec le serveur, particulièrement pour le jeu, le clavardage et les mises à jour d'état.
# Organisation par Pages

### [[Projet3-CyberCity/Coté Client/1. Page d'Accueil\|1. Page d'Accueil]] (MainPageComponent)

**Fonctionnalité**: Point d'entrée de l'application permettant de naviguer vers les autres sections.

**Services utilisés**:  `JoinCharacterCreationService`: Permet de rejoindre une partie existante

**Composants**:
- `ButtonComponent`: Boutons de navigation customisés

**Éléments de la page**:
- Popup de saisie de code pour rejoindre une partie
- Logo de l'application
- Cadre avec boutons de navigation

**Navigation possible vers**:
- Création de partie
- Administration des jeux
- Rejoindre une partie existante (via code)

### [[Projet3-CyberCity/Coté Client/2. Administration des Jeux\|2. Administration des Jeux]] (AdminPageComponent)

**Fonctionnalité**: Interface pour gérer les jeux disponibles (création, édition, suppression).

**Services utilisés**:
- `GameService`: CRUD (Create, Read, Update, Delete) des jeux dans la base de données
- `EditService`: Gestion de l'édition des jeux

**Composants**:
- `GameBoxComponent`: Affichage d'un jeu
- `OneButtonPopupComponent`: Popups d'information et d'erreur
- `TwoButtonsPopupComponent`: Popups de confirmation

**Éléments de la page**:
- Grille d'affichage des jeux
- Boutons de navigation
- Flèches de pagination
- Popup de création d'un nouveau jeu

**Navigation possible vers**:
- Édition de jeu (EditionPageComponent)
- Création de jeu
- Page d'accueil (MainPageComponent)
### [[Projet3-CyberCity/Coté Client/3. Édition de Jeu\|3. Édition de Jeu]] (EditionPageComponent)

**Fonctionnalité**: Interface pour créer ou modifier un jeu (grille, tuiles, items).

**Services utilisés**:
- `EditService`: Gestion de l'édition et vérification
- `GameService`: Sauvegarde du jeu
- `AutoTileService`: Logique des tuiles pour les murs

**Composants**:
- `GridComponent`: Grille de jeu éditable
- `TilesContainerComponent`: Sélection des tuiles
- `ItemsContainerComponent`: Sélection des items
- `DescriptionEditingComponent`: Édition des métadonnées
- `CellComponent`: Affichage d'une cellule de la grille

**Éléments de la page**:
- Zone de la grille de jeu
- Zone des contrôles d'édition
- Popups de confirmation et d'erreur

**Navigation possible vers**:
- Administration des jeux (AdminPageComponent)
### [[Projet3-CyberCity/Coté Client/4. Création de Partie\|4. Création de Partie]] (GameCreationPageComponent)

**Fonctionnalité**: Sélection d'un jeu pour lancer une partie.

**Services utilisés**:
- `GameService`: Récupération des jeux disponibles
- `GameCreationService`: Gestion de la sélection

**Composants**:
- `GameBoxComponent`: Affichage des jeux disponibles
- `OneButtonPopupComponent`: Message d'erreur ou d'information

**Éléments de la page**:
- Grille d'affichage des jeux
- Boutons de navigation
- Flèches de pagination

**Navigation possible vers**:
- Création de personnage (CharacterCreationPageComponent)
- Page d'accueil (MainPageComponent)
### [[Projet3-CyberCity/Coté Client/5. Création de Personnage\|5. Création de Personnage]] (CharacterCreationPageComponent)

**Fonctionnalité**: Création du personnage avant de rejoindre une partie.

**Services utilisés**:
- `CharacterCreationService`: Création du personnage et de la partie
- `GameCreationService`: Récupération du jeu sélectionné
- `WaitingRoomService`: Communication avec la salle d'attente
- `GameService`: Vérification de la disponibilité du jeu

**Composants**:
- `OneButtonPopupComponent`: Messages d'erreur et d'information

**Éléments de la page**:
- Sélecteur d'avatar avec carousel
- Champ de saisie du nom
- Sélection d'attributs (vie, rapidité, attaque, défense)
- Options de bonus et dé
- Boutons de navigation

**Navigation possible vers**:
- Salle d'attente (WaitingRoomPageComponent)
- Page d'accueil (MainPageComponent) ou sélection de jeu (GameCreationPageComponent)

### [[Projet3-CyberCity/Coté Client/6. Salle d'Attente\|6. Salle d'Attente]] (WaitingRoomPageComponent)

**Fonctionnalité**: Interface où les joueurs se regroupent avant le début de la partie.

**Services utilisés**:
- `WaitingRoomService`: Gestion de la salle d'attente
- `CharacterCreationService`: Obtention des informations du joueur
- `ChatService`: Communication entre joueurs

**Composants**:
- `ChatboxComponent`: Système de chat
- `OneButtonPopupComponent`: Messages d'information
- `TwoButtonsPopupComponent`: Confirmations

**Éléments de la page**:
- Grille des joueurs présents
- Code d'accès à la salle
- Contrôles d'administration (verrouillage, démarrage)
- Options d'ajout de joueurs virtuels
- Mini-jeu d'animation néon

**Navigation possible vers**:
- Vue de jeu (GameViewPageComponent) (quand la partie commence)
- Page d'accueil (MainPageComponent) (annulation)

### [[Projet3-CyberCity/Coté Client/7. Vue de Jeu\|7. Vue de Jeu]] (GameViewPageComponent)

**Fonctionnalité**: Interface principale du jeu où se déroule la partie.

**Services utilisés**:
- `GameViewService`: Logique principale du jeu
- `CombatService`: Gestion des combats
- `StatsService`: Suivi des statistiques
- `LogService`: Journal des événements

**Composants**:
- `GridComponent`: Grille de jeu
- `CellComponent`: Affichage des cellules
- `PlayerInfoComponent`: Information sur le joueur
- `PlayerCommandsComponent`: Commandes de jeu
- `PlayersListComponent`: Liste des joueurs
- `CombatMenuComponent`: Interface de combat
- `ChatboxComponent`: Chat entre joueurs
- `GameLogComponent`: Journal des événements
- `GameInfoComponent`: Informations sur la partie
- `TimerComponent`: Affichage du temps restant
- `AlertNotificationComponent`: Notifications
- `TileInformationComponent`: Information sur les tuiles
- `ItemRejectPopupComponent`: Gestion de l'inventaire
- `OneButtonPopupComponent`: Messages d'information
- `TwoButtonsPopupComponent`: Confirmations

**Éléments de la page**:
- Disposition en trois colonnes (profil, grille, infos)
- Bouton de contrôle de musique
- Popups de fin de partie et d'abandon

**Navigation possible vers**:
- Page des statistiques (StatsPageComponent) (fin de partie)
- Page d'accueil (MainPageComponent) (abandon)

### [[Projet3-CyberCity/Coté Client/8. Statistiques\|8. Statistiques]] (StatsPageComponent)

**Fonctionnalité**: Affichage des statistiques après une partie.

**Services utilisés**:
- `StatsService`: Récupération des statistiques de jeu
- `ChatService`: Communication entre joueurs
- `GameViewService`: Nettoyage des états
- `SocketService`: Communication avec le serveur

**Composants**:
- `ChatboxComponent`: Chat entre joueurs
- `GameLogComponent`: Journal des événements (via ChatboxComponent)

**Éléments de la page**:
- Tableau de statistiques des joueurs
- Résumé global de la partie
- Section du joueur gagnant
- Bouton de retour

**Navigation possible vers**:
- Page d'accueil (MainPageComponent)

### [[Projet3-CyberCity/Coté Client/9. Application Principale\|9. Application Principale]] (AppComponent)

**Fonctionnalité**: Composant racine contenant le routeur et les animations de transition.

**Services utilisés**:
- `Router`: Navigation entre les pages

**Composants**:
- `RouterOutlet`: Conteneur pour les routes

**Éléments de la page**:
- Écran de chargement
- Conteneur pour les animations de transition entre pages

# Communication Client-Serveur

La communication avec le serveur est principalement gérée via:

1. **Socket.IO**: Services implémentant la communication en temps réel:
    - `SocketService`: Service principal gérant les connexions
    - `GameSocketHandlerService`: Événements liés au jeu
    - `CombatSocketService`: Gestion des combats
    - `ChatService`: Messagerie
    - `WaitingRoomService`: Gestion de la salle d'attente

2. **HTTP**: Utilisé principalement pour la gestion des jeux:
    - `GameService`: CRUD des jeux via API REST

# Entités Principales

- `Game`: Définition d'un jeu (grille, mode, taille)
- `OnGoingGame`: État d'une partie en cours
- `Player`: Informations sur un joueur
- `Bot`: Extension de Player pour les IA (Joueurs Virtuels défensifs et agressifs)
- `Combat`: État d'un combat entre joueurs
- `Cell`: Cellule de la grille de jeu
- `Item`: Objets que les joueurs peuvent collecter