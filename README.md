# Cinematic Maker - Roblox Studio Plugin

[![Roblox Plugin](https://img.shields.io/badge/Ro%20blox-Plugin-000000.svg?style=for-the-badge&logo=roblox&colorB=3399ff)](https://create.roblox.com/store/asset/135812529565935/CinematicMaker)
[![Version](https://img.shields.io/badge/Version-1.0.0-green.svg?style=for-the-badge)]()

**[![Cinematic Maker Logo](https://github.com/Alienduck/CinematicMakerPublic/blob/main/cinematicMakerBgLess.png?raw=true)]**

> **Note:** This repository does not contain the plugin's source code. It serves as a central hub for documentation, bug reporting, feature requests, and community support.

## 📖 About

**Cinematic Maker** is a powerful and intuitive Roblox Studio plugin designed to radically simplify the creation of cutscenes, complex camera movements, and dynamic shots in your games.

Whether you are a solo developer looking to add a narrative intro or a studio aiming to create epic trailers, Cinematic Maker allows you to visually compose your camera shots without writing a single line of complex camera code.

### ✨ Key Features

* **📸 Intuitive Visual Editor:** Position your camera in Studio, set the duration and transitions, and capture the "Shot" with a single click.
* **🎞️ Timeline System:** Easily visualize, reorder, delete, or modify your existing shots using the "Edit" mode.
* **🚀 Smooth Transitions:** Precisely control transition time, Easing Style (Quad, Bounce, Elastic...), and Easing Direction (In, Out, InOut) for every movement.
* **✨ Dynamic Effects:** Easily add special effects to your shots (the system is designed to be extensible).
* **▶️ Instant Preview:** Test your cinematic directly within the editor before exporting.
* **💾 Clean Export:** The plugin generates structured, ready-to-use `ModuleScripts`, neatly stored in `ReplicatedStorage`.
* **📦 Automatic Installation:** A single button click installs the necessary modules required for the system to run in your game.

---

## 🛠️ Installation and Setup

### Step 1: Get the plugin
Download and install the plugin from the Roblox Marketplace:
👉 **[LINK TO THE PLUGIN PAGE HERE]** 👈 %% TODO %%

### Step 2: Initialize the system in your game
For cinematics to work in-game, the plugin needs to install its "engine" (the camera controller).

1.  Open Roblox Studio.
2.  Open the **"Plugins"** tab and click on the **Cinematic Maker** icon to open the interface.
3.  In the plugin interface, scroll down to the bottom to the **PROJECT** section.
4.  Click on the **"📥 INSTALL SYSTEM"** button.
    * *This will create a `Packages` folder and a `CinematicController` module in your `ReplicatedStorage`. Do not delete them!*

---

## 🎬 Quick Start Guide: Your First Cinematic

Creating a cinematic takes just a few simple steps:

### 1. Create Shots
1.  Open the plugin widget.
2.  In the Studio 3D view, move your camera to the desired starting position.
3.  In the **EDITOR** section of the plugin, adjust settings like:
    * `Duration (sec)`: Time the camera stays at this position once it arrives.
    * `Transition Time (sec)`: Time taken to travel from the previous position to this one.
    * `Easing Style/Direction`: The style of the movement curve.
4.  Click **"📸 ADD SHOT"**.
5.  Move your camera again to the next position, adjust settings if needed, and click "ADD SHOT" again. Repeat to build your sequence.

### 2. Preview and Edit
* Click **"▶️ PREVIEW"** to see the result.
* To modify a shot, click on it in the **TIMELINE**. Adjust values in the editor, then click **"💾 UPDATE SHOT"**.

### 3. Save
1.  In the **PROJECT** section, give your cinematic a name in the "Plan Name" field (e.g., `GameIntro`).
2.  Click **"💾 SAVE TO MODULE"**.
3.  Your cinematic is saved in `ReplicatedStorage > Cinematics > GameIntro`.

---

## 💻 Using Cinematics in Your Scripts

Once your module is saved, playing it is very simple. You can trigger it from a `LocalScript` (e.g., when a player joins or touches a part).

Here is a typical code example:

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- 1. Wait for the cinematics folder to load
local CinematicsFolder = ReplicatedStorage:WaitForChild("Cinematics")

-- 2. Load your specific cinematic module (replace 'GameIntro' with your plan name)
local MyCinematicPlan = require(CinematicsFolder:WaitForChild("GameIntro"))

-- 3. Play the cinematic!
MyCinematicPlan:Play()

-- Note: The system automatically handles loading the controller.
-- Just ensure you have run "INSTALL SYSTEM" via the plugin at least once.
```

## 🆘 Support and Community

This repository is the official place to get help and discuss the plugin.

How to use Issues?

- 🐛 Report a Bug: If something isn't working as expected, open an Issue with the bug tag. Try to provide clear steps to reproduce the problem and, if possible, screenshots or videos.

- 💡 Suggest a Feature: Have an idea to make the plugin even better? Open an Issue with the enhancement tag. Describe your idea and why it would be useful.

- ❓ Ask a Question: If you are stuck or don't understand how to do something, feel free to open an Issue with the question tag.

👉 [Open an Issue](https://github.com/Alienduck/CinematicMakerPublic/issues)

📄 License

© Lucid Games Studio - All rights reserved. Use of this plugin is subject to the Roblox Marketplace Terms of Use. The code generated by the plugin within your games belongs to you.
