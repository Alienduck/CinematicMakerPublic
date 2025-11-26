# Cinematic Maker - Plugin Roblox Studio

[![Roblox Plugin](https://img.shields.io/badge/Ro%20blox-Plugin-000000.svg?style=for-the-badge&logo=roblox&colorB=3399ff)](https://create.roblox.com/store/asset/135812529565935/CinematicMaker)
[![Version](https://img.shields.io/badge/Version-1.0.0-green.svg?style=for-the-badge)]()

**[Logo Cinematic Maker©![Cinematic Maker Logo](https://github.com/Alienduck/CinematicMakerPublic/blob/main/cinematicMakerBgLess.png?raw=true)]**

> **Note :** Ce dépôt ne contient pas le code source du plugin. Il sert de hub central pour la documentation, le signalement de bugs, les demandes de fonctionnalités et le support communautaire.

## 📖 À propos

**Cinematic Maker** est un plugin puissant et intuitif pour Roblox Studio conçu pour simplifier radicalement la création de cinématiques (cutscenes), de mouvements de caméra complexes et de plans dynamiques dans vos jeux.

Que vous soyez un développeur solo souhaitant ajouter une intro narrative ou un studio cherchant à créer des bandes-annonces épiques, Cinematic Maker vous permet de composer vos plans visuellement sans écrire une seule ligne de code complexe pour la gestion de la caméra.

### ✨ Fonctionnalités Principales

* **📸 Éditeur Visuel Intuitif :** Positionnez votre caméra dans Studio, réglez la durée et les transitions, et capturez le plan ("Shot") en un clic.
* **🎞️ Système de Timeline :** Visualisez, réorganisez, supprimez ou modifiez facilement vos plans existants grâce au mode "Édition".
* **🚀 Transitions Fluides :** Contrôlez précisément le temps de transition, le style d'atténuation (Easing Style : Quad, Bounce, Elastic...) et la direction (In, Out, InOut) pour chaque mouvement.
* **✨ Effets Dynamiques :** Ajoutez facilement des effets spéciaux à vos plans (le système est conçu pour être extensible).
* **▶️ Prévisualisation Instantanée :** Testez votre cinématique directement dans l'éditeur avant de l'exporter.
* **💾 Exportation Propre :** Le plugin génère des `ModuleScripts` structurés, prêts à l'emploi, stockés proprement dans `ReplicatedStorage`.
* **📦 Installation Automatique :** Un bouton suffit pour installer les modules nécessaires au fonctionnement du système dans votre jeu.

---

## 🛠️ Installation et Configuration

### Étape 1 : Obtenir le plugin
Téléchargez et installez le plugin depuis le Roblox Marketplace :
👉 **[OBTENIR LE PLUGIN ICI](https://create.roblox.com/store/asset/135812529565935/CinematicMaker)** 👈

### Étape 2 : Initialiser le système dans votre jeu
Pour que les cinématiques fonctionnent en jeu, le plugin doit installer son "moteur" (le contrôleur de caméra).

1.  Ouvrez Roblox Studio.
2.  Ouvrez l'onglet **"Plugins"** et cliquez sur l'icône de **Cinematic Maker** pour ouvrir l'interface.
3.  Dans l'interface du plugin, descendez tout en bas dans la section **PROJECT**.
4.  Cliquez sur le bouton **"📥 INSTALL SYSTEM"**.
    * *Cela va créer un dossier `Packages` et un module `CinematicController` dans votre `ReplicatedStorage`. Ne les supprimez pas !*

---

## 🎬 Guide de Démarrage Rapide : Votre première cinématique

Créer une cinématique se fait en quelques étapes simples :

### 1. Créer les Plans (Shots)
1.  Ouvrez le widget du plugin.
2.  Dans la vue 3D de Studio, déplacez votre caméra à la position de départ souhaitée.
3.  Dans la section **EDITOR** du plugin, réglez :
    * `Duration (sec)` : Le temps que la caméra passera à cette position une fois arrivée.
    * `Transition Time (sec)` : Le temps qu'il faudra pour voyager de la position précédente à celle-ci.
    * `Easing Style/Direction` : Le style du mouvement.
4.  Cliquez sur **"📸 ADD SHOT"**.
5.  Déplacez à nouveau votre caméra vers la prochaine position, ajustez les paramètres si nécessaire, et cliquez à nouveau sur "ADD SHOT". Répétez l'opération pour créer votre séquence.

### 2. Prévisualiser et Éditer
* Cliquez sur **"▶️ PREVIEW"** pour voir le résultat.
* Pour modifier un plan, cliquez dessus dans la **TIMELINE**. Ajustez les valeurs dans l'éditeur, puis cliquez sur **"💾 UPDATE SHOT"**.

### 3. Sauvegarder
1.  Dans la section **PROJECT**, donnez un nom à votre cinématique dans le champ "Plan Name" (ex: `IntroJeu`).
2.  Cliquez sur **"💾 SAVE TO MODULE"**.
3.  Votre cinématique est sauvegardée dans `ReplicatedStorage > Cinematics > IntroJeu`.

---

## 💻 Utiliser les cinématiques dans vos scripts

Une fois votre module sauvegardé, le jouer est très simple. Vous pouvez le déclencher depuis un `LocalScript` (par exemple, quand un joueur rejoint le jeu ou touche une partie).

Voici un exemple de code typique :

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- 1. Attendre que le dossier des cinématiques soit chargé
local CinematicsFolder = ReplicatedStorage:WaitForChild("Cinematics")

-- 2. Charger votre module de cinématique spécifique (remplacez 'IntroJeu' par le nom de votre plan)
local MyCinematicPlan = require(CinematicsFolder:WaitForChild("IntroJeu"))

-- 3. Jouer la cinématique !
MyCinematicPlan:Play()

-- Note : Le système gère automatiquement le chargement du contrôleur.
-- Assurez-vous juste d'avoir fait "INSTALL SYSTEM" via le plugin au moins une fois.
```

---

## 🆘 Support et Communauté

Ce dépôt est l'endroit officiel pour obtenir de l'aide et discuter du plugin.

**Comment utiliser les Issues ?**

- 🐛 Signaler un Bug : Si quelque chose ne fonctionne pas comme prévu, ouvrez une Issue avec le tag bug. Essayez de fournir des étapes claires pour reproduire le problème et, si possible, des captures d'écran ou des vidéos.

- 💡 Suggérer une Fonctionnalité : Vous avez une idée pour rendre le plugin encore meilleur ? Ouvrez une Issue avec le tag enhancement (amélioration). Décrivez votre idée et pourquoi elle serait utile.

- ❓ Poser une Question : Si vous êtes bloqué ou si vous ne comprenez pas comment faire quelque chose, n'hésitez pas à ouvrir une Issue avec le tag question.

👉 [Ouvrir une Issue](https://github.com/Alienduck/CinematicMakerPublic/issues)

---

## 📄 Licence

© Lucid Games Studio - Tous droits réservés. L'utilisation de ce plugin est soumise aux conditions d'utilisation du Roblox Marketplace. Le code généré par le plugin dans vos jeux vous appartient.
