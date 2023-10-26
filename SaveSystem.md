# Mosaic-Toolset
 System implementations for Mosaic Dreams projects.

## Save System:

### Description:
A simple encrypted SaveSystem, made for Unity. It aims to simplify saving variables without having to save a Data Class with some encryption mechanics.

### Syntax:

#### Namespace:
``` C#
using Mosaic.Toolset.SaveSystem;
```

#### Implementation:

##### Config:
``` C#
SaveSystem.Config(SO);
```
Call this at the start of the game to configure the system using your desired SaveSettings SO.

##### Saving:
``` C#
SaveSystem.Save("KEY", VALUE);
```

This will serialize the value and save it into a binary file.
> Note: `Save()` only writes the key and value into a dictionary. You can use `SaveFile()` to actually write into a file. `SaveFile()` is automatically called when the game closes.

##### Loading:

``` C#
SaveSystem.Load<TYPE>("KEY");
```
This should return a deserialized VALUE according to the KEY.

##### Save/Load File:
``` C#
SaveSystem.SaveFile();
SaveSystem.LoadFile();
```
The `SaveFile()` function will write the dictionary located in memory into a file. Only call it when necessary.
`LoadFile()` will read the corresponding file and write it to the same dictionary. You probably wouldn't need to use this at all.
