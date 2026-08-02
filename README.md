# MindGuard AI — Stage 1, Module 1 (Standalone Project)

This is a real, standalone Android Studio project — not a snippet bundle.
Package: `com.mindguard.app` (app shell) / `com.mindguard.collection` (engine).

## How to open

1. Unzip.
2. Open the `MindGuardAI/` folder directly in Android Studio ("Open" →
   select the folder, not a file).
3. Android Studio will regenerate the Gradle wrapper JAR automatically on
   first sync (the binary `gradle-wrapper.jar` isn't included in this zip;
   only `gradle-wrapper.properties` is, which tells Studio which Gradle
   version to fetch — 8.7).
4. Let Gradle sync.

## Expected build result right now

**One and only one compile error is expected:** `DatabaseModule.kt` imports
`com.mindguard.collection.data.local.MindGuardDatabase`, which doesn't exist
yet. That class arrives in Module 2.

Everything else — manifest, `MindGuardApplication` (`@HiltAndroidApp`),
`MainActivity` (`@AndroidEntryPoint`), the placeholder layout/theme/strings,
`CollectionModule.kt`, and all of `util/` — should compile and the app
should install/launch on a device or emulator (API 29+), showing a plain
placeholder screen.

## Project layout

```
MindGuardAI/
├── build.gradle.kts                 root plugin versions
├── settings.gradle.kts
├── gradle.properties
├── gradle/wrapper/gradle-wrapper.properties
└── app/
    ├── build.gradle.kts             dependencies (Room, Hilt, WorkManager, Coroutines...)
    ├── proguard-rules.pro
    └── src/main/
        ├── AndroidManifest.xml      declares PACKAGE_USAGE_STATS, QUERY_ALL_PACKAGES
        │                            (needed by later modules; not used yet)
        ├── java/com/mindguard/
        │   ├── app/
        │   │   ├── MindGuardApplication.kt   @HiltAndroidApp
        │   │   └── MainActivity.kt           @AndroidEntryPoint, placeholder UI
        │   └── collection/
        │       ├── di/
        │       │   ├── CollectionModule.kt   ✅ implemented
        │       │   └── DatabaseModule.kt     ⚠️ needs Module 2's MindGuardDatabase
        │       ├── util/
        │       │   ├── Constants.kt          ✅ implemented
        │       │   ├── Result.kt             ✅ implemented
        │       │   └── DateTimeUtils.kt      ✅ implemented
        │       ├── data/{local/{entity,dao}, repository, datasource}   empty, Module 2+
        │       ├── domain/{model, repository, usecase}                 empty, Module 2+
        │       ├── presentation/dashboard/                             empty, Module 16
        │       └── worker/                                             empty, later modules
        └── res/
            ├── layout/activity_main.xml
            ├── values/{strings,colors,themes}.xml
            ├── drawable/ic_launcher_foreground.xml
            └── mipmap-anydpi-v26/{ic_launcher,ic_launcher_round}.xml
```

## Why permissions are declared but unused right now

`PACKAGE_USAGE_STATS` and `QUERY_ALL_PACKAGES` are declared in the manifest
now so it doesn't need repeated edits later, but nothing in Module 1
actually requests or checks them — that's Module 3 (Permission Flow).

## Next

Module 2: Room Database — all 11 entities (`DeviceInfo`, `InstalledApps`,
`RawUsageEvents`, `UsageStatistics`, `AppSessions`, `AppTransitions`,
`CategoryUsage`, `ScreenEvents`, `HourlyUsage`, `DatasetMetadata`,
`AppLaunchHistory`), their DAOs, repositories, and Room migrations. Once
that lands, `DatabaseModule.kt` resolves and the whole project builds clean.
