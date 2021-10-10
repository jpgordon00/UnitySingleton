# UnitySingleton
Modern Singleton for MonoBehaviouir's in Unity.

## Features
- Automatic MonoBehaviour singleton instantiation and removal.
- Singleton's can be instantiated on specified scenes only.

## How do I use it
- Add 'Singleton' and 'SceneSingletonListener' somewhere Unity reads scripts.
- Add 'SceneSingletonListener'' to the first loaded scene.
- Declare and use a singleton:
```javascript
using UnityEngine;

public class SingletonComp : Singleton<SingletonTest>
{
}

// in any class during runtime...
SingletonComp = SingletonComp.Instance;
```
- Declare and use a singleton for only certain scenes:
```javascript
using UnityEngine;

public class SingletonComp : Singleton<SingletonComp>
{
  public static string[] SceneDependencies {
        get => new string[] { "Menu Scene" };
    }
}

// in any class during runtime...
SingletonComp = SingletonComp.Instance;
```

## Limitations
- Instantiation and Destruction of singletones is not via 'Singleton.Instance' property, it uses the scene listener instead.
> For some Unity applications, in particular those that don't rely on scene transitions, using a scene listener for a listener is entirely unnecesary. If a scene listener is not present, instantion and destruction should be done via 'Singleton.Instance' property. 
- Instantiation via attachment of component does not allow component properties to be edited in the editor.
> Allow instantiation via prefab.
- Remove 'Singleton.CreateInstance' by using reflection to find properties at any inheritance level.
> Currently the properties 'Persistent' and 'SceneDependencies' are only read on the top level of the inherited member.
- Replace list assembling by comparing System.Runtime.Type.Name with comparing types ( casting System.Runtime.Type to Type ).
