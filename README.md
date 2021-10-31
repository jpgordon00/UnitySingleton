# UnitySingleton
Modern Singleton for MonoBehaviouir's in Unity.

## Features
- Automatic MonoBehaviour singleton instantiation and removal.
> Attach one component to any object in the scene for automatic instantiation of Singletons. Alternatively, any call to the 'Instance' property where a scene listener is not present in the scene will instantiate the object.
- Instantiation via prefab can be done by specifying the 'ResourceName' property, otherwise any top-level inherited member of 'Singleton' will by attached to a new game object.
- Singleton's can be instantiated on only specified scenes.

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
- Use a singleton that is also a prefab in the 'Resources' folder.
```javascript
using UnityEngine;

public class SingletonComp : Singleton<SingletonComp>
{

  // in '...Resources/Singleton'
  public static string ResourceName {
        get => "Singleton";
    }
}

// in any class during runtime...
SingletonComp = SingletonComp.Instance;
```

## Limitations
- ~~Instantiation and Destruction of singletones is not via 'Singleton.Instance' property, it uses the scene listener instead.~~
> For some Unity applications, in particular those that don't rely on scene transitions, using a scene listener for a listener is entirely unnecesary. If a scene listener is not present, instantion and destruction should be done via 'Singleton.Instance' property. 
- ~~Instantiation via attachment of component does not allow component properties to be edited in the editor.~~
> ~~Allow instantiation via prefab in addition to the current solution that instatiates in code.~~
- Remove 'Singleton.CreateInstance' by using reflection to find properties at any inheritance level.
> Currently the properties 'Persistent', 'SceneDependencies' and 'ResourceName', and all other properties are only read on the top level of the inherited member. Alternatively you could recursively or iteratively search through children until Instance types are found.
- Replace list assembling by comparing System.Runtime.Type.Name with comparing types ( casting System.Runtime.Type to Type ). 
