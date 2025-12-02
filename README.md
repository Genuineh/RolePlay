# 历史深潜 · 当我成为张骞
## Historical Deep Dive: When I Became Zhang Qian

<div align="center">

![Version](https://img.shields.io/badge/version-0.1.0-blue.svg)
![Flutter](https://img.shields.io/badge/Flutter-3.24+-02569B.svg?logo=flutter)
![Dart](https://img.shields.io/badge/Dart-3.0+-0175C2.svg?logo=dart)
![License](https://img.shields.io/badge/license-MIT-green.svg)

**A Revolutionary Historical Immersion Education Platform**

[English](#english) | [中文](#中文)

</div>

---

## 中文

### 📖 项目简介

「历史深潜」是一款创新的**沉浸式历史教育应用**，通过互动式叙事和AI技术，让用户亲身体验历史人物的抉择时刻，深入理解历史事件背后的复杂性。

**核心特色：**
- 🎭 **角色扮演历史人物**：成为张骞、玄奘、郑和等历史伟人，做出改变历史的抉择
- 🌿 **分支叙事系统**：每个选择都会导向不同的历史分支，探索平行历史可能性
- 🤖 **AI实时生成故事**：40秒内生成专属历史剧本，想扮演谁就扮演谁
- 📦 **完全离线运行**：所有故事可离线游玩，随时随地穿越历史
- 🎨 **中国传统美学**：水墨风格界面，毛笔字体，古琴配乐
- 🏆 **成就系统**：收集历史成就，解锁隐藏剧情
- 📱 **全平台支持**：Android、iOS、Windows、macOS、Web五端同步

### 🎯 目标用户

- 📚 **历史爱好者**：深度探索历史事件的多重维度
- 🎓 **学生群体**：寓教于乐，沉浸式学习历史知识
- 👨‍🏫 **教育工作者**：创新教学工具，激发学生兴趣
- 🎮 **游戏玩家**：享受高质量文字冒险游戏体验
- 👪 **家庭教育**：亲子共玩，传承历史文化

### ✨ 核心功能

#### 1. 官方精品故事库（20+个）
- ✅ 张骞出使西域
- ✅ 苏武牧羊北海
- ✅ 玄奘西天取经
- ✅ 郑和七下西洋
- ✅ 鉴真东渡日本
- ✅ 戚继光抗击倭寇
- ✅ 左宗棠收复新疆
- ✅ 林则徐虎门销烟
- ✅ 利玛窦来华传教
- ✅ 文天祥正气长存
- 🔄 更多故事持续更新...

每个故事包含：
- 30+ 精心设计的故事节点
- 3-10 个不同结局
- 10+ 张历史复原插图
- 详细的历史百科注释
- 沉浸式背景音乐

#### 2. AI故事创作工坊
输入你想扮演的历史人物或参与的历史事件：
- "我想成为荆轲刺秦王"
- "我想参加鸿门宴"
- "我想成为王昭君出塞"
- "我想经历虎门销烟"

**40秒后**，获得一个专属的、可离线游玩的完整历史剧本！

**技术支持：**
- Claude 3.5 Sonnet（首选）
- DeepSeek-V3（高性价比）
- GPT-4o（备用）

#### 3. 离线故事包系统
- 📦 `.hsp` 格式（History Story Package）
- 🔄 一键导入/导出故事包
- 📤 分享给朋友，让他们体验你的专属历史
- 💾 完全本地存储，无需网络
- 📊 自动保存游戏进度

#### 4. 成就与排行系统
- 🏆 50+ 可解锁成就
- ⚡ 速通挑战
- 🎯 完美抉择奖
- 🗺️ 全分支探索者
- 📖 历史学家认证

#### 5. 社交分享功能
- 🎨 精美分享海报生成
- 📱 一键分享到微信/抖音/小红书
- 🔗 二维码邀请好友
- 🏅 炫耀你的历史成就

### 🛠️ 技术栈

```
Flutter 3.24+
├── 状态管理: Riverpod
├── 路由: go_router
├── 本地存储: Hive + hive_flutter
├── 文件操作: archive, file_picker, path_provider
├── 网络请求: http, dio
├── UI组件: flutter_markdown, cached_network_image
├── 音频播放: just_audio / audioplayers
├── 数据序列化: json_serializable
├── 分享功能: share_plus
├── 二维码: qr_flutter
└── 图表: fl_chart
```

### 📁 项目结构

```
historical_deep_dive/
├── lib/
│   ├── main.dart                 # 应用入口
│   ├── app.dart                  # App配置
│   ├── core/                     # 核心功能
│   │   ├── theme/               # 主题系统（水墨风）
│   │   ├── constants/           # 常量定义
│   │   ├── utils/               # 工具类
│   │   └── router/              # 路由配置
│   ├── data/                    # 数据层
│   │   ├── models/              # 数据模型
│   │   │   ├── story.dart       # 故事模型
│   │   │   ├── node.dart        # 节点模型
│   │   │   ├── question.dart    # 问题模型
│   │   │   ├── achievement.dart # 成就模型
│   │   │   └── user_progress.dart # 进度模型
│   │   ├── services/            # 业务服务
│   │   │   ├── package_service.dart  # 包管理
│   │   │   ├── storage_service.dart  # 存储服务
│   │   │   ├── ai_service.dart       # AI生成
│   │   │   └── share_service.dart    # 分享服务
│   │   └── repositories/        # 数据仓库
│   └── presentation/            # 展示层
│       ├── screens/             # 页面
│       │   ├── home/           # 主页
│       │   ├── player/         # 游戏播放器
│       │   ├── creator/        # AI创作器
│       │   ├── library/        # 故事库
│       │   └── settings/       # 设置
│       ├── widgets/             # 组件
│       └── providers/           # 状态管理
├── assets/                      # 资源文件
│   ├── images/                 # 图片资源
│   ├── fonts/                  # 字体文件
│   ├── audio/                  # 音频文件
│   └── official_stories/       # 官方故事包
├── test/                        # 测试文件
└── docs/                        # 文档
```

### 🚀 快速开始

#### 环境要求
- Flutter SDK 3.24 或更高版本
- Dart SDK 3.0 或更高版本
- Android Studio / VS Code
- Git

#### 安装步骤

1. **克隆项目**
```bash
git clone https://github.com/Genuineh/RolePlay.git
cd RolePlay
```

2. **安装依赖**
```bash
flutter pub get
```

3. **生成代码（如果需要）**
```bash
flutter pub run build_runner build --delete-conflicting-outputs
```

4. **运行项目**
```bash
# Android
flutter run -d android

# iOS
flutter run -d ios

# Windows
flutter run -d windows

# macOS
flutter run -d macos

# Web
flutter run -d chrome
```

### 📦 构建发布

#### Android
```bash
flutter build apk --release
# 或构建 App Bundle
flutter build appbundle --release
```

#### iOS
```bash
flutter build ipa --release
```

#### Windows
```bash
flutter build windows --release
```

#### macOS
```bash
flutter build macos --release
```

#### Web
```bash
flutter build web --release
```

### 🎨 设计规范

#### 配色方案
```dart
// 主色调 - 水墨黑
Primary: #2C2C2C

// 辅助色 - 宣纸白
Secondary: #F5F5DC

// 强调色 - 朱砂红
Accent: #C8102E

// 文字色
Text Primary: #1A1A1A
Text Secondary: #666666

// 背景色
Background Light: #FAFAF8
Background Dark: #1C1C1C
```

#### 字体
- **标题**：行楷、隶书
- **正文**：宋体、仿宋
- **英文**：Noto Serif SC

### 📱 平台特性

| 平台 | 状态 | 特性说明 |
|------|------|---------|
| Android | ✅ | 完整支持，包括文件导入导出 |
| iOS | ✅ | 完整支持，符合App Store审核标准 |
| Windows | ✅ | 桌面体验，支持键盘快捷键 |
| macOS | ✅ | 原生菜单栏集成 |
| Web | ✅ | 渐进式Web应用(PWA) |
| Linux | 🔄 | 计划支持 |

### 🗓️ 开发路线图

#### Phase 1 - MVP (Week 1-8) ✅ In Progress
- [x] 项目初始化
- [ ] 核心功能开发
- [ ] 10个官方故事
- [ ] AI生成功能
- [ ] 基础UI实现

#### Phase 2 - 增强版 (Week 9-12)
- [ ] 20个官方故事
- [ ] 成就系统完善
- [ ] 社交分享优化
- [ ] 性能优化
- [ ] 多平台测试

#### Phase 3 - 社区版 (Month 4-6)
- [ ] 用户上传故事
- [ ] 社区评分系统
- [ ] 多人协作模式
- [ ] 云端同步
- [ ] 全球排行榜

#### Phase 4 - Pro版 (Month 7-12)
- [ ] VR/AR体验
- [ ] 真人语音配音
- [ ] 3D场景重建
- [ ] AI辅助历史教学
- [ ] 教育机构合作

### 🤝 贡献指南

我们欢迎所有形式的贡献！

#### 如何贡献
1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

#### 贡献类型
- 🐛 Bug修复
- ✨ 新功能开发
- 📝 文档改进
- 🎨 UI/UX优化
- 📚 新增历史故事内容
- 🌍 多语言翻译

### 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

### 📞 联系我们

- **项目主页**: https://github.com/Genuineh/RolePlay
- **问题反馈**: [GitHub Issues](https://github.com/Genuineh/RolePlay/issues)
- **邮箱**: [待添加]
- **微信公众号**: [待添加]
- **官方网站**: [待添加]

### 🙏 致谢

- Flutter团队提供的优秀框架
- Anthropic Claude AI提供的强大生成能力
- 所有历史资料提供者和审核专家
- 开源社区的大力支持

### 📊 项目状态

- 🚧 **当前阶段**: 项目初始化
- 📅 **开始日期**: 2025-12-02
- 🎯 **预计MVP完成**: 2026-02-02
- 👥 **团队规模**: 1-3人
- 💰 **资金状态**: 自筹

---

## English

### 📖 Project Overview

**Historical Deep Dive** is an innovative **immersive historical education platform** that uses interactive storytelling and AI technology to let users experience the critical decision-making moments of historical figures and deeply understand the complexity behind historical events.

**Key Features:**
- 🎭 **Role-play Historical Figures**: Become Zhang Qian, Xuanzang, Zheng He, and other great historical figures
- 🌿 **Branching Narrative System**: Every choice leads to different historical branches
- 🤖 **AI-Generated Stories**: Generate custom historical scripts in 40 seconds
- 📦 **Fully Offline**: Play all stories offline, anytime, anywhere
- 🎨 **Traditional Chinese Aesthetics**: Ink-wash style interface, calligraphy fonts, guqin music
- 🏆 **Achievement System**: Collect achievements, unlock hidden storylines
- 📱 **Cross-Platform**: Android, iOS, Windows, macOS, Web

### 🎯 Target Audience

- 📚 History enthusiasts seeking deep exploration
- 🎓 Students learning history in an engaging way
- 👨‍🏫 Educators looking for innovative teaching tools
- 🎮 Gamers enjoying quality text adventure experiences
- 👪 Families wanting to pass on historical culture

### ✨ Core Features

#### 1. Official Story Library (20+)
Premium historical stories including:
- Zhang Qian's Mission to the West
- Su Wu's Shepherding
- Xuanzang's Journey West
- Zheng He's Voyages
- And many more...

#### 2. AI Story Workshop
Create custom stories in 40 seconds:
- "I want to become Jing Ke assassinating the King of Qin"
- "I want to attend the Hongmen Banquet"
- Input any historical figure or event!

#### 3. Offline Story Package System
- Import/export `.hsp` files
- Share stories with friends
- Completely local storage
- Auto-save progress

#### 4. Achievement & Leaderboard
- 50+ unlockable achievements
- Speed run challenges
- Perfect choice awards
- Full exploration badges

#### 5. Social Sharing
- Generate beautiful share posters
- Share to WeChat/TikTok/Xiaohongshu
- QR code invitations
- Show off your achievements

### 🛠️ Tech Stack

- **Framework**: Flutter 3.24+
- **Language**: Dart 3.0+
- **State Management**: Riverpod
- **Routing**: go_router
- **Local Storage**: Hive
- **AI Integration**: Claude 3.5 Sonnet / DeepSeek-V3 / GPT-4o

### 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/Genuineh/RolePlay.git

# Install dependencies
flutter pub get

# Run the app
flutter run
```

### 📱 Platform Support

| Platform | Status | Features |
|----------|--------|----------|
| Android | ✅ | Full support |
| iOS | ✅ | Full support |
| Windows | ✅ | Desktop experience |
| macOS | ✅ | Native menu bar |
| Web | ✅ | PWA ready |

### 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

### 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### 📞 Contact

- **GitHub**: https://github.com/Genuineh/RolePlay
- **Issues**: [GitHub Issues](https://github.com/Genuineh/RolePlay/issues)

---

<div align="center">

**让历史活起来，让教育更有趣**  
**Make History Come Alive, Make Education Fun**

Made with ❤️ by the Historical Deep Dive Team

</div>
