# API 文档 / API Documentation
# Historical Deep Dive - AI Integration & Services

## 概览 / Overview

本文档描述历史深潜应用的API集成方案，包括AI故事生成、云函数部署和数据服务接口。

---

## 1. AI Story Generation API

### 1.1 Serverless Function Endpoint

#### Recommended Providers
1. **Cloudflare Workers** (首选)
   - URL: `https://your-worker.workers.dev/api/generate`
   - 优点: 全球CDN, 免费额度高, 低延迟
   - 成本: 免费10万请求/天

2. **Aliyun Function Compute** (备选)
   - URL: `https://your-fc.cn-hangzhou.fc.aliyuncs.com/api/generate`
   - 优点: 国内速度快, 支付宝绑定
   - 成本: ¥0.00003/请求

3. **Vercel Serverless Functions** (国际版)
   - URL: `https://your-app.vercel.app/api/generate`
   - 优点: 易部署, GitHub集成
   - 成本: 免费10万次/月

### 1.2 Request Format

#### Endpoint
```
POST /api/generate
Content-Type: application/json
```

#### Request Body
```json
{
  "prompt": "我想成为荆轲刺秦王",
  "difficulty": "medium",
  "estimatedMinutes": 30,
  "language": "zh",
  "model": "claude-3.5-sonnet",
  "maxNodes": 32,
  "minEndings": 3
}
```

#### Parameters

| Field | Type | Required | Description | Example |
|-------|------|----------|-------------|---------|
| `prompt` | string | Yes | 用户输入的历史人物或事件 | "我想成为张骞出使西域" |
| `difficulty` | string | No | 难度等级 (easy/medium/hard/expert) | "medium" |
| `estimatedMinutes` | number | No | 预期游玩时长（分钟） | 30 |
| `language` | string | No | 语言代码 (zh/en) | "zh" |
| `model` | string | No | AI模型选择 | "claude-3.5-sonnet" |
| `maxNodes` | number | No | 最大节点数 | 32 |
| `minEndings` | number | No | 最少结局数 | 3 |

### 1.3 Response Format

#### Success Response (200 OK)
```json
{
  "success": true,
  "generationTime": 42.5,
  "model": "claude-3.5-sonnet",
  "story": {
    "id": "story_jingke_20250102_abcd1234",
    "title": "当我成为荆轲",
    "description": "公元前227年，燕国太子丹密谋刺秦，你作为荆轲，将面临人生中最重要的抉择...",
    "author": "AI Generated",
    "coverImagePath": "assets/characters/jingke.jpg",
    "difficulty": "medium",
    "estimatedMinutes": 30,
    "tags": ["战国", "刺客", "历史转折"],
    "metadata": {
      "historicalPeriod": "战国时期",
      "mainCharacter": "荆轲",
      "historicalEvent": "荆轲刺秦王",
      "generatedAt": "2025-01-02T10:30:00Z",
      "aiModel": "claude-3.5-sonnet"
    },
    "nodes": [
      {
        "id": "node_1",
        "type": "narrative",
        "content": "公元前227年，易水河畔。寒风凛冽...",
        "imagePath": "assets/scenes/yishui.jpg",
        "nextNodeIds": ["node_2"]
      },
      {
        "id": "node_2",
        "type": "choice",
        "content": "太子丹握着你的手，眼中满是期待...",
        "question": {
          "id": "q_1",
          "type": "multipleChoice",
          "questionText": "此刻，你会如何回应太子丹？",
          "choices": [
            {
              "id": "c1",
              "text": "慷慨激昂：风萧萧兮易水寒，壮士一去兮不复还！",
              "isCorrect": true
            },
            {
              "id": "c2",
              "text": "谨慎思考：容我再思考一下具体计划",
              "isCorrect": false
            },
            {
              "id": "c3",
              "text": "婉拒使命：此事凶险，恕我不能从命",
              "isCorrect": false
            }
          ],
          "correctAnswer": "c1",
          "explanation": "历史上，荆轲确实说出了千古名句，展现了视死如归的勇气。",
          "branchMapping": {
            "c1": "node_3_hero",
            "c2": "node_3_cautious",
            "c3": "node_3_refuse"
          }
        },
        "encyclopedia": {
          "title": "荆轲其人",
          "content": "荆轲（？－公元前227年），战国末期卫国人...",
          "imageUrl": "assets/encyclopedia/jingke_portrait.jpg"
        }
      }
    ]
  }
}
```

#### Error Response (400/500)
```json
{
  "success": false,
  "error": {
    "code": "GENERATION_FAILED",
    "message": "AI故事生成失败，请稍后重试",
    "details": "Rate limit exceeded: 10 requests per minute"
  }
}
```

### 1.4 Error Codes

| Code | HTTP Status | Description | User Action |
|------|-------------|-------------|-------------|
| `INVALID_PROMPT` | 400 | 提示词无效或为空 | 重新输入合法的历史人物/事件 |
| `RATE_LIMIT_EXCEEDED` | 429 | 超过请求频率限制 | 等待1分钟后重试 |
| `AI_SERVICE_ERROR` | 500 | AI服务暂时不可用 | 稍后重试或更换模型 |
| `CONTENT_FILTER_BLOCKED` | 403 | 内容被安全过滤器拦截 | 修改提示词，避免敏感内容 |
| `GENERATION_TIMEOUT` | 504 | 生成超时（>120秒） | 减少节点数或降低难度 |

---

## 2. Serverless Function Implementation

### 2.1 Cloudflare Workers Example

#### File: `workers/generate.js`

```javascript
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  // CORS headers
  const corsHeaders = {
    'Access-Control-Allow-Origin': '*',
    'Access-Control-Allow-Methods': 'POST, OPTIONS',
    'Access-Control-Allow-Headers': 'Content-Type',
  }
  
  if (request.method === 'OPTIONS') {
    return new Response(null, { headers: corsHeaders })
  }
  
  if (request.method !== 'POST') {
    return new Response('Method not allowed', { status: 405 })
  }
  
  try {
    // Parse request
    const body = await request.json()
    const { prompt, difficulty = 'medium', estimatedMinutes = 30, model = 'claude-3.5-sonnet' } = body
    
    // Validate
    if (!prompt || prompt.length < 5) {
      return jsonResponse({ 
        success: false, 
        error: { code: 'INVALID_PROMPT', message: '提示词太短' }
      }, 400, corsHeaders)
    }
    
    // Rate limiting (using KV storage)
    const clientId = request.headers.get('X-Client-ID') || 'anonymous'
    const rateLimitKey = `ratelimit_${clientId}`
    const count = await RATE_LIMIT_KV.get(rateLimitKey) || 0
    
    if (count >= 10) {
      return jsonResponse({
        success: false,
        error: { code: 'RATE_LIMIT_EXCEEDED', message: '请求过于频繁' }
      }, 429, corsHeaders)
    }
    
    await RATE_LIMIT_KV.put(rateLimitKey, count + 1, { expirationTtl: 60 })
    
    // Call AI API
    const startTime = Date.now()
    const story = await generateStoryWithAI(prompt, difficulty, estimatedMinutes, model)
    const generationTime = (Date.now() - startTime) / 1000
    
    // Return response
    return jsonResponse({
      success: true,
      generationTime,
      model,
      story
    }, 200, corsHeaders)
    
  } catch (error) {
    console.error('Generation error:', error)
    return jsonResponse({
      success: false,
      error: { 
        code: 'AI_SERVICE_ERROR', 
        message: 'AI生成失败',
        details: error.message
      }
    }, 500, corsHeaders)
  }
}

async function generateStoryWithAI(prompt, difficulty, estimatedMinutes, model) {
  const apiKey = AI_API_KEY // Environment variable
  
  // Build full prompt
  const fullPrompt = buildFullPrompt(prompt, difficulty, estimatedMinutes)
  
  // Call Claude API
  const response = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'x-api-key': apiKey,
      'anthropic-version': '2023-06-01'
    },
    body: JSON.stringify({
      model: 'claude-3-5-sonnet-20241022',
      max_tokens: 16000,
      temperature: 0.7,
      messages: [{
        role: 'user',
        content: fullPrompt
      }]
    })
  })
  
  if (!response.ok) {
    throw new Error(`Claude API error: ${response.status}`)
  }
  
  const data = await response.json()
  const storyText = data.content[0].text
  
  // Parse JSON from response
  const storyJson = extractJsonFromText(storyText)
  
  // Validate structure
  validateStoryStructure(storyJson)
  
  // Match images
  await matchImagesForStory(storyJson)
  
  return storyJson
}

function buildFullPrompt(userPrompt, difficulty, estimatedMinutes) {
  return `
你是一位精通中国历史的大师级故事作家。请根据以下要求生成一个完整的交互式历史故事。

【用户需求】
${userPrompt}

【故事要求】
- 难度等级: ${difficulty}
- 预计时长: ${estimatedMinutes}分钟
- 节点数量: ${Math.floor(estimatedMinutes / 1.5)} - ${Math.floor(estimatedMinutes / 1)} 个
- 结局数量: 至少3个不同结局

【历史准确性要求】
1. 所有历史事件、人物、地点必须真实准确
2. 时间线要符合历史记录
3. 人物性格和行为要符合史书记载
4. 不得虚构重大历史事件

【故事结构要求】
1. 开场：引人入胜的历史场景设定
2. 发展：5-8个关键决策点
3. 分支：每个决策至少2个选项，正确/错误分支
4. 高潮：历史转折点的抉择
5. 结局：3-5个不同历史结局

【选择设计原则】
1. 选项要基于真实历史可能性
2. 正确选项应该有历史依据
3. 错误选项导向合理的历史分支
4. 避免绝对的对错，展现历史复杂性

【输出格式】
请以JSON格式输出，结构如下：
\`\`\`json
{
  "id": "story_unique_id",
  "title": "故事标题",
  "description": "50-100字故事简介",
  "author": "AI Generated",
  "difficulty": "${difficulty}",
  "estimatedMinutes": ${estimatedMinutes},
  "tags": ["标签1", "标签2"],
  "metadata": {
    "historicalPeriod": "历史时期",
    "mainCharacter": "主角名字",
    "historicalEvent": "历史事件"
  },
  "nodes": [
    {
      "id": "node_1",
      "type": "narrative",
      "content": "故事内容...",
      "nextNodeIds": ["node_2"]
    },
    {
      "id": "node_2",
      "type": "choice",
      "content": "场景描述...",
      "question": {
        "id": "q_1",
        "type": "multipleChoice",
        "questionText": "你会如何做？",
        "choices": [
          {"id": "c1", "text": "选项1", "isCorrect": true},
          {"id": "c2", "text": "选项2", "isCorrect": false}
        ],
        "correctAnswer": "c1",
        "explanation": "历史解释...",
        "branchMapping": {
          "c1": "node_3_positive",
          "c2": "node_3_negative"
        }
      },
      "encyclopedia": {
        "title": "历史知识点",
        "content": "详细解释..."
      }
    }
  ]
}
\`\`\`

【重要提示】
- 必须返回完整的、可解析的JSON
- 所有节点ID必须唯一且在branchMapping中正确引用
- 至少包含一个ending类型的节点
- 内容要生动有趣，但保持历史严肃性
- 避免现代语言和观念

现在请开始创作！
  `.trim()
}

function jsonResponse(data, status = 200, headers = {}) {
  return new Response(JSON.stringify(data), {
    status,
    headers: {
      'Content-Type': 'application/json',
      ...headers
    }
  })
}

// Helper functions
function extractJsonFromText(text) {
  // Extract JSON from markdown code blocks or plain text
  const jsonMatch = text.match(/```json\n([\s\S]*?)\n```/) || 
                   text.match(/```\n([\s\S]*?)\n```/) ||
                   [null, text]
  
  try {
    return JSON.parse(jsonMatch[1])
  } catch (error) {
    throw new Error('Failed to parse AI response as JSON')
  }
}

function validateStoryStructure(story) {
  if (!story.id || !story.title || !story.nodes || story.nodes.length < 10) {
    throw new Error('Invalid story structure')
  }
  
  // Validate node connections
  const nodeIds = new Set(story.nodes.map(n => n.id))
  for (const node of story.nodes) {
    if (node.nextNodeIds) {
      for (const nextId of node.nextNodeIds) {
        if (!nodeIds.has(nextId)) {
          throw new Error(`Invalid node reference: ${nextId}`)
        }
      }
    }
  }
  
  // Check for at least one ending
  const hasEnding = story.nodes.some(n => n.type === 'ending')
  if (!hasEnding) {
    throw new Error('Story must have at least one ending node')
  }
}

async function matchImagesForStory(story) {
  // Simple keyword matching to pre-loaded image library
  // In production, this could call an AI image generation API
  
  const imageLibrary = {
    '战国': 'assets/periods/warring_states.jpg',
    '秦朝': 'assets/periods/qin.jpg',
    '汉朝': 'assets/periods/han.jpg',
    '唐朝': 'assets/periods/tang.jpg',
    '宋朝': 'assets/periods/song.jpg',
    '明朝': 'assets/periods/ming.jpg',
    '清朝': 'assets/periods/qing.jpg',
  }
  
  // Match cover image
  const period = story.metadata?.historicalPeriod || ''
  story.coverImagePath = imageLibrary[period] || 'assets/default_cover.jpg'
  
  // Match node images based on keywords
  for (const node of story.nodes) {
    if (!node.imagePath) {
      // Simple keyword-based matching
      node.imagePath = matchImageByKeywords(node.content, imageLibrary)
    }
  }
}

function matchImageByKeywords(content, library) {
  for (const [keyword, imagePath] of Object.entries(library)) {
    if (content.includes(keyword)) {
      return imagePath
    }
  }
  return 'assets/default_scene.jpg'
}
```

### 2.2 Deployment

#### Cloudflare Workers
```bash
# Install Wrangler CLI
npm install -g wrangler

# Login
wrangler login

# Create project
wrangler init historical-deep-dive-api

# Add secrets
wrangler secret put AI_API_KEY

# Deploy
wrangler deploy
```

#### Environment Variables
```toml
# wrangler.toml
name = "historical-deep-dive-api"
main = "src/index.js"
compatibility_date = "2025-01-02"

[vars]
ENVIRONMENT = "production"

[[kv_namespaces]]
binding = "RATE_LIMIT_KV"
id = "your_kv_namespace_id"
```

---

## 3. Flutter Client Integration

### 3.1 AI Service Class

```dart
// lib/data/services/ai_service.dart
import 'package:dio/dio.dart';
import '../models/story.dart';

class AIService {
  final Dio _dio;
  final String _endpoint;
  
  AIService({
    required Dio dio,
    required String endpoint,
  }) : _dio = dio, _endpoint = endpoint;
  
  Future<Story> generateStory({
    required String prompt,
    DifficultyLevel difficulty = DifficultyLevel.medium,
    int estimatedMinutes = 30,
    String model = 'claude-3.5-sonnet',
  }) async {
    try {
      final response = await _dio.post(
        _endpoint,
        data: {
          'prompt': prompt,
          'difficulty': difficulty.name,
          'estimatedMinutes': estimatedMinutes,
          'model': model,
        },
        options: Options(
          receiveTimeout: const Duration(seconds: 120),
          sendTimeout: const Duration(seconds: 30),
        ),
      );
      
      if (response.statusCode == 200 && response.data['success'] == true) {
        final storyJson = response.data['story'];
        return Story.fromJson(storyJson);
      } else {
        throw AIGenerationException(
          response.data['error']['message'] ?? 'Unknown error'
        );
      }
    } on DioException catch (e) {
      if (e.type == DioExceptionType.receiveTimeout) {
        throw AIGenerationException('生成超时，请重试');
      } else if (e.response?.statusCode == 429) {
        throw AIGenerationException('请求过于频繁，请稍后再试');
      } else {
        throw AIGenerationException('网络错误：${e.message}');
      }
    }
  }
}

class AIGenerationException implements Exception {
  final String message;
  AIGenerationException(this.message);
  
  @override
  String toString() => message;
}
```

### 3.2 Usage Example

```dart
// In Creator Screen
final aiService = ref.read(aiServiceProvider);

try {
  setState(() => isGenerating = true);
  
  final story = await aiService.generateStory(
    prompt: '我想成为荆轲刺秦王',
    difficulty: DifficultyLevel.medium,
    estimatedMinutes: 30,
  );
  
  // Save story
  await ref.read(storyRepositoryProvider).saveStory(story);
  
  // Navigate to player
  context.go('/player/${story.id}');
  
} on AIGenerationException catch (e) {
  ScaffoldMessenger.of(context).showSnackBar(
    SnackBar(content: Text(e.message)),
  );
} finally {
  setState(() => isGenerating = false);
}
```

---

## 4. Rate Limiting & Cost Management

### 4.1 Client-Side Rate Limiting

```dart
class RateLimiter {
  static const maxRequestsPerDay = 10;
  static const storageKey = 'ai_generation_count';
  
  Future<bool> canMakeRequest() async {
    final prefs = await SharedPreferences.getInstance();
    final today = DateTime.now().toIso8601String().substring(0, 10);
    final key = '${storageKey}_$today';
    final count = prefs.getInt(key) ?? 0;
    
    return count < maxRequestsPerDay;
  }
  
  Future<void> recordRequest() async {
    final prefs = await SharedPreferences.getInstance();
    final today = DateTime.now().toIso8601String().substring(0, 10);
    final key = '${storageKey}_$today';
    final count = prefs.getInt(key) ?? 0;
    await prefs.setInt(key, count + 1);
  }
  
  Future<int> getRemainingRequests() async {
    final prefs = await SharedPreferences.getInstance();
    final today = DateTime.now().toIso8601String().substring(0, 10);
    final key = '${storageKey}_$today';
    final count = prefs.getInt(key) ?? 0;
    return maxRequestsPerDay - count;
  }
}
```

### 4.2 Cost Estimation

#### Claude 3.5 Sonnet Pricing
- Input: $3 / 1M tokens
- Output: $15 / 1M tokens
- Average story: ~8K input + ~12K output = $0.18 per story

#### Monthly Cost Projection
```
100 users × 5 stories/month = 500 stories
500 × $0.18 = $90/month

1,000 users × 5 stories/month = 5,000 stories
5,000 × $0.18 = $900/month

10,000 users × 5 stories/month = 50,000 stories  
50,000 × $0.18 = $9,000/month
```

#### Cost Optimization Strategies
1. **Caching**: Cache similar prompts for 24h
2. **DeepSeek Fallback**: Much cheaper ($0.02 per story)
3. **Rate Limiting**: 10 stories per user per day
4. **Freemium Model**: Charge for unlimited generations

---

## 5. Alternative AI Providers

### 5.1 DeepSeek API

```javascript
// Lower cost alternative
const response = await fetch('https://api.deepseek.com/v1/chat/completions', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${DEEPSEEK_API_KEY}`
  },
  body: JSON.stringify({
    model: 'deepseek-chat',
    messages: [{
      role: 'user',
      content: fullPrompt
    }],
    max_tokens: 16000,
    temperature: 0.7
  })
})

// Cost: ~$0.02 per story (10x cheaper than Claude)
```

### 5.2 OpenAI GPT-4o

```javascript
// Fallback option
const response = await fetch('https://api.openai.com/v1/chat/completions', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${OPENAI_API_KEY}`
  },
  body: JSON.stringify({
    model: 'gpt-4o',
    messages: [{
      role: 'user',
      content: fullPrompt
    }],
    max_tokens: 16000,
    temperature: 0.7
  })
})

// Cost: ~$0.12 per story (middle ground)
```

---

## 6. Testing & Debugging

### 6.1 Test Prompts

```
简单: "我想成为苏武牧羊"
中等: "我想成为张骞出使西域"
困难: "我想参与玄奘西天取经"
专家: "我想成为郑和指挥下西洋船队"
```

### 6.2 Monitoring

```javascript
// Add logging to serverless function
console.log('[AI Generation]', {
  prompt: prompt.substring(0, 50),
  difficulty,
  startTime: new Date().toISOString(),
  model
})

// Track metrics
await METRICS_KV.put(`generation_${Date.now()}`, JSON.stringify({
  success: true,
  generationTime,
  nodeCount: story.nodes.length,
  model
}))
```

---

**API Version**: 1.0  
**Last Updated**: 2025-12-02  
**Maintained By**: Historical Deep Dive Team
