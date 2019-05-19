
# Weaver

A a code weaver built for use in [Unity Engine](https://unity3d.com/). 
Based very heavily off of [Fody](https://github.com/Fody/Fody). 
Implemented using [Mono.Cecil](http://www.mono-project.com/docs/tools+libraries/libraries/Mono.Cecil/).

### What is Code Weaving?

Weaving refers to the process of injecting functionality into an existing program. 
This can be done conceptually at a number of levels:

* Source code weaving would inject source code lines before the code is compiled
* IL weaving (for .NET) adds the code as IL instructions in the assembly

A great example of this is the [Unity Project Updater](https://docs.unity3d.com/Manual/APIUpdater.html). 
It uses both versions of code weaving on your project. It uses text replacing for
unsupported code in your source files and IL weaving for compiled dlls.

Weaver for now only uses IL Weaving which runs once every time an assembly is recompiled. 

### Features

* Hooked into Unity callbacks to run automatically. 
* Filter only the assemblies you want to weave. 
* Validation for end user.
* Custom logger.
* Utility functions to write MSIL.


## How To Use

Weaver is run using a single ScriptableObjects you will need to create a new 
instance for your project. Int Unity use the create menu to create a new instance. 

*Right click in the Project Window* `Create/Weaver/Settings`


> **You Only Need One:** Only one instance should exist in your project since 
every operation only needs to happen once. 


#### Weaved Assemblies

When you create a new instance by default Weaver will not edit any assemblies. 
It is up to you to define which assemblies you want to be modified. Click on 
the + icon on the bottom right and a context menu will pop up with all the valid
assemblies you can target. You can also disable the assemblies in this list by
unchecking the check box beside it's name. This will stop them from being edited.

> **Menu Content:** The assemblies in the menu are populated with reflection and
will be found if they they are anywhere ein the Unity Project.

#### Components

Weaver is built around it's components as they are what do the weaving of the
assemblies. Weaver itself is just a provider of information for the components.
They get notified when they should run and on which assemblies they should run against.

To add a new component use the `(+)` button to open the menu and pick any option. 

> **There Can Only Be One:** You can only have one instance of each component as
having more would be useless.

> **Adding New Componet Types:** The component menu uses reflection to find all
types that inherit from `WeaverComponent` and are not abstract and are part of
the EditorAssembly. Any new classes that match thoese rules will populate inside
the menu.

### Logs

To make the process a bit more clear but also not spam to your console Weaver
logs all it's contents to it's own console on the ScriptableObject. Errors are
also logged to the Unity console because that is important.


### Toggling Weaver

If you would like Weaver to not run while in your project you can uncheck
`Is Enabled` in the settings object. You also have the option to define if
Weaver will run depending on the Script Symbols defined in Unity.


You can use any flag like `UNITY_EDITOR` or the inverse flag `!UNITY_EDITOR`. 
Weaver will only run if all flags are active.

## Meta

Handcrafted by Byron Mayne [[twitter](https://twitter.com/byMayne) &bull; [github](https://github.com/ByronMayne)]

Released under the [MIT License](http://www.opensource.org/licenses/mit-license.php).

If you have any feedback or suggestions for Weaver feel free to contact me. 
