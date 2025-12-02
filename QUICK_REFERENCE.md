# 快速参考卡 / Quick Reference Card
# Historical Deep Dive Development

## 📱 项目信息 / Project Info

**项目名称**: 历史深潜 · 当我成为张骞  
**英文名**: Historical Deep Dive: When I Became Zhang Qian  
**仓库**: https://github.com/Genuineh/RolePlay  
**状态**: 📋 Planning Complete → 🚧 Development Ready  

---

## 🗂️ 文档导航 / Documentation Map

```
RolePlay/
├── 📖 README.md              ← 从这里开始！项目概述
├── 📋 TODO.md                ← 12周开发计划
├── 📄 PROJECT_SUMMARY.md     ← 初始化总结
├── 📝 CHANGELOG.md           ← 版本历史
└── 📚 docs/
    ├── 🏗️ ARCHITECTURE.md   ← 系统架构设计
    ├── 🔌 API.md             ← AI集成指南
    ├── 📦 PROJECT_SPEC.md    ← Flutter配置
    ├── 🗺️ ROADMAP.md         ← 时间线规划
    ├── 🤝 CONTRIBUTING.md    ← 贡献指南
    └── 🛠️ SETUP.md           ← 环境配置
```

---

## 🚀 快速开始 / Quick Start

### 1️⃣ 克隆项目
```bash
git clone https://github.com/Genuineh/RolePlay.git
cd RolePlay
```

### 2️⃣ 安装Flutter (如未安装)
```bash
# 查看 docs/SETUP.md 获取详细指南
flutter --version  # 需要 3.24+
flutter doctor
```

### 3️⃣ 初始化Flutter项目 (当前未创建)
```bash
flutter create --platforms=android,ios,windows,macos,web .
flutter pub get
```

### 4️⃣ 运行应用
```bash
flutter devices         # 查看可用设备
flutter run -d chrome   # 在Chrome中运行
flutter run -d macos    # 在macOS中运行
```

---

## 📚 阅读顺序 / Reading Order

### 新手开发者 👶
1. 📖 **README.md** - 了解项目是什么
2. 🛠️ **docs/SETUP.md** - 配置开发环境
3. 📋 **TODO.md** - 看看要做什么（Week 1开始）
4. 🤝 **docs/CONTRIBUTING.md** - 学习代码规范

### 有经验开发者 👨‍💻
1. 📖 **README.md** - 快速了解
2. 🏗️ **docs/ARCHITECTURE.md** - 理解架构
3. 📦 **docs/PROJECT_SPEC.md** - 看看技术栈
4. 🗺️ **docs/ROADMAP.md** - 了解时间线

### 设计师/内容创作者 🎨
1. 📖 **README.md** - 项目概述
2. 📋 **TODO.md** (Week 4, 9-10) - 内容需求
3. 🤝 **docs/CONTRIBUTING.md** (设计贡献部分)

---

## 💻 常用命令 / Common Commands

### Flutter基础
```bash
flutter doctor -v          # 检查环境
flutter devices            # 列出设备
flutter pub get            # 安装依赖
flutter clean              # 清理构建
flutter analyze            # 代码分析
dart format lib/           # 格式化代码
flutter test               # 运行测试
```

### 代码生成
```bash
flutter pub run build_runner build --delete-conflicting-outputs
flutter pub run build_runner watch  # 监听模式
```

### 构建发布
```bash
flutter build apk --release          # Android APK
flutter build appbundle --release    # Android AAB
flutter build ios --release          # iOS
flutter build windows --release      # Windows
flutter build macos --release        # macOS
flutter build web --release          # Web
```

### Git工作流
```bash
git checkout -b feature/my-feature   # 创建分支
git add .                             # 暂存更改
git commit -m "feat: add feature"    # 提交
git push origin feature/my-feature   # 推送
# 然后在GitHub创建Pull Request
```

---

## 🔑 关键概念 / Key Concepts

### 核心功能 / Core Features
- 📦 **.hsp包** - History Story Package，ZIP格式的离线故事包
- 🎮 **Story Player** - 沉浸式故事播放器，支持分支剧情
- 🤖 **AI Generator** - 40秒生成完整历史故事
- 🏆 **Achievement System** - 成就系统，激励探索
- 📤 **Share Poster** - 动态生成分享海报

### 技术架构 / Tech Stack
- **Framework**: Flutter 3.24+ (Dart 3.0+)
- **State**: Riverpod (Provider-based)
- **Routing**: go_router (Declarative)
- **Storage**: Hive (NoSQL local DB)
- **AI**: Claude 3.5 Sonnet / DeepSeek-V3
- **Platforms**: Android, iOS, Windows, macOS, Web

### 数据模型 / Data Models
```
Story
├── id, title, description
├── nodes[]
│   ├── Node (narrative/choice/ending)
│   ├── Question (multiple-choice)
│   └── Encyclopedia (历史知识)
└── metadata

UserProgress
├── currentNodeId
├── visitedNodes[]
├── choicesMade{}
└── achievements[]
```

---

## 🎯 开发路线 / Development Timeline

```
✅ Week 0: Project Planning & Documentation (DONE!)
🔄 Week 1: Foundation (Theme, Hive, Structure)
📝 Week 2: Data Layer (.hsp packages, Storage)
📝 Week 3: Story Player (UI, Logic, Progress)
📝 Week 4: Official Content (10 stories)
📝 Week 5: AI Integration (Generation in 40s)
📝 Week 6: Gamification (Achievements, Share)
📝 Week 7: Polish (UI, Audio, Dark Mode)
🎯 Week 8: MVP Launch (All platforms)
📝 Week 9-10: Content Expansion (20 stories)
🚀 Week 11-12: Go-to-Market (App stores)
```

---

## 🛠️ 故障排除 / Troubleshooting

### Flutter Doctor问题
```bash
# Android licenses
flutter doctor --android-licenses

# iOS tools (macOS only)
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
sudo xcodebuild -runFirstLaunch

# CocoaPods (macOS)
sudo gem install cocoapods
```

### 依赖问题
```bash
flutter clean
flutter pub cache repair
flutter pub get
```

### 构建失败
```bash
# Android
cd android && ./gradlew clean && cd ..
flutter clean && flutter build apk

# iOS
cd ios && pod install && cd ..
flutter clean && flutter build ios
```

---

## 📞 获取帮助 / Get Help

### 项目相关
- 🐛 **Bug报告**: [GitHub Issues](https://github.com/Genuineh/RolePlay/issues)
- 💬 **讨论**: [GitHub Discussions](https://github.com/Genuineh/RolePlay/discussions)
- 📖 **文档**: 查看 `docs/` 目录

### Flutter学习
- 📚 **Flutter文档**: https://docs.flutter.dev/
- 🇨🇳 **Flutter中文网**: https://flutter.cn/
- 🎓 **教程**: https://flutter.dev/learn

### AI集成
- 🤖 **Claude**: https://docs.anthropic.com/
- 🧠 **DeepSeek**: https://platform.deepseek.com/
- 💡 **OpenAI**: https://platform.openai.com/docs

---

## ⚠️ 安全注意事项 / Security

```bash
# ❌ 永远不要这样做
const API_KEY = "sk-xxxxx"  # 不要硬编码密钥！

# ✅ 正确做法
# 1. 使用Serverless函数中转
# 2. 使用环境变量 (.env文件，不提交到Git)
# 3. 使用平台安全存储
```

**已在.gitignore中排除:**
- `.env` 和 `.env.*`
- `secrets.json`
- `api_keys.dart`
- `*.keystore` 和 `*.jks`

---

## 🎨 UI设计资源 / Design Resources

### 色彩方案
- **墨黑**: #2C2C2C
- **宣纸白**: #F5F5DC
- **朱砂红**: #C8102E
- **参考**: http://zhongguose.com/

### 字体
- **标题**: 行楷、隶书
- **正文**: 宋体、仿宋
- **英文**: Noto Serif SC

### 图标
- Material Icons
- 中国传统图案
- 自定义SVG图标

---

## 📊 项目统计 / Project Stats

- **文档**: 11个文件
- **文档总量**: ~103,000 字符
- **计划周期**: 8-12周
- **目标平台**: 5个
- **故事数**: 20个 (MVP: 10个)
- **代码行数**: 待实现 (~20,000+ lines estimated)

---

## 🏆 成功标准 / Success Criteria

### MVP (Week 8)
- ✅ 运行在5个平台
- ✅ 10个完整故事
- ✅ AI生成 < 45秒
- ✅ 应用体积 < 80MB
- ✅ 4.5+ 星评分

### Launch (Week 12)
- 🎯 1,000+ 下载
- 🎯 10+ 正面评价
- 🎯 上架所有主流应用商店

---

## 📝 Commit规范 / Commit Convention

```bash
feat(player): add auto-save feature
fix(storage): resolve Hive race condition
docs(readme): update installation steps
style(ui): improve button styling
refactor(model): simplify Story class
test(player): add unit tests for node navigation
chore(deps): update dependencies
```

---

## 🎯 核心价值观 / Core Values

1. **历史准确性** - 所有内容必须有史可查
2. **教育价值** - 寓教于乐，传播知识
3. **用户体验** - 界面美观，操作流畅
4. **代码质量** - 遵循规范，易于维护
5. **开源精神** - 欢迎贡献，共同成长

---

## 🚀 Let's Build Something Amazing!

```
 _____ _____ _____ _____ _____ _____ _____ _____ _____
|  |  |     |   __|_   _|     | __  |     |     |  _  |
|     |-   -|__   | | | |  |  |    -|-   -|   --|     |
|__|__|_____|_____| |_| |_____|__|__|_____|_____|__|__|

    让历史活起来，让教育更有趣
    Make History Come Alive, Make Education Fun
```

**准备好了吗？开始编码吧！** 🎉

---

**版本**: 1.0  
**更新**: 2025-12-02  
**维护**: Historical Deep Dive Team
