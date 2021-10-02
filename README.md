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

public class SingletonComp : Singleton<SingletonTest>
{
  public static string[] SceneDependencies {
        get => new string[] { "Menu Scene" };
    }
}

// in any class during runtime...
SingletonComp = SingletonComp.Instance;
```

## Limitations
- Instantiate and Destroy singleton via 'Singleton.Instance' properrty.
- Remove 'Singleton.CreateInstance' by using reflection to find properties at any inheritance level.
- Replace list assembling by comparing System.Runtime.Type.Name with comparing types ( casting System.Runtime.Type to Type ).
- Use reflection to find properties at any inheritance level in 'SceneSingletonListener.ChangedActiveScene'
