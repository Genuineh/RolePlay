# 开发环境设置指南
# Development Environment Setup Guide

## 系统要求 / System Requirements

### 必需 / Required
- **操作系统 / OS**: Windows 10+, macOS 10.14+, or Linux (Ubuntu 18.04+)
- **磁盘空间 / Disk Space**: 至少10GB可用空间
- **内存 / RAM**: 至少8GB (推荐16GB)
- **网络 / Network**: 稳定的互联网连接（用于下载依赖）

---

## 1. 安装 Flutter SDK

### Windows

```powershell
# 方法1: 使用 Git
git clone https://github.com/flutter/flutter.git -b stable
cd flutter
.\flutter\bin\flutter doctor

# 添加到系统路径
# 在"系统属性" > "环境变量"中添加:
# C:\path\to\flutter\bin

# 方法2: 下载ZIP
# 访问 https://docs.flutter.dev/get-started/install/windows
# 下载并解压，然后添加到PATH
```

### macOS

```bash
# 使用 Homebrew (推荐)
brew install flutter

# 或手动安装
cd ~
git clone https://github.com/flutter/flutter.git -b stable
export PATH="$PATH:`pwd`/flutter/bin"

# 添加到 ~/.zshrc 或 ~/.bash_profile
echo 'export PATH="$PATH:$HOME/flutter/bin"' >> ~/.zshrc
source ~/.zshrc
```

### Linux

```bash
cd ~
git clone https://github.com/flutter/flutter.git -b stable
export PATH="$PATH:`pwd`/flutter/bin"

# 添加到 ~/.bashrc
echo 'export PATH="$PATH:$HOME/flutter/bin"' >> ~/.bashrc
source ~/.bashrc
```

### 验证安装 / Verify Installation

```bash
flutter --version
flutter doctor
```

期望输出:
```
Flutter 3.24.0 • channel stable
Dart 3.0.0
```

---

## 2. 安装平台特定工具

### Android (所有平台)

1. **下载 Android Studio**
   - 访问: https://developer.android.com/studio
   - 下载并安装

2. **安装 Android SDK**
   ```bash
   # 在 Android Studio 中:
   # Settings > Appearance & Behavior > System Settings > Android SDK
   # 安装:
   # - Android SDK Platform (API 34)
   # - Android SDK Build-Tools
   # - Android SDK Platform-Tools
   # - Android SDK Command-line Tools
   ```

3. **接受许可**
   ```bash
   flutter doctor --android-licenses
   # 输入 'y' 接受所有许可
   ```

4. **设置模拟器**
   ```bash
   # 在 Android Studio 中:
   # Tools > Device Manager > Create Device
   # 选择 Pixel 6 或任意设备
   ```

### iOS (仅 macOS)

1. **安装 Xcode**
   ```bash
   # 从 Mac App Store 安装 Xcode (15+)
   # 或访问: https://developer.apple.com/xcode/
   
   # 安装命令行工具
   sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
   sudo xcodebuild -runFirstLaunch
   ```

2. **安装 CocoaPods**
   ```bash
   sudo gem install cocoapods
   pod setup
   ```

3. **设置模拟器**
   ```bash
   # 在 Xcode 中:
   # Xcode > Open Developer Tool > Simulator
   # 或使用命令行:
   open -a Simulator
   ```

### Windows Desktop

1. **安装 Visual Studio 2022**
   - 下载: https://visualstudio.microsoft.com/downloads/
   - 安装"使用C++的桌面开发"工作负载

2. **启用 Windows 桌面支持**
   ```powershell
   flutter config --enable-windows-desktop
   ```

### macOS Desktop

1. **启用 macOS 桌面支持**
   ```bash
   flutter config --enable-macos-desktop
   ```

2. **安装依赖**
   ```bash
   # Xcode已安装则自动包含所需工具
   ```

### Linux Desktop

1. **安装依赖**
   ```bash
   sudo apt-get update
   sudo apt-get install \
     clang \
     cmake \
     ninja-build \
     pkg-config \
     libgtk-3-dev \
     liblzma-dev \
     libstdc++-12-dev
   ```

2. **启用 Linux 桌面支持**
   ```bash
   flutter config --enable-linux-desktop
   ```

### Web

```bash
# Web支持默认启用
flutter config --enable-web

# 安装 Chrome (用于调试)
# Windows/Mac: 从官网下载
# Linux:
sudo apt-get install google-chrome-stable
```

---

## 3. 安装 IDE 和插件

### VS Code (推荐)

1. **下载安装**
   - 访问: https://code.visualstudio.com/
   - 下载并安装

2. **安装扩展**
   ```
   必需扩展:
   - Flutter (Dart-Code.flutter)
   - Dart (Dart-Code.dart-code)
   
   推荐扩展:
   - Error Lens (usernamehw.errorlens)
   - GitLens (eamodio.gitlens)
   - Pubspec Assist (jeroen-meijer.pubspec-assist)
   - Flutter Widget Snippets (alexisvt.flutter-snippets)
   - Awesome Flutter Snippets (Nash.awesome-flutter-snippets)
   ```

3. **配置 VS Code**
   ```json
   // settings.json
   {
     "dart.flutterSdkPath": "/path/to/flutter",
     "dart.lineLength": 100,
     "editor.formatOnSave": true,
     "editor.rulers": [80, 100],
     "[dart]": {
       "editor.defaultFormatter": "Dart-Code.dart-code",
       "editor.formatOnSave": true,
       "editor.selectionHighlight": false,
       "editor.suggest.snippetsPreventQuickSuggestions": false,
       "editor.suggestSelection": "first",
       "editor.tabCompletion": "onlySnippets",
       "editor.wordBasedSuggestions": false
     }
   }
   ```

### Android Studio (备选)

1. **安装 Flutter 插件**
   - File > Settings > Plugins
   - 搜索"Flutter"并安装
   - 重启 Android Studio

2. **配置 Flutter SDK**
   - File > Settings > Languages & Frameworks > Flutter
   - 设置 Flutter SDK 路径

---

## 4. 克隆并设置项目

### 克隆仓库

```bash
# 克隆项目
git clone https://github.com/Genuineh/RolePlay.git
cd RolePlay

# 或者使用 SSH
git clone git@github.com:Genuineh/RolePlay.git
cd RolePlay
```

### 安装依赖

```bash
# 获取 Flutter 依赖
flutter pub get

# 如果有代码生成文件，运行:
flutter pub run build_runner build --delete-conflicting-outputs
```

### 运行项目

```bash
# 查看可用设备
flutter devices

# 在特定设备上运行
flutter run -d <device_id>

# 示例:
flutter run -d chrome        # Web
flutter run -d windows       # Windows
flutter run -d macos         # macOS
flutter run -d emulator-5554 # Android模拟器
flutter run -d "iPhone 15"   # iOS模拟器
```

---

## 5. 常见问题解决

### Flutter Doctor 问题

#### Android 许可未接受
```bash
flutter doctor --android-licenses
# 输入 'y' 接受所有
```

#### Xcode 未配置
```bash
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
sudo xcodebuild -runFirstLaunch
```

#### CocoaPods 未安装
```bash
sudo gem install cocoapods
pod setup
```

### 依赖问题

#### Pub get 失败
```bash
# 清除缓存
flutter clean
flutter pub cache repair
flutter pub get
```

#### 包冲突
```bash
# 删除 pubspec.lock 并重新获取
rm pubspec.lock
flutter pub get
```

### 构建问题

#### Android 构建失败
```bash
# 清理构建
cd android
./gradlew clean
cd ..
flutter clean
flutter pub get
flutter build apk
```

#### iOS 构建失败
```bash
# 清理 Pods
cd ios
rm -rf Pods Podfile.lock
pod install
cd ..
flutter clean
flutter build ios
```

#### Windows 构建失败
```bash
# 确保 Visual Studio 已安装
# 重新生成项目文件
flutter create --platforms=windows .
flutter build windows
```

### 运行时问题

#### 热重载不工作
```bash
# 在 flutter run 时按:
# r - 热重载 (hot reload)
# R - 热重启 (hot restart)
# q - 退出

# 或重新运行
flutter run
```

#### 设备未检测到
```bash
# Android:
adb devices
adb kill-server
adb start-server

# iOS:
xcrun simctl list
open -a Simulator

# 重新检测
flutter devices
```

---

## 6. 开发工具推荐

### 调试工具

```bash
# Flutter DevTools
flutter pub global activate devtools
flutter pub global run devtools

# 或在运行应用时:
flutter run
# 然后在终端中点击显示的 DevTools URL
```

### 代码质量工具

```bash
# 静态分析
flutter analyze

# 格式化代码
dart format lib/ test/

# 修复可自动修复的问题
dart fix --apply
```

### 性能分析

```bash
# 性能追踪
flutter run --profile

# 在 DevTools 中查看性能
# Timeline, Memory, CPU Profiler
```

---

## 7. 项目特定设置

### 字体文件

```bash
# 下载中文字体（如果尚未包含）
# 推荐免费商用字体:
# - 思源宋体 (Noto Serif SC)
# - 思源黑体 (Noto Sans SC)
# - 方正书宋
# - 站酷快乐体

# 下载后放置在:
assets/fonts/
```

### 环境变量 (可选)

```bash
# 创建 .env 文件 (不要提交到 Git)
touch .env

# 添加 API 密钥 (如果需要)
# CLAUDE_API_KEY=your_key_here
# DEEPSEEK_API_KEY=your_key_here

# 安装 flutter_dotenv
flutter pub add flutter_dotenv
```

### 资源文件

```bash
# 官方故事包将在 Week 4 添加到:
assets/official_stories/

# 图片资源:
assets/images/

# 音频资源:
assets/audio/
```

---

## 8. Git 工作流

### 配置 Git

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### 分支策略

```bash
# 创建功能分支
git checkout -b feature/your-feature-name

# 提交更改
git add .
git commit -m "feat: add your feature"

# 推送到 GitHub
git push origin feature/your-feature-name

# 创建 Pull Request (在 GitHub 网页上)
```

---

## 9. 验证设置

运行以下命令确保一切正常:

```bash
# 1. 检查 Flutter
flutter doctor -v

# 2. 检查设备
flutter devices

# 3. 创建测试项目
flutter create test_app
cd test_app
flutter run

# 4. 如果成功，删除测试项目
cd ..
rm -rf test_app
```

期望的 `flutter doctor` 输出:
```
[✓] Flutter (Channel stable, 3.24.0, on macOS 14.0)
[✓] Android toolchain - develop for Android devices
[✓] Xcode - develop for iOS and macOS
[✓] Chrome - develop for the web
[✓] Android Studio (version 2023.1)
[✓] VS Code (version 1.85)
[✓] Connected device (4 available)
[✓] Network resources

• No issues found!
```

---

## 10. 下一步

设置完成后:

1. ✅ 阅读 [README.md](../README.md) 了解项目概况
2. ✅ 查看 [TODO.md](../TODO.md) 了解开发计划
3. ✅ 阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 了解如何贡献
4. ✅ 查看 [ARCHITECTURE.md](ARCHITECTURE.md) 了解系统架构
5. 🚀 开始编码!

---

## 获取帮助

遇到问题？

- 📖 Flutter文档: https://docs.flutter.dev/
- 💬 Flutter中文社区: https://flutter.cn/
- 🐛 项目Issues: https://github.com/Genuineh/RolePlay/issues
- 💡 GitHub Discussions: https://github.com/Genuineh/RolePlay/discussions

---

**文档版本**: 1.0  
**最后更新**: 2025-12-02  
**维护者**: Historical Deep Dive Team

祝开发顺利！🎉
