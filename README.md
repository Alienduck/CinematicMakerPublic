# Cinematic Maker - Official Documentation

[![Roblox Plugin](https://img.shields.io/badge/Ro%20blox-Plugin-000000.svg?style=for-the-badge&logo=roblox&colorB=3399ff)](https://create.roblox.com/store/asset/135812529565935/CinematicMaker)
[![Version](https://img.shields.io/badge/Version-1.0.0-green.svg?style=for-the-badge)]()

![Cinematic Maker Logo](https://github.com/Alienduck/CinematicMakerPublic/blob/main/Logo_Plugin_Cinematic.png?raw=true)

> **Note:** This repository does not contain the plugin's source code. It serves as a central hub for documentation, bug reporting, feature requests, and community support.

Welcome to the documentation for the **Cinematic Maker** plugin for Roblox Studio. This document details the structure of plans, shot configuration, the use of effects, and the general workflow within the editor.

## Table of Contents
1. [Cinematic Structure](#cinematic-structure)
    - [The Plan](#the-plan)
    - [The Camera Shot](#the-camera-shot)
2. [Effects and Transitions System](#effects-and-transitions-system)
    - [Effect Transitions](#effect-transitions)
    - [List of Available Effects](#list-of-available-effects)
3. [Using the Editor (Plugin)](#using-the-editor-plugin)
    - [Standard Workflow](#standard-workflow)
    - [Shot Editing Mode](#shot-editing-mode)
    - [Project Management (Import/Export)](#project-management-importexport)

---

<h2 id="cinematic-structure"> Cinematic Structure </h2>

### The Plan

A **Plan** is the main object of a cinematic. It is an ordered sequence composed of multiple [Shots](#the-camera-shot).

The plugin generates a `ModuleScript` for each saved plan. To play a cinematic in-game, you simply need to require this module and call its `:Play()` method.

**Script Usage Example:**
```lua
local Plan = require(Path.To.Plan)

-- 3. Play the plan at the desired moment (e.g., trigger, event)
Plan:Play()
```

### The Camera Shot

A **Shot** represents a static camera viewpoint at a specific moment in your cinematic. Each shot defines the camera's position and how it should move towards that point.

| **Parameter**        | **Type**   | **Description**                                                                                                                       |
| -------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Duration**         | `number`   | The duration (in seconds) the camera will remain static at this shot's position once arrived.                                         |
| **Transition Time**  | `number`   | The duration (in seconds) the camera will take to travel from the _previous_ shot's position to this one.                             |
| **Easing Style**     | `Dropdown` | The interpolation curve style of the movement (e.g., Linear, Quad, Bounce...). Defines the "feel" of the movement.                    |
| **Easing Direction** | `Dropdown` | The direction of the interpolation (In, Out, InOut). Defines whether acceleration/deceleration occurs at the beginning, end, or both. |
## Effects and Transitions System

Each shot can be assigned **a single active visual effect**.

### Effect Transitions

Some effects (like Zoom, Blur, etc.) have an internal transition system. This allows animating the appearance and disappearance of the effect, instead of an abrupt change.

> ℹ️ **Note:** Check the **"Transition"** box in an effect's parameters to reveal these options.

|**Transition Parameter**|**Type**|**Default**|**Description**|
|---|---|---|---|
|**TransitionIn**|`boolean`|`true`|If checked, the effect will animate in at the beginning of the shot (appearance).|
|**TransitionOut**|`boolean`|`true`|If checked, the effect will animate towards its default value at the end of the shot (disappearance).|
|**TransitionStartTime**|`number`|`1.0`|Duration of the animated entry (In).|
|**TransitionEndTime**|`number`|`1.0`|Duration of the animated exit (Out).|
|**EasingStyle**|`Dropdown`|`Sine`|The animation curve style for the effect's transitions.|
|**EasingDirection**|`Dropdown`|`InOut`|The direction of the animation curve.|
### List of Available Effects

Here are the currently supported effects:

#### `NULL`

No active effect on this shot.

#### `ZOOM`

Modifies the camera's Field of View (FOV).

- **FieldOfView** (`number`, default: 70): The target FOV value. Lower than 70 for a close-up (zoom in), higher than 70 for a wide angle (zoom out).
    
- _Supports transitions._
    

#### `BLUR`

Applies a Gaussian blur to the screen.

- **Size** (`number`, default: 10): The intensity of the blur.
    
- _Supports transitions._
    

#### `LETTER_BOXING`

Adds cinematic black bars at the top and bottom of the screen.

- **Ratio** (`number`, default: 0.1): The relative height of the bars (between 0 and 1).
    
- **Color** (`Color3`, default: Black): The color of the bars.
    
- **Transparency** (`number`, default: 0): The transparency of the bars.
    
- _Supports transitions._
    

#### `COLOR_GRADING`

Applies color correction to the image.

- **TintColor** (`Color3`, default: White): Applies a global tint. White is neutral.
    
- **Brightness** (`number`, default: 0): Global brightness, from -1 (complete black) to 1 (complete white).
    
- **Contrast** (`number`, default: 0): Contrast intensity, from -1 to 1.
    
- **Saturation** (`number`, default: 0): Color intensity, from -1 (black and white) to 1 (very vivid colors).
    

#### `CAMERA_SHAKE`

Applies procedural shaking to the camera.

- **Preset** (`Dropdown`, default: 'Bump'): Selects the type of shake from a predefined list (e.g., Bump, Explosion, Earthquake, BadTrip...).
    

---

## Using the Editor (Plugin)

The plugin interface is divided into two main states: creation and modification.

### Standard Workflow (Creation Mode)

In this mode, you capture new viewpoints.

1. Position your Studio camera at the desired location.
    
2. Configure the shot parameters (Duration, Transition, Effect) in the side panel.
    
3. Use the action buttons:
    
    - **📸 Add Shot:** Captures the current camera position and adds the shot with the chosen parameters to the end of the timeline.
        
    - **▶️ Preview:** Plays the complete cinematic in the Studio window to visualize the result.
        

### Shot Editing Mode

To modify an existing shot, **simply click on the shot in the timeline**. The editor switches to modification mode, and the panel fills with that shot's parameters.

The action buttons change:

- **❌ Cancel Edit:** Cancels current changes and returns to standard creation mode.
    
- **📍 Teleport To Shot:** **Very useful.** Instantly repositions your Studio camera to the exact position where this shot was captured. This allows for reframing without having to redo everything.
    
- **💾 Update Shot:** Validates changes and updates the selected shot.
    
    > ⚠️ **Warning:** This button also captures your camera's **current** position. If you only want to modify parameters (duration, effect...) without changing the position, ensure you have clicked **Teleport To Shot** before updating.
    

### Project Management (Import/Export)

This section at the bottom of the plugin allows managing your cinematic files.

- **📥 Install System (Critical):**
    
    - Installs the necessary modules and dependencies into `ReplicatedStorage` for cinematics to work in-game.
        
    - **Must be done at least once per project.** To update the system, delete the existing `Packages` folder and `CinematicController` module in `ReplicatedStorage`, then click this button again.
        
- **💾 Save To Module:**
    
    - Exports the current timeline into a `ModuleScript`. Don't forget to give your plan an explicit name in the text field above before saving.
        
- **📂 Import Selected:**
    
    - Allows reloading an existing cinematic to modify it. Simply select a plan's `ModuleScript` in the explorer, then click this button to load all its shots into the timeline.
