# SkyTrack

An Android application built with Kotlin and Jetpack Compose.

## Overview

SkyTrack is an Android app featuring a modern UI built with Material 3 and Jetpack Compose.

## Requirements

- Android Studio (latest version recommended)
- JDK 11 or higher
- Android SDK with API level 24 (minimum) and API level 36 (target)

## Setup

1. Clone the repository
2. Open the project in Android Studio
3. Sync Gradle files
4. Run the app on an emulator or physical device

## Build Configuration

- **Min SDK**: 24
- **Target SDK**: 36
- **Compile SDK**: 36
- **Language**: Kotlin
- **UI Framework**: Jetpack Compose
- **Design System**: Material 3

## Tech Stack

- Kotlin
- Jetpack Compose
- Material 3
- AndroidX libraries

## Project Structure

```
app/
├── src/
│   ├── main/
│   │   ├── java/com/ikiugu/skytrack/
│   │   │   ├── MainActivity.kt
│   │   │   └── ui/
│   │   └── res/
│   └── test/
```

## Building the App

To build a debug APK:
```bash
./gradlew assembleDebug
```

To build a release APK:
```bash
./gradlew assembleRelease
```

## License

[Add your license here]
