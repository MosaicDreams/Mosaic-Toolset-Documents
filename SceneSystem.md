# Mosaic-Toolset
 System implementations for Mosaic Dreams projects.

---
## Table Of Contents 
<!-- toc -->

- [Scene System](#scene-system)
    - [Description](#description)
    - [Namespace](#namespace)
- [Scriptable Objects](#scriptable-objects)
    - [Scenes](#scene-scriptable-object)
    - [Transitions](#transition-scriptable-object)
- [Databases](#databases-also-scriptable-object)
    - [Objects](#object-database)
    - [Scenes](#scene-database)
- [Configurations](#config)
    - [Objects](#objects)
    - [System](#system)
- [Methods](#methods)
    - [Open](#open-scene)
    - [Open Additive](#open-scene-additive)
    - [Close](#close-scene)
    - [Close Current](#close-current-scene)
- [Features](#features)

<!-- tocstop -->

---

## [Scene System](#table-of-context)

### Description :
A simple Scene Management System to control scene flow in Unity. It aims to simplify moving between scenes, and opening/closing them.

### Namespace :
``` C#
using Mosaic.Toolset.SceneSystem; // For using system
using Mosaic.Toolset.SceneSystem.Debugging; // For enabling debugging
```

---
## [Scriptable objects](#table-of-context)

The base system works on scriptable objects And there are two main scriptable objects that you want to use first.

1. ### Scene Scriptable object :
this is a wrapper to three things :

**1. Name :** the name of your scene, this is important because when you want to call this scriptable object you're gonna call it by this name **NOT the scene name**.

**2. Scene Refrence :** we added a feature that stores scenes in the code and you can drag your desired scene in the scriptable object through inspector. then hit the **green plus** to actually add the scene.

**3. Transition :** you will create the transition scriptable object, set the datas and give it to the scene scriptable object. You may ask what is the **Trasition Scriptable Object**, *well...*

2. ### Transition Scriptable object :
This is where you store your transition effect but it requires four things :

**1. Name :** this is the name of your effect. Like `fade`.

**2. Prefab :** this is a little tricky but you make your effect with Tween Actions. We will document on how using this feature.

**3. Transition Duration :** you will deside on how many seconds your transition should last.

**4. Preload :** this is a boolean

---
## [Databases (also scriptable object)](#table-of-context)

After you add your Scenes and your Transitions you create your own database and store your scenes ant their transitions.
then you use them in your code using the SceneSystem.

**there are two Databases :**

1. ### Object Database :

Object database scriptable only requires canvas prefab as your default canvas. we used this to create default canvas and load transitions on it.
> **NOTE** : you can find it in **Mosaic Toolset/Scene System/Object Database**

2. ### Scene Database :

Scene database gets two things : **1)** Scenes that you want to use () and **2)** Transitions you want to use in your game ().
 We wanted to do this to organize scenes and the transitions you want to use later in your code.
> **NOTE** : you can find it in **Mosaic Toolset/Scene System/Scene Database** 

---
## [Config](#table-of-context)

After you set your databases, you need to configure them. To do that you need to create a script and add it to an empty GameObject. in the script you need to configure **two** things :

1. ### Objects :

```C#
SceneSystem.ConfigObjects(ObjectDatabase objects);
```
Call this method at the start of the game that the SceneSystem configure your desired ObjectDatabase scriptable object.

> **NOTE** : *objects* is a scriptable object that holds a default prefab of *canvas*. you can find it in **Mosaic Toolset/Scene System/Object Database**

2. ### System :

```C#
SceneSystem.ConfigSceneSystem(SceneDatabase scenes);
```
Call this method at the start of your game that the SceneSystem configure scenes and scene transitions that you used in the SceneDatabase.

> **NOTE** : **scenes** is a scriptable object that holds scene and transition configurations. you can find it in **Mosaic Toolset/Scene System/Scene Database** 
---
## [Methods](#table-of-context) 
So after configuring databases you are ready to use the system. 
There are ***currently*** four methods to use in the scene system.

> **NOTE** : methods get *"Scene name"* or *Scene index*. *Scene name* is the name you chosed in the **Scene** scriptable object (NOT database) and the *Scene index* is the order in the Scene Database

1. ### Open Scene :

``` C#
SceneSystem.Open(string name);
SceneSystem.Open(int index);
```

This method is for openning scenes but closing all the loaded scenes, causing the current scene the only loaded scene.

2. ### Open Scene Additive :

```C#
SceneSystem.OpenAdditive(string name);
SceneSystem.OpenAdditive(int index);
```

This method is for openning scenes and keeping the last loaded scene you used.
> **NOTE** : beware of the consequences of openning scenes additively.

3. ### Close Scene : 
```C#
SceneSystem.Close(string name);
SceneSystem.Close(int index);
```

This method is for closing the desired loaded scene. if there are any scenes that opened additively, it will go on that scene.
> **NOTE** : be careful if you want to close the only scene that is opened.

4. ### Close Current Scene :
```C#
SceneSystem.CloseActiveScene();
```

If you want to close your current scene and don't want to write the scene name everytime, use this method. It will find your current active scene and close it, but be careful if you have only one open scene.

---
## [Features](#table-of-context) 
- [x] Open a scene and close last.
- [x] Open scene additive (don't close last).
- [x] Closing a scene
- [x] Closing current scene
- [x] Transition between scenes.
- [x] Multiple transition pack.
---
## ToDo 

- [ ] Preloading scenes
- [ ] Openning preloaded scenes
- [ ] Fixing List of Scenes
---
#### Added Bonus :
- [ ] Create an Enum of SceneDB to use in OpenScene().
- [ ] Optimization (Object Pooling, ...).


