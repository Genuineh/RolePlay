# Flutter Project Specification
# Historical Deep Dive - pubspec.yaml Template

## Complete Dependencies List

```yaml
name: historical_deep_dive
description: A revolutionary historical immersion education platform
publish_to: 'none'
version: 0.1.0+1

environment:
  sdk: '>=3.0.0 <4.0.0'
  flutter: '>=3.24.0'

dependencies:
  flutter:
    sdk: flutter
  
  # State Management
  flutter_riverpod: ^2.5.1
  riverpod_annotation: ^2.3.5
  
  # Routing
  go_router: ^14.0.2
  
  # Local Storage
  hive: ^2.2.3
  hive_flutter: ^1.1.0
  path_provider: ^2.1.2
  shared_preferences: ^2.2.2
  
  # File Operations
  archive: ^3.4.10
  file_picker: ^8.0.0+1
  permission_handler: ^11.3.0
  
  # Network
  http: ^1.2.0
  dio: ^5.4.1
  
  # UI Components
  flutter_markdown: ^0.6.19
  markdown: ^7.2.1
  cached_network_image: ^3.3.1
  flutter_svg: ^2.0.10+1
  flutter_launcher_icons: ^0.13.1
  flutter_native_splash: ^2.3.10
  
  # Audio
  just_audio: ^0.9.36
  audioplayers: ^5.2.1
  
  # Serialization
  json_annotation: ^4.8.1
  freezed_annotation: ^2.4.1
  
  # Sharing
  share_plus: ^7.2.2
  qr_flutter: ^4.1.0
  
  # Utils
  intl: ^0.19.0
  logger: ^2.0.2+1
  uuid: ^4.3.3
  equatable: ^2.0.5
  
  # Fonts & Icons
  google_fonts: ^6.1.0
  flutter_localizations:
    sdk: flutter
  
  # Image Processing
  image: ^4.1.7
  
  # Analytics (Optional)
  # firebase_core: ^2.24.2
  # firebase_analytics: ^10.8.0

dev_dependencies:
  flutter_test:
    sdk: flutter
  
  # Linting
  flutter_lints: ^3.0.1
  
  # Code Generation
  build_runner: ^2.4.8
  json_serializable: ^6.7.1
  freezed: ^2.4.7
  riverpod_generator: ^2.3.11
  
  # Testing
  mockito: ^5.4.4
  integration_test:
    sdk: flutter

flutter:
  uses-material-design: true
  
  # Assets
  assets:
    - assets/images/
    - assets/images/characters/
    - assets/images/scenes/
    - assets/images/periods/
    - assets/images/encyclopedia/
    - assets/fonts/
    - assets/audio/
    - assets/audio/music/
    - assets/audio/sfx/
    - assets/official_stories/
  
  # Fonts
  fonts:
    # Chinese Calligraphy Fonts
    - family: KaiTi
      fonts:
        - asset: assets/fonts/KaiTi.ttf
    - family: LiShu
      fonts:
        - asset: assets/fonts/LiShu.ttf
    - family: FangSong
      fonts:
        - asset: assets/fonts/FangSong.ttf
    
    # Note: Download free Chinese fonts from:
    # - Google Fonts (Noto Serif SC, Ma Shan Zheng, etc.)
    # - Open source repositories
```

## Platform-Specific Configuration

### Android (android/app/build.gradle)

```gradle
android {
    namespace "com.historicaldeep.dive"
    compileSdkVersion 34
    ndkVersion flutter.ndkVersion

    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }

    defaultConfig {
        applicationId "com.historicaldeep.dive"
        minSdkVersion 21
        targetSdkVersion 34
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
        
        // Enable MultiDex
        multiDexEnabled true
    }

    buildTypes {
        release {
            signingConfig signingConfigs.release
            minifyEnabled true
            shrinkResources true
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    implementation 'androidx.multidex:multidex:2.0.1'
}
```

### iOS (ios/Runner/Info.plist)

```xml
<key>CFBundleDisplayName</key>
<string>历史深潜</string>
<key>CFBundleName</key>
<string>Historical Deep Dive</string>

<!-- File Access Permissions -->
<key>NSPhotoLibraryUsageDescription</key>
<string>需要访问相册以保存分享海报</string>
<key>NSPhotoLibraryAddUsageDescription</key>
<string>需要保存图片到相册</string>

<!-- Optional: Document access -->
<key>UIFileSharingEnabled</key>
<true/>
<key>LSSupportsOpeningDocumentsInPlace</key>
<true/>
```

### Windows (windows/runner/main.cpp)

```cpp
// Set window title
window.SetTitle(L"历史深潜 - Historical Deep Dive");

// Set minimum window size
window.SetMinimumSize(Size(800, 600));
```

### macOS (macos/Runner/Info.plist)

```xml
<key>CFBundleName</key>
<string>Historical Deep Dive</string>
<key>CFBundleDisplayName</key>
<string>历史深潜</string>

<!-- Network access -->
<key>com.apple.security.network.client</key>
<true/>

<!-- File access -->
<key>com.apple.security.files.user-selected.read-write</key>
<true/>
```

### Web (web/index.html)

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>历史深潜 - Historical Deep Dive</title>
  <meta name="description" content="沉浸式历史教育平台，让你穿越时空，体验历史伟人的抉择时刻">
  <meta name="keywords" content="历史教育,互动故事,AI生成,文字冒险">
  
  <!-- PWA -->
  <link rel="manifest" href="manifest.json">
  <meta name="theme-color" content="#2C2C2C">
  
  <!-- Icons -->
  <link rel="icon" type="image/png" href="favicon.png">
  <link rel="apple-touch-icon" href="icons/Icon-192.png">
</head>
<body>
  <script src="flutter.js" defer></script>
</body>
</html>
```

## Project Structure to Create

```
historical_deep_dive/
├── android/                  # Android platform code
├── ios/                      # iOS platform code
├── linux/                    # Linux platform code (optional)
├── macos/                    # macOS platform code
├── web/                      # Web platform code
├── windows/                  # Windows platform code
├── lib/                      # Dart source code
│   ├── main.dart            # App entry point
│   ├── app.dart             # App configuration
│   ├── core/                # Core functionality
│   │   ├── theme/
│   │   │   ├── app_theme.dart
│   │   │   ├── colors.dart
│   │   │   └── text_styles.dart
│   │   ├── constants/
│   │   │   └── app_constants.dart
│   │   ├── utils/
│   │   │   ├── logger.dart
│   │   │   └── extensions.dart
│   │   └── router/
│   │       └── app_router.dart
│   ├── data/
│   │   ├── models/
│   │   │   ├── story.dart
│   │   │   ├── story.g.dart
│   │   │   ├── story.freezed.dart
│   │   │   ├── node.dart
│   │   │   ├── node.g.dart
│   │   │   ├── question.dart
│   │   │   ├── question.g.dart
│   │   │   ├── achievement.dart
│   │   │   ├── achievement.g.dart
│   │   │   ├── user_progress.dart
│   │   │   └── user_progress.g.dart
│   │   ├── services/
│   │   │   ├── package_service.dart
│   │   │   ├── storage_service.dart
│   │   │   ├── ai_service.dart
│   │   │   └── share_service.dart
│   │   └── repositories/
│   │       ├── story_repository.dart
│   │       └── user_repository.dart
│   └── presentation/
│       ├── screens/
│       │   ├── home/
│       │   │   ├── home_screen.dart
│       │   │   └── widgets/
│       │   ├── player/
│       │   │   ├── player_screen.dart
│       │   │   └── widgets/
│       │   ├── creator/
│       │   │   ├── creator_screen.dart
│       │   │   └── widgets/
│       │   ├── library/
│       │   │   ├── library_screen.dart
│       │   │   └── widgets/
│       │   └── settings/
│       │       └── settings_screen.dart
│       ├── widgets/
│       │   ├── common/
│       │   │   ├── app_button.dart
│       │   │   ├── app_card.dart
│       │   │   └── loading_indicator.dart
│       │   ├── story_card.dart
│       │   └── choice_button.dart
│       └── providers/
│           ├── story_provider.dart
│           ├── story_provider.g.dart
│           ├── player_provider.dart
│           ├── player_provider.g.dart
│           ├── user_provider.dart
│           └── user_provider.g.dart
├── assets/                   # Asset files
│   ├── images/
│   │   ├── logo.png
│   │   ├── characters/
│   │   ├── scenes/
│   │   ├── periods/
│   │   └── encyclopedia/
│   ├── fonts/
│   │   ├── KaiTi.ttf
│   │   ├── LiShu.ttf
│   │   └── FangSong.ttf
│   ├── audio/
│   │   ├── music/
│   │   │   ├── guqin_01.mp3
│   │   │   └── pipa_01.mp3
│   │   └── sfx/
│   │       ├── button_click.mp3
│   │       └── achievement_unlock.mp3
│   └── official_stories/
│       ├── zhang_qian.hsp
│       ├── su_wu.hsp
│       └── xuanzang.hsp
├── test/                     # Unit tests
│   ├── models/
│   ├── services/
│   └── widgets/
├── integration_test/         # Integration tests
├── docs/                     # Documentation
│   ├── ARCHITECTURE.md
│   ├── API.md
│   ├── ROADMAP.md
│   └── CONTRIBUTING.md
├── .gitignore
├── pubspec.yaml
├── analysis_options.yaml
├── README.md
└── TODO.md
```

## Code Generation Commands

```bash
# Generate code for models (json_serializable, freezed)
flutter pub run build_runner build --delete-conflicting-outputs

# Watch mode for development
flutter pub run build_runner watch --delete-conflicting-outputs

# Generate app icons
flutter pub run flutter_launcher_icons

# Generate splash screen
flutter pub run flutter_native_splash:create
```

## Build Commands

```bash
# Development build
flutter run -d <device>

# Release builds
flutter build apk --release                    # Android APK
flutter build appbundle --release              # Android App Bundle
flutter build ipa --release                    # iOS
flutter build windows --release                # Windows
flutter build macos --release                  # macOS
flutter build web --release                    # Web

# Clean build
flutter clean && flutter pub get && flutter build <platform> --release
```

## Testing Commands

```bash
# Run all tests
flutter test

# Run with coverage
flutter test --coverage

# Run integration tests
flutter drive --driver=test_driver/integration_test.dart \
              --target=integration_test/app_test.dart
```

## Linting & Formatting

```bash
# Analyze code
flutter analyze

# Format code
dart format lib/ test/

# Fix linting issues
dart fix --apply
```

## analysis_options.yaml

```yaml
include: package:flutter_lints/flutter.yaml

linter:
  rules:
    - always_declare_return_types
    - always_put_required_named_parameters_first
    - avoid_print
    - avoid_unnecessary_containers
    - avoid_web_libraries_in_flutter
    - prefer_const_constructors
    - prefer_const_declarations
    - prefer_const_literals_to_create_immutables
    - prefer_final_fields
    - prefer_final_locals
    - require_trailing_commas
    - sort_child_properties_last
    - use_key_in_widget_constructors

analyzer:
  exclude:
    - "**/*.g.dart"
    - "**/*.freezed.dart"
  errors:
    invalid_annotation_target: ignore
```

## Environment Variables (.env - NOT committed)

```env
# AI API Keys (DO NOT COMMIT)
CLAUDE_API_KEY=your_claude_api_key_here
DEEPSEEK_API_KEY=your_deepseek_api_key_here
OPENAI_API_KEY=your_openai_api_key_here

# Serverless Endpoint
AI_GENERATION_ENDPOINT=https://your-worker.workers.dev/api/generate

# Analytics (Optional)
FIREBASE_PROJECT_ID=your_project_id
```

## Secrets Management

**NEVER commit API keys to Git!**

Use:
1. Environment variables (via flutter_dotenv)
2. Serverless functions (recommended)
3. Platform-specific secure storage

---

**Document Version**: 1.0  
**Last Updated**: 2025-12-02  
**Maintained By**: Historical Deep Dive Team
