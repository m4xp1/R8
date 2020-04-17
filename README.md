# R8
Demonstrate **NullPointerException during IR Conversion** bug.

You must run **release** build type. Or run **./gradlew assembleRelease** command.

If you add **-dontoptimize** in proguard rules the problem will disappear and the assembly will complete successfully. But that's not what we want.
