# Cinematic Maker - Documentation Officielle

[![Roblox Plugin](https://img.shields.io/badge/Ro%20blox-Plugin-000000.svg?style=for-the-badge&logo=roblox&colorB=3399ff)](https://create.roblox.com/store/asset/135812529565935/CinematicMaker)
[![Version](https://img.shields.io/badge/Version-1.0.0-green.svg?style=for-the-badge)]()

![Cinematic Maker Logo](https://github.com/Alienduck/CinematicMakerPublic/blob/main/Logo_Plugin_Cinematic.png?raw=true)

> **Note :** Ce dépôt ne contient pas le code source du plugin. Il sert de hub central pour la documentation, le signalement de bugs, les demandes de fonctionnalités et le support communautaire.


Bienvenue dans la documentation du plugin **Cinematic Maker** pour Roblox Studio. Ce document détaille la structure des plans, la configuration des shots, l'utilisation des effets et le flux de travail général dans l'éditeur.

## Table des Matières
1. [Structure d'une Cinématique](#structure-dune-cinématique)
    - [Le Plan (Plan)](#le-plan-plan)
    - [Le Plan de Caméra (Shot)](#le-plan-de-caméra-shot)
2. [Système d'Effets et Transitions](#système-deffets-et-transitions)
    - [Les Transitions d'Effet](#les-transitions-deffet)
    - [Liste des Effets Disponibles](#liste-des-effets-disponibles)
3. [Utilisation de l'Éditeur (Plugin)](#utilisation-de-léditeur-plugin)
    - [Flux de Travail Standard](#flux-de-travail-standard)
    - [Mode Édition de Shot](#mode-édition-de-shot)
    - [Gestion du Projet (Import/Export)](#gestion-du-projet-importexport)

---

<h2 id="structure-dune-cinématique"> Structure d'une cinématique </h2>

### Le Plan (Plan)

Un **Plan** est l'objet principal d'une cinématique. C'est une séquence ordonnée composée de plusieurs [Shots](#le-plan-de-caméra-shot).

Le plugin génère un `ModuleScript` pour chaque plan sauvegardé. Pour jouer une cinématique en jeu, il suffit de requérir ce module et d'appeler sa méthode `:Play()`.

**Exemple d'utilisation en script :**
```lua
local Plan = require(Path.To.Plan)

-- 3. Jouer le plan au moment voulu (ex: déclencheur, événement)
Plan:Play()
```

### Le Plan de Caméra (Shot)

Un **Shot** représente un point de vue de caméra statique à un instant T dans votre cinématique. Chaque shot définit la position de la caméra et comment elle doit se déplacer vers ce point.

|**Paramètre**|**Type**|**Description**|
|---|---|---|
|**Duration**|`number`|La durée (en secondes) pendant laquelle la caméra restera statique à la position de ce shot une fois arrivée.|
|**Transition Time**|`number`|La durée (en secondes) que la caméra prendra pour voyager depuis la position du shot _précédent_ vers celui-ci.|
|**Easing Style**|`Dropdown`|Le style de la courbe d'interpolation du mouvement (ex: Linear, Quad, Bounce...). Définit le "ressenti" du mouvement.|
|**Easing Direction**|`Dropdown`|La direction de l'interpolation (In, Out, InOut). Définit si l'accélération/décélération se produit au début, à la fin, ou les deux.|
## Système d'Effets et Transitions

Chaque shot peut se voir attribuer **un seul effet visuel** actif.

### Les Transitions d'Effet

Certains effets (comme le Zoom, le Blur, etc.) possèdent un système de transition interne. Cela permet d'animer l'apparition et la disparition de l'effet, au lieu d'un changement brutal.

> ℹ️ **Note :** Cochez la case **"Transition"** dans les paramètres d'un effet pour révéler ces options.


|**Paramètre de Transition**|**Type**|**Défaut**|**Description**|
|---|---|---|---|
|**TransitionIn**|`boolean`|`true`|Si coché, l'effet s'animera au début du shot (apparition).|
|**TransitionOut**|`boolean`|`true`|Si coché, l'effet s'animera vers sa valeur par défaut à la fin du shot (disparition).|
|**TransitionStartTime**|`number`|`1.0`|Durée de l'animation d'entrée (In).|
|**TransitionEndTime**|`number`|`1.0`|Durée de l'animation de sortie (Out).|
|**EasingStyle**|`Dropdown`|`Sine`|Le style de la courbe d'animation pour les transitions de l'effet.|
|**EasingDirection**|`Dropdown`|`InOut`|La direction de la courbe d'animation.|

### Liste des Effets Disponibles

Voici les effets actuellement pris en charge :

#### `NULL`

Aucun effet actif sur ce shot.

#### `ZOOM`

Modifie le champ de vision (Field of View) de la caméra.

- **FieldOfView** (`number`, défaut: 70) : La valeur cible du FOV. Inférieur à 70 pour un plan serré (zoom in), supérieur à 70 pour un grand angle (zoom out).
    
- _Supporte les transitions._
    

#### `BLUR`

Applique un flou gaussien à l'écran.

- **Size** (`number`, défaut: 10) : L'intensité du flou.
    
- _Supporte les transitions._
    

#### `LETTER_BOXING`

Ajoute des bandes noires cinématographiques en haut et en bas de l'écran.

- **Ratio** (`number`, défaut: 0.1) : La hauteur relative des bandes (entre 0 et 1).
    
- **Color** (`Color3`, défaut: Noir) : La couleur des bandes.
    
- **Transparency** (`number`, défaut: 0) : La transparence des bandes.
    
- _Supporte les transitions._
    

#### `COLOR_GRADING`

Applique une correction colorimétrique à l'image.

- **TintColor** (`Color3`, défaut: Blanc) : Applique une teinte globale. Le blanc est neutre.
    
- **Brightness** (`number`, défaut: 0) : Luminosité globale, de -1 (noir complet) à 1 (blanc complet).
    
- **Contrast** (`number`, défaut: 0) : Intensité du contraste, de -1 à 1.
    
- **Saturation** (`number`, défaut: 0) : Intensité des couleurs, de -1 (noir et blanc) à 1 (couleurs très vives).
    

#### `CAMERA_SHAKE`

Applique un tremblement procédural à la caméra.

- **Preset** (`Dropdown`, défaut: 'Bump') : Sélectionne le type de tremblement parmi une liste prédéfinie (ex: Bump, Explosion, Earthquake, BadTrip...).
    

---

## Utilisation de l'Éditeur (Plugin)

L'interface du plugin est divisée en deux états principaux : la création et la modification.

### Flux de Travail Standard (Mode Création)

Dans ce mode, vous capturez de nouveaux points de vue.

1. Positionnez votre caméra de studio à l'endroit souhaité.
    
2. Configurez les paramètres du shot (Durée, Transition, Effet) dans le panneau latéral.
    
3. Utilisez les boutons d'action :
    
    - **📸 Add Shot :** Capture la position actuelle de la caméra et ajoute le shot avec les paramètres choisis à la fin de la timeline.
        
    - **▶️ Preview :** Joue la cinématique complète dans la fenêtre de Studio pour visualiser le résultat.
        

### Mode Édition de Shot

Pour modifier un shot existant, **cliquez simplement sur le shot dans la timeline**. L'éditeur passe en mode modification et le panneau se remplit avec les paramètres de ce shot.

Les boutons d'action changent :

- **❌ Cancel Edit :** Annule les modifications en cours et retourne au mode création standard.
    
- **📍 Teleport To Shot :** **Très utile.** Repositionne instantanément votre caméra de studio à la position exacte où ce shot a été capturé. Cela permet de réajuster le cadrage sans tout refaire.
    
- **💾 Update Shot :** Valide les modifications et met à jour le shot sélectionné.
    
    > ⚠️ **Attention :** Ce bouton capture également la position **actuelle** de votre caméra. Si vous ne voulez modifier que les paramètres (durée, effet...) sans changer la position, assurez-vous d'avoir cliqué sur **Teleport To Shot** avant de faire votre mise à jour.
    

### Gestion du Projet (Import/Export)

Cette section en bas du plugin permet de gérer vos fichiers de cinématiques.

- **📥 Install System (Critique) :**
    
    - Installe les modules et dépendances nécessaires dans `ReplicatedStorage` pour que les cinématiques fonctionnent en jeu.
        
    - **À faire au moins une fois par projet.** Pour mettre à jour le système, supprimez le dossier `Packages` et le module `CinematicController` existants dans `ReplicatedStorage`, puis cliquez à nouveau sur ce bouton.
        
- **💾 Save To Module :**
    
    - Exporte la timeline actuelle dans un `ModuleScript`. N'oubliez pas de donner un nom explicite à votre plan dans le champ texte au-dessus avant de sauvegarder.
        
- **📂 Import Selected :**
    
    - Permet de recharger une cinématique existante pour la modifier. Sélectionnez simplement le `ModuleScript` d'un plan dans l'explorateur, puis cliquez sur ce bouton pour charger tous ses shots dans la timeline.
