---
{"dg-publish":true,"permalink":"/projet3-cyber-city/documentation-cote-serveur/"}
---

# Documentation Coté Serveur

Le serveur de jeu est construit selon une architecture orientée services, utilisant Node.js avec Type Script. Il s'appuie principalement sur Socket.IO pour les communications en temps réel et MongoDB pour la persistance des données. L'architecture est conçue pour gérer plusieurs parties simultanément, avec une logique complexe pour les mécanismes de jeu, le combat, et les interactions entre joueurs.

Le point d'entrée principal est le fichier `server.ts` qui initialise le serveur HTTP et configure Socket.IO. L'application est structurée selon le principe d'injection de dépendances , permettant de maintenir un couplage faible entre les différentes parties du système.

## Organisation fonctionnelles des services

Le côté serveur peut être divisé en plusieurs catégories fonctionnelles afin d’en faciliter la compréhension. Les sections suivantes présentent un résumé de chaque catégorie. Pour consulter la documentation détaillée, **cliquez sur le titre correspondant** pour y accéder directement.

### [[Projet3-CyberCity/Coté Serveur/1. Infrastructure et Configuration\|1. Infrastructure et Configuration]]

- **Server** (`server.ts`) - Point d'entrée qui configure le serveur HTTP et Socket.IO
- **Application** (`app.ts`) - Configuration Express et middlewares HTTP
- **Database** (`database.service.ts`) - Interface avec la base de données MongoDB

### [[Projet3-CyberCity/Coté Serveur/2. Gestion des WebSockets\|2. Gestion des WebSockets]]

- **SocketService** (`socket.service.ts`) - Service central qui gère les connexions Socket.IO
- **GameSocketHandlerService** (`game-socket-handler.service.ts`) - Gère les événements socket liés au jeu principal
- **WaitingSocketService** (`waiting-room-socket.service.ts`) - Gère les événements socket de la salle d'attente
- **JoinGameService** (`join-game.service.ts`) - Gère la logique de rejoindre une partie

### [[Projet3-CyberCity/Coté Serveur/3. Gestion des Parties\|3. Gestion des Parties]]

- **OnGoingGameService** (`on-going-game.service.ts`) - Service principal qui gère l'état des parties en cours
- **GameStateService** (`game-state.service.ts`) - Gère les transitions d'états du jeu
- **GameTimerService** (`game-timer.service.ts`) - Gestion des timers de jeu
- **TimerSocketService** (`timer-socket.service.ts`) - Événements socket liés aux timers

### [[Projet3-CyberCity/Coté Serveur/4. Système de Combat\|4. Système de Combat]]

- **CombatService** (`combat.service.ts`) - Logique principale du système de combat
- **CombatSocketService** (`combat-socket.service.ts`) - Gestion des événements socket liés au combat
- **CombatEndingService** (`combat-ending.service.ts`) - Gère la fin des combats
- **CombatHelperService** (`combat-helper.service.ts`) - Utilitaires pour le combat

### [[Projet3-CyberCity/Coté Serveur/5. Gestion des Items\|5. Gestion des Items]]

- **GameItemService** (`game-item.service.ts`) - Gestion des items dans le jeu
- **GameItemHandlerService** (`game-item-handler.service.ts`) - Traitement des événements liés aux items
- **ItemHandlerService** (`item-handler.service.ts`) - Utilitaires pour la manipulation des items

### [[Projet3-CyberCity/Coté Serveur/6. Gestion des Joueurs\|6. Gestion des Joueurs]]

- **GamePlayerService** (`game-player.service.ts`) - Service de gestion des joueurs
- **OnGoingGameItemHandling** (`on-going-game-item-handling.ts`) - Interaction des joueurs avec les items
- **OnGoingGamePathFinding** (`on-going-game-path-finding.ts`) - Logique de déplacement des joueurs

### [[Projet3-CyberCity/Coté Serveur/7. Contrôle de Jeu et Vérification\|7. Contrôle de Jeu et Vérification]]

- **GameVerifierService** (`game-verification.service.ts`) - Validation des parties
- **AutoTileService** (`auto-tile.service.ts`) - Gestion automatique des tuiles

### [[Projet3-CyberCity/Coté Serveur/8. Système du Chatbox\|8. Système du Chatbox]]

- **ChatService** (`chat.service.ts`) - Gestion des messages de chat

### [[Projet3-CyberCity/Coté Serveur/9. Classes du Jeu (Coté Serveur)\|9. Classes du Jeu (Coté Serveur)]]

- **OnGoingGame** (`on-going-game.ts`) - Représente une partie en cours
- **Player** (`player.ts`) - Représente un joueur
- **Bot** (`bot.ts`, `aggressive-bot.ts`, `defensive-bot.ts`) - Les Joueurs Virtuels
- **Game** (`game.ts`) - Structure d'un jeu (plateau, règles)
- **Grid** (`grid.ts`) - Représente la grille de jeu
- **Cell** (`cell.ts`) - Représente une cellule de la grille
- **Item** (`item.ts`) - Représente un objet dans le jeu
- **Timer** (`timer.ts`) - Représente le timer utilisé lors des parties

## Flux d'information

L'architecture du serveur suit un modèle événementiel où:

1. Les clients se connectent via WebSockets (Socket.IO)
2. Les événements socket sont routés vers les services appropriés
3. Ces services mettent à jour l'état du jeu (instances de `OnGoingGame`)
4. Les modifications sont transmises à tous les clients concernés

Le serveur maintient l'état de toutes les parties en cours en mémoire, avec des références entre les différentes entités (joueurs, objets, grille de jeu). La persistance des données est assurée par MongoDB pour les configurations de jeux (plateaux personnalisés).