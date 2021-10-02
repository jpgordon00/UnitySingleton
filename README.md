# UnitySingleton
Modern Singleton for MonoBehaviouir's

## How do I use it
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
