# Mosaic-Toolset
 System implementations for Mosaic Dreams projects.

## Menu System:

### Description:
A simple Menu Management System to control pages and popups. It aims to simplify tween-opening/closing pages or popups.

### Syntax:

#### Namespaces:
``` C#
using Mosaic.Toolset.MenuSystem;
using Mosaic.Toolset.MenuSystem.Debugging;
```
>**Note:** Only add `Debugging` if you want to enable/disable debugging from your code. See more in the [Debugging](#Debugging) section.

#### Config:

``` C#
MenuSystem.ConfigObjects(ObjectDatabase objectdb)
```
Call this at the start of the game to configure the system using your desired ObjectDatabase scriptable object.
>**Note:** This function instantiates the objects needed for the system, i.e. Page Canvas and Popup Canvas.

``` C#
MenuSystem.ConfigPages(PageDatabase pagedb);
```
Call this at the start of the game to configure the system using your desired PageDatabase scriptable object.
>**Note:** This function registers the pages. If a Page has `Preload` enabled, it instantiates and sets up the corresponding prefab here.

``` C#
MenuSystem.ConfigPopups(PopupDatabase popupdb);
```
Call this at the start of the game to configure the system using your desired PopupDatabase scriptable object.
>**Note:** This function registers the pages. If a Popup has `Preload` enabled, it instantiates and sets up the corresponding prefab here.

#### Pages:
>**Note: If you want info on how to set up Pages and page prefabs you can find that [here]().**

##### Open Page:

>**Note:** `OpenPage()` re-sets the current page, meaning it closes the current page first and then opens the desired page. If you want to have multiple pages open, use [OpenPageAdditive()](#Open-Page-Additive) instead.

``` C#
MenuSystem.OpenPage(string name);
MenuSystem.OpenPage(int index);
MenuSystem.OpenPage(PageType type);
```

This function should open the desired page and close the last one.

>`OpenPage(PageType type)` takes an Enum Value from the generated Enum as input.

##### Open Page Additive:
``` C#
MenuSystem.OpenPageAdditive(string name);
MenuSystem.OpenPageAdditive(int index);
MenuSystem.OpenPageAdditive(PageType type);
```

This should open the desired page without closing the last one.

>`OpenPageAdditive(PageType type)` takes an Enum Value from the generated Enum as input.

##### Close Page:
``` C#
MenuSystem.ClosePage(string name);
MenuSystem.ClosePage(int index);
MenuSystem.ClosePage(PageType type);
```

This should close the desired page.

>`ClosePage(PageType type)` takes an Enum Value from the generated Enum as input.

##### Close Current Page:
``` C#
MenuSystem.CloseCurrent();
```

This should close the current page.

#### Popups:

##### Open Popup:
``` C#
MenuSystem.OpenPopup(string name);
MenuSystem.OpenPopup(int index);
MenuSystem.OpenPopup(PopupType type);
```

This should open the desired popup **without closing the last one.**

>`OpenPopup(PopupType type)` takes an Enum Value from the generated Enum as input.

##### Close Popup:
``` C#
MenuSystem.ClosePopup(string name);
MenuSystem.ClosePopup(int index);
MenuSystem.ClosePopup(PopupType type);
```

This should close the desired popup.

>`ClosePopup(PopupType type)` takes an Enum Value from the generated Enum as input.

#### Debugging:
``` C#
MenuSystemLogger.SetDebuggingMode(true);
```
If you want to enable/disable debugging, you should call this function after [Config](#Config) functions. 
>**Note:** Make sure to add `Mosaic.Toolset.MenuSystem.Debugging` to your namespaces as mentioned [here](#Namespaces).

### Scriptable Objects:
This system introduces four scriptable objects which are accessible through `Assets/Create/Mosaic Toolset/Menu System`.
ObjectDatabase, PageDatabase and PopupDatabase are pretty self-explanatory.

#### Page Object:
This scriptable object has four properties which are shown in the inspector:
- Prefab: a prefab gameobject which has a PageParent component.
- Transition Duration: how much it takes to open/close the page.
- Preload: whether the page should be instantiated when `ConfigPages()` is called. It will be cached in memory, and it will not be destroyed.
- Cache: whether the page should stay in memory even after `ClosePage()` or `ClosePopup()` is called.

### Essential Features:
- [x] Open a page and close last.
- [x] Open an additive page.
- [x] Close a page.
- [x] Transition between pages.
- [x] Page Element upgrade to store scale as well as position.
- [x] Warning system to use in Scriptable Objects for debugging.
- [x] Pooling objects.
- [x] Enum Generation.
- [x] Cache functionality.
- [x] A sample menu.
- [x] Refactor.
- [x] Document.

### Added Bonus:
- [ ] Performance Tests.
