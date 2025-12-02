# 贡献指南 / Contributing Guide
# Historical Deep Dive Project

欢迎为历史深潜项目做出贡献！/ Welcome to contribute to the Historical Deep Dive project!

## 如何贡献 / How to Contribute

### 1. 报告问题 / Report Issues

如果您发现了bug或有功能建议，请：
- 搜索现有的[Issues](https://github.com/Genuineh/RolePlay/issues)，避免重复
- 使用清晰的标题和描述
- 提供复现步骤、截图或错误日志
- 说明您的操作系统和Flutter版本

### 2. 提交代码 / Submit Code

#### 步骤 / Steps

1. **Fork 本仓库**
   ```bash
   # 在GitHub上点击Fork按钮
   ```

2. **克隆到本地**
   ```bash
   git clone https://github.com/YOUR_USERNAME/RolePlay.git
   cd RolePlay
   ```

3. **创建特性分支**
   ```bash
   git checkout -b feature/amazing-feature
   # 或
   git checkout -b bugfix/fix-issue-123
   ```

4. **进行开发**
   ```bash
   # 安装依赖
   flutter pub get
   
   # 运行代码生成（如果需要）
   flutter pub run build_runner build
   
   # 运行应用
   flutter run
   ```

5. **编写测试**
   ```bash
   # 为新功能编写测试
   flutter test
   ```

6. **提交更改**
   ```bash
   git add .
   git commit -m "feat: add amazing feature"
   
   # 遵循 Conventional Commits 规范
   # feat: 新功能
   # fix: 修复bug
   # docs: 文档更新
   # style: 代码格式
   # refactor: 重构
   # test: 测试
   # chore: 构建/工具
   ```

7. **推送到GitHub**
   ```bash
   git push origin feature/amazing-feature
   ```

8. **创建 Pull Request**
   - 在GitHub上打开您的fork
   - 点击"New Pull Request"
   - 填写PR描述，说明您的更改
   - 链接相关的Issue（如果有）

### 3. 代码规范 / Code Standards

#### Dart/Flutter 代码风格

```dart
// ✅ 好的代码
class StoryCard extends StatelessWidget {
  const StoryCard({
    super.key,
    required this.story,
    this.onTap,
  });

  final Story story;
  final VoidCallback? onTap;

  @override
  Widget build(BuildContext context) {
    return Card(
      child: ListTile(
        title: Text(story.title),
        onTap: onTap,
      ),
    );
  }
}

// ❌ 不好的代码
class story_card extends StatelessWidget {
  story_card({this.story, this.onTap});  // 缺少 key, const
  
  var story;  // 类型不明确
  var onTap;
  
  Widget build(context) {  // 缺少类型注解
    return Card(
      child: ListTile(
        title: Text(story.title)
      )  // 缺少逗号
    );
  }
}
```

#### 命名规范

- **类名**: `PascalCase` (例如: `StoryCard`, `PlayerScreen`)
- **变量/函数**: `camelCase` (例如: `currentNode`, `loadStory()`)
- **常量**: `lowerCamelCase` (例如: `maxStorySize`)
- **私有成员**: `_leadingUnderscore` (例如: `_storyBox`, `_loadData()`)
- **文件名**: `snake_case` (例如: `story_card.dart`, `player_screen.dart`)

#### 文档注释

```dart
/// 故事卡片组件，用于在列表中显示故事信息
/// 
/// 显示故事的封面、标题、描述和进度。
/// 点击卡片会导航到故事详情页。
/// 
/// Example:
/// ```dart
/// StoryCard(
///   story: myStory,
///   onTap: () => context.go('/player/${myStory.id}'),
/// )
/// ```
class StoryCard extends StatelessWidget {
  // ...
}
```

#### 代码组织

```dart
class MyWidget extends StatelessWidget {
  // 1. Constructor
  const MyWidget({super.key, required this.data});
  
  // 2. Fields
  final String data;
  
  // 3. Static methods
  static MyWidget create() => MyWidget(data: 'default');
  
  // 4. Lifecycle methods
  @override
  Widget build(BuildContext context) {
    return _buildContent();
  }
  
  // 5. Private methods
  Widget _buildContent() {
    return Container();
  }
}
```

### 4. 提交信息规范 / Commit Message Convention

使用 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

```
<type>(<scope>): <subject>

<body>

<footer>
```

#### Types

- `feat`: 新功能
- `fix`: 修复bug
- `docs`: 文档更新
- `style`: 代码格式（不影响代码逻辑）
- `refactor`: 重构（既不是新功能也不是修复bug）
- `perf`: 性能优化
- `test`: 测试相关
- `chore`: 构建过程或辅助工具的变动

#### 示例

```bash
feat(player): add auto-save functionality

Implement automatic progress saving every 30 seconds
during story playback. This prevents progress loss if
the app crashes or user force-quits.

Closes #123

---

fix(ai): handle timeout errors gracefully

Previously, timeout errors would crash the app.
Now they show a user-friendly error message with
retry option.

Fixes #456

---

docs(readme): update installation instructions

Add steps for Windows platform setup.
```

### 5. Pull Request 规范

#### PR标题
使用与commit message相同的规范：
```
feat(player): add encyclopedia popup
fix(storage): resolve Hive initialization race condition
```

#### PR描述模板

```markdown
## 描述 / Description
简要描述这个PR的目的和内容

## 更改类型 / Type of Change
- [ ] Bug fix (修复bug)
- [ ] New feature (新功能)
- [ ] Breaking change (破坏性更改)
- [ ] Documentation update (文档更新)

## 测试 / Testing
- [ ] 我已经在本地测试了这些更改
- [ ] 我已经添加了相应的测试
- [ ] 所有现有测试都通过

## 截图 / Screenshots
（如果是UI更改，请提供截图）

## 相关Issue / Related Issues
Closes #123
Fixes #456

## 检查清单 / Checklist
- [ ] 我的代码遵循项目的代码规范
- [ ] 我已经进行了自我审查
- [ ] 我已经注释了难以理解的代码
- [ ] 我已经更新了相关文档
- [ ] 我的更改没有产生新的警告
- [ ] 我已经添加了测试证明修复有效或功能正常工作
```

### 6. 代码审查 / Code Review

当您的PR提交后：

1. **自动检查**
   - CI会自动运行linter和测试
   - 确保所有检查都通过

2. **人工审查**
   - 维护者会审查您的代码
   - 可能会提出修改建议
   - 请及时响应反馈

3. **合并**
   - 审查通过后，维护者会合并您的PR
   - 您的贡献将出现在贡献者列表中

### 7. 内容贡献 / Content Contribution

#### 编写故事内容

如果您想贡献历史故事内容：

1. **选择历史主题**
   - 确保史实准确
   - 选择有教育价值的内容
   - 避免重复已有故事

2. **故事结构**
   ```json
   {
     "id": "story_unique_id",
     "title": "故事标题",
     "description": "简短描述（50-100字）",
     "nodes": [
       {
         "id": "node_1",
         "type": "narrative",
         "content": "故事内容，要生动有趣..."
       }
     ]
   }
   ```

3. **质量要求**
   - 历史准确性：所有史实必须有据可查
   - 教育价值：包含历史知识和文化内涵
   - 可玩性：至少3个不同结局，5-8个决策点
   - 文字质量：流畅、生动、无错别字

4. **提交方式**
   - 将故事JSON文件放在 `assets/community_stories/`
   - 附上参考资料和出处
   - 说明教育意义和目标受众

### 8. 翻译贡献 / Translation

帮助我们翻译应用到其他语言：

1. **支持的语言**
   - 中文（简体）✅
   - 英文 🔄
   - 日文 📝
   - 韩文 📝
   - 更多...

2. **翻译文件位置**
   ```
   lib/l10n/
   ├── app_en.arb  # 英文
   ├── app_zh.arb  # 中文
   └── app_ja.arb  # 日文
   ```

3. **翻译规范**
   - 保持原意
   - 符合目标语言习惯
   - 保留占位符 `{variable}`
   - 注意文化差异

### 9. 设计贡献 / Design Contribution

如果您是设计师：

1. **UI/UX设计**
   - 使用Figma或Sketch
   - 遵循现有设计语言
   - 提供设计文件和导出资源

2. **图标和插图**
   - 符合中国传统美学
   - 提供SVG或高分辨率PNG
   - 确保版权清晰

3. **字体和排版**
   - 推荐免费商用字体
   - 提供字体文件或下载链接

### 10. 获取帮助 / Get Help

遇到问题？

- 📖 阅读文档：[docs/](../docs/)
- 💬 提问：[GitHub Discussions](https://github.com/Genuineh/RolePlay/discussions)
- 🐛 报告Bug：[GitHub Issues](https://github.com/Genuineh/RolePlay/issues)
- 📧 联系维护者：[待添加]

---

## 贡献者公约 / Contributor Covenant

### 我们的承诺

为了促进一个开放和友好的环境，我们作为贡献者和维护者承诺：无论年龄、体型、残疾、种族、性别认同和表达、经验水平、国籍、个人形象、种族、宗教或性取向如何，参与我们的项目和社区的每个人都不会受到骚扰。

### 我们的标准

积极行为的例子：
- 使用友好和包容的语言
- 尊重不同的观点和经验
- 优雅地接受建设性批评
- 关注对社区最有利的事情
- 对其他社区成员表示同理心

不可接受的行为例子：
- 使用性化的语言或图像
- 侮辱/贬损的评论，人身攻击
- 公开或私下骚扰
- 未经许可发布他人的私人信息
- 其他在专业环境中被认为不适当的行为

---

## 许可证 / License

通过向此项目贡献代码，您同意您的贡献将按照项目的MIT许可证进行许可。

---

## 致谢 / Acknowledgments

感谢所有为项目做出贡献的人！

[![贡献者](https://contrib.rocks/image?repo=Genuineh/RolePlay)](https://github.com/Genuineh/RolePlay/graphs/contributors)

---

**最后更新**: 2025-12-02  
**版本**: 1.0  
**维护者**: Historical Deep Dive Team

让我们一起打造最好的历史教育应用！🚀
