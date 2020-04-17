# R8

This branch demonstrate **Shaking error: Missing method in androidx.fragment.app.FragmentManager error**.

This is a standard project created in android studio with the addition four proguard rules.

When trying to launch a release application, we get an runtime exception. If you remove the rule **-addconfigurationdebugging** the problem disappears. 
On my other project where there are no fragments, everything works well.

## Additional question

Why are these rules **-keepattributes InnerClasses** and **-dontwarn** ignored by R8 and warnings are still printed to the console when building the release application?

```
AGPBI: {"kind":"warning","text":"Should have retained InnerClasses attribute of androidx.loader.content.AsyncTaskLoader$LoadTask.","sources":[{"file":"/home/m4xp1/.gradle/caches/transforms-2/files-2.1/370dd66fff47c4dc108a4dd6d2a3e3d2/loader-1.0.0-runtime.jar"}],"tool":"R8"}
AGPBI: {"kind":"warning","text":"Should have retained InnerClasses attribute of androidx.loader.content.AsyncTaskLoader$LoadTask.","sources":[{"file":"/home/m4xp1/.gradle/caches/transforms-2/files-2.1/370dd66fff47c4dc108a4dd6d2a3e3d2/loader-1.0.0-runtime.jar"}],"tool":"R8"}
AGPBI: {"kind":"warning","text":"Should have retained InnerClasses attribute of kotlin.collections.AbstractList$IteratorImpl.","sources":[{"file":"/home/m4xp1/.gradle/caches/transforms-2/files-2.1/b5ba43d2d6a7dd5a77138c2b3a737375/jetified-kotlin-stdlib-1.3.71.jar"}],"tool":"R8"}
AGPBI: {"kind":"warning","text":"Should have retained InnerClasses attribute of kotlinx.coroutines.AwaitAll$DisposeHandlersOnCancel.","sources":[{"file":"/home/m4xp1/.gradle/caches/transforms-2/files-2.1/c5fa06e9c19ea5acda15c401ed4cf1f7/jetified-kotlinx-coroutines-core-1.3.0.jar"}],"tool":"R8"}
AGPBI: {"kind":"warning","text":"Should have retained InnerClasses attribute of kotlinx.coroutines.AwaitAll$DisposeHandlersOnCancel.","sources":[{"file":"/home/m4xp1/.gradle/caches/transforms-2/files-2.1/c5fa06e9c19ea5acda15c401ed4cf1f7/jetified-kotlinx-coroutines-core-1.3.0.jar"}],"tool":"R8"}
AGPBI: {"kind":"warning","text":"Should have retained InnerClasses attribute of kotlinx.coroutines.AwaitAll$AwaitAllNode.","sources":[{"file":"/home/m4xp1/.gradle/caches/transforms-2/files-2.1/c5fa06e9c19ea5acda15c401ed4cf1f7/jetified-kotlinx-coroutines-core-1.3.0.jar"}],"tool":"R8"}
```

If you explicitly tell R8 to keep classes, then the problem disappears. 

```
-keep class androidx.loader.content.AsyncTaskLoader$LoadTask
```

But this should not be, **-keepattributes InnerClasses** and **-dontwarn** rules should hide all problems, but this is not so. Why?
