# 《美容注射的艺术与生活美学》可视化网站建设计划
## Web Visualization Platform Development Plan

---

## 📋 项目概述 (Project Overview)

### 项目目标
为《美容注射的艺术与生活美学》书籍创建一个优雅、专业、用户友好的可视化网站平台，结合AI对话、图像生成和交互式内容展示功能。

### 目标用户
- **主要用户群**：18-45岁女性用户
- **次要用户群**：医美从业人员、科普爱好者
- **设备分布**：移动端优先（70%），平板和PC（30%）

### 核心价值主张
- 优雅的中性化设计，平衡专业性与亲和力
- AI赋能的交互式学习体验
- 丰富的可视化内容展示
- 跨平台无缝体验（特别优化iOS兼容性）

---

## 🎨 设计系统 (Design System)

### 整体美学风格

#### 色彩方案 (Color Palette)
**主色调（Primary Colors）**
```
- 高级灰: #8B8B8D, #A5A5A7
- 米白: #FAF9F6, #F5F5F0
- 浅驼色: #D4C5B9, #C9B8A8
```

**辅助色（Secondary Colors）**
```
- 柔和薄荷绿: #B8E6D5, #A8D5C5
- 淡紫: #D5C6E1, #C4B5D5
- 粉蓝: #C5D5E8, #B5C5D8
```

**强调色（Accent Colors）**
```
- 玫瑰金: #E5C3C6, #D4B3B6
- 浅珊瑚色: #F4C8C0, #E8B8B0
```

**功能色（Functional Colors）**
```
- 成功: #B8E6D5 (柔和绿)
- 警告: #F4D9C0 (柔和橙)
- 错误: #F4C8C8 (柔和红)
- 信息: #C5D5E8 (柔和蓝)
```

#### 排版系统 (Typography)

**字体家族**
```css
/* 中文主字体 */
font-family: 'PingFang SC', 'Microsoft YaHei', sans-serif;

/* 英文主字体 */
font-family: 'Inter', 'SF Pro Display', -apple-system, sans-serif;

/* 代码/等宽字体 */
font-family: 'JetBrains Mono', 'Fira Code', monospace;
```

**字号层级**
```
- 超大标题 (Hero): 36px / 2.25rem (mobile), 48px / 3rem (desktop)
- 一级标题 (H1): 28px / 1.75rem (mobile), 36px / 2.25rem (desktop)
- 二级标题 (H2): 24px / 1.5rem (mobile), 30px / 1.875rem (desktop)
- 三级标题 (H3): 20px / 1.25rem (mobile), 24px / 1.5rem (desktop)
- 正文 (Body): 16px / 1rem (默认中号)
  - 小号: 14px / 0.875rem
  - 大号: 18px / 1.125rem
- 辅助文字 (Caption): 14px / 0.875rem (mobile), 14px / 0.875rem (desktop)
- 小字 (Small): 12px / 0.75rem (用于备案信息等)
```

**字重**
```
- Thin: 100
- Light: 300
- Regular: 400 (正文默认)
- Medium: 500 (标题默认)
- Semibold: 600 (强调)
- Bold: 700 (重要标题)
```

**行高**
```
- 标题行高: 1.2-1.3
- 正文行高: 1.6-1.8
- 辅助文字行高: 1.4-1.5
```

#### 间距系统 (Spacing)
```
- xs: 4px / 0.25rem
- sm: 8px / 0.5rem
- md: 16px / 1rem
- lg: 24px / 1.5rem
- xl: 32px / 2rem
- 2xl: 48px / 3rem
- 3xl: 64px / 4rem
- 4xl: 96px / 6rem
```

#### 圆角系统 (Border Radius)
```
- none: 0
- sm: 4px / 0.25rem
- md: 8px / 0.5rem
- lg: 12px / 0.75rem
- xl: 16px / 1rem
- 2xl: 24px / 1.5rem
- full: 9999px (圆形)
```

#### 阴影系统 (Shadows)
```css
/* 轻量阴影 */
--shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);

/* 标准阴影 */
--shadow-md: 0 4px 6px rgba(0, 0, 0, 0.07), 0 2px 4px rgba(0, 0, 0, 0.05);

/* 提升阴影 */
--shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1), 0 4px 6px rgba(0, 0, 0, 0.05);

/* 浮动阴影 */
--shadow-xl: 0 20px 25px rgba(0, 0, 0, 0.1), 0 10px 10px rgba(0, 0, 0, 0.04);
```

### 图标设计规范

#### Web Font 图标库选择
- **主要图标库**: Remix Icon (推荐，现代简约风格)
- **备选方案**: Phosphor Icons 或 Material Symbols
- **图标风格**: 线性图标为主，关键位置使用轻量填充

#### 自定义SVG图标
为核心医美概念创建定制图标：
- 透明质酸分子结构
- 肉毒素作用机制
- 皮肤层次结构
- 注射技术示意
- 面部美学比例

#### 图标动效
```javascript
// 使用Framer Motion实现微动效
const iconAnimation = {
  hover: { scale: 1.1, rotate: 5 },
  tap: { scale: 0.95 }
}
```

---

## 🏗️ 技术架构 (Technical Stack)

### 前端框架
```
- Framework: Next.js 14+ (App Router)
- Language: TypeScript
- UI Library: React 18+
- Styling: TailwindCSS 3.4+
- Components: shadcn/ui
- Animations: Framer Motion
- Icons: Remix Icon / Phosphor Icons
```

### 状态管理
```
- Global State: Zustand
- Server State: TanStack Query (React Query)
- Form State: React Hook Form + Zod
```

### AI集成
```
- AI Provider: OpenAI API / Anthropic Claude
- Streaming: Server-Sent Events (SSE)
- Image Generation: Flux nano banana model
```

### 数据存储
```
- User Settings: LocalStorage
- Chat History: IndexedDB
- Image Cache: Cache API
```

### 部署平台
```
- Hosting: Vercel (推荐) / Netlify
- CDN: Vercel Edge Network
- Analytics: Vercel Analytics / Plausible
```

---

## 📱 响应式设计规范

### 断点系统 (Breakpoints)
```javascript
const breakpoints = {
  mobile: '375px',    // 小屏手机
  tablet: '768px',    // 平板
  laptop: '1024px',   // 笔记本
  desktop: '1440px'   // 桌面显示器
}
```

### 移动优先策略
1. **设计流程**: 先设计移动端 → 扩展到平板 → 适配桌面
2. **关键交互**: 触摸优先，点击面积 ≥ 44px × 44px
3. **内容优先级**: 移动端显示最核心功能，平板/PC展开更多
4. **性能优化**: 移动端首屏加载 < 2s

---

## 🎯 核心功能模块

### 1. Header组件

#### 结构设计
```
┌─────────────────────────────────────────┐
│ [Logo] 美容注射的艺术  [☰] [⚙️] [ℹ️]      │
└─────────────────────────────────────────┘
```

#### 功能清单
- **Logo**: 点击返回首页，尺寸自适应
- **标题**: 响应式显示（移动端简化）
- **使用说明图标**: 打开用户指南
- **关于图标**: 显示项目介绍
- **设置图标**: 打开设置面板

#### 设置面板功能
```typescript
interface Settings {
  theme: 'elegant-rose' | 'soft-mint' | 'lavender-dream' | 'warm-caramel';
  fontSize: 'small' | 'medium' | 'large'; // 默认: medium
  aiStyle: 'casual' | 'standard' | 'scientific'; // 默认: standard
  aiLength: 'detailed' | 'standard' | 'concise'; // 默认: concise
}
```

### 2. Footer组件

#### 结构设计
```
┌─────────────────────────────────────────┐
│  [主要功能导航]                           │
│  - 首页  - 章节浏览  - AI对话  - 图像生成  │
├─────────────────────────────────────────┤
│  重庆联合丽格第五医疗美容医院              │
│  地址：重庆市渝中区临江支路28号            │
│  [QR Code] 联系咨询                      │
├─────────────────────────────────────────┤
│  渝ICP备15004871号 | 渝公网安备...        │
│  邮箱: bccsw@cqlhlg.work | ☎ 023-68726872│
└─────────────────────────────────────────┘
```

#### 备案信息样式
```css
.registration-info {
  font-size: 12px;
  opacity: 0.6;
  color: var(--text-secondary);
  line-height: 1.5;
}
```

### 3. AI对话功能

#### 核心特性
- ✅ **流式输出**: 实时显示AI响应
- ✅ **iOS兼容**: 特别优化Safari兼容性
- ✅ **历史记录**: 保存对话历史，可重新加载
- ✅ **智能建议**: 自动生成后续问题
- ✅ **划词AI**: 选中文本触发AI分析

#### iOS兼容性方案
```typescript
// 使用fetch而非EventSource，确保iOS Safari兼容
async function streamAIResponse(prompt: string) {
  const response = await fetch('/api/ai/chat', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ prompt, settings })
  });
  
  const reader = response.body?.getReader();
  // 使用TextDecoder处理流
}
```

#### 建议问题生成
```typescript
interface SuggestedQuestion {
  category: '深入了解' | '相关话题' | '实际应用';
  question: string;
  emoji: string;
}
```

### 4. 图像生成功能

#### Flux nano banana集成
```typescript
interface ImageGenerationParams {
  prompt: string;
  style: 'medical-illustration' | 'artistic' | 'diagram';
  aspectRatio: '1:1' | '16:9' | '9:16';
}
```

#### 历史记录管理
```typescript
interface ImageHistory {
  id: string;
  prompt: string;
  imageUrl: string;
  timestamp: number;
  metadata: {
    style: string;
    settings: object;
  };
}
```

#### 导出功能
- **PNG导出**: 高质量图片下载
- **PDF导出**: 包含提示词和图片的完整报告
- **报告模板**: 优雅的排版设计

### 5. 内容可视化

#### 章节可视化
- SVG图表展示章节结构
- 交互式进度指示器
- 视觉化知识地图

#### 人物对话可视化
```
┌─────────────────────────────────────┐
│ [费曼头像] "让我用最简单的方式..."    │
│                                     │
│      [苏格拉底头像] "但是我们真的..." │
│                                     │
│ [老子头像] "道可道，非常道..."       │
└─────────────────────────────────────┘
```

#### 列表管理
- **分类折叠**: 长列表自动分组
- **AI刷新**: 一键重新生成内容
- **搜索过滤**: 快速查找功能

---

## 🎨 主题配色方案

### Theme 1: Elegant Rose (优雅玫瑰)
```css
:root[data-theme="elegant-rose"] {
  --primary: #E5C3C6;
  --secondary: #D4B3B6;
  --background: #FAF9F6;
  --surface: #F5F5F0;
  --text-primary: #3A3A3A;
  --text-secondary: #6B6B6B;
}
```

### Theme 2: Soft Mint (柔和薄荷)
```css
:root[data-theme="soft-mint"] {
  --primary: #B8E6D5;
  --secondary: #A8D5C5;
  --background: #F5FAF8;
  --surface: #FFFFFF;
  --text-primary: #2D3E3A;
  --text-secondary: #5A6B67;
}
```

### Theme 3: Lavender Dream (淡紫梦境)
```css
:root[data-theme="lavender-dream"] {
  --primary: #D5C6E1;
  --secondary: #C4B5D5;
  --background: #F8F7FA;
  --surface: #FFFFFF;
  --text-primary: #3A3645;
  --text-secondary: #6B677A;
}
```

### Theme 4: Warm Caramel (温暖焦糖)
```css
:root[data-theme="warm-caramel"] {
  --primary: #D4C5B9;
  --secondary: #C9B8A8;
  --background: #FAF8F5;
  --surface: #F5F3F0;
  --text-primary: #3E3A36;
  --text-secondary: #6E6A66;
}
```

---

## 📄 页面结构规划

### 1. 首页 (Home)
```
- Hero Section: 书籍介绍 + 视觉吸引
- 核心特色: 费曼教学法、苏格拉底对话、7位大师
- 快速导航: 章节浏览、AI对话、角色介绍
- 最新更新: 动态内容展示
```

### 2. 章节浏览 (Chapters)
```
- 章节卡片网格: 优雅的卡片布局
- 进度指示器: 阅读进度可视化
- 快速预览: 悬停显示章节摘要
- 标签筛选: 按主题分类
```

### 3. 角色介绍 (Characters)
```
- 7位历史人物: 费曼、苏格拉底、老子、达·芬奇、居里夫人、孔子、亚里士多德
- 人物卡片: 头像、简介、核心思想
- 对话风格展示: 典型语录
- 互动元素: 点击查看更多
```

### 4. AI对话 (AI Chat)
```
- 对话界面: 简洁的聊天UI
- 历史记录: 侧边栏显示过往对话
- 建议问题: 智能推荐相关问题
- 划词功能: 选中文本触发AI
```

### 5. 图像生成 (Image Generation)
```
- 提示词输入: 多行文本框
- 风格选择: 医学插图/艺术风格/图表
- 历史画廊: 缩略图网格
- 导出选项: PNG/PDF下载
```

### 6. 术语表 (Glossary)
```
- 搜索功能: 实时过滤
- 分类导航: A-Z索引
- 详细解释: 弹出模态框
- 相关链接: 关联章节
```

---

## 🔧 开发规范

### 文件结构
```
injection-arts-web/
├── app/
│   ├── (routes)/
│   │   ├── page.tsx              # 首页
│   │   ├── chapters/
│   │   ├── characters/
│   │   ├── ai-chat/
│   │   └── image-gen/
│   ├── api/
│   │   ├── ai/
│   │   └── images/
│   └── layout.tsx
├── components/
│   ├── ui/                       # shadcn/ui组件
│   ├── header/
│   ├── footer/
│   ├── chat/
│   └── visualization/
├── lib/
│   ├── ai/                       # AI集成
│   ├── utils/
│   └── constants/
├── public/
│   ├── logo.png
│   ├── favicon.png
│   └── consultant.png
├── styles/
│   └── globals.css
└── types/
    └── index.ts
```

### 代码规范
```typescript
// 使用TypeScript严格模式
"strict": true,
"noImplicitAny": true,

// 组件命名: PascalCase
export default function HeaderComponent() {}

// 函数命名: camelCase
function handleUserInput() {}

// 常量命名: UPPER_SNAKE_CASE
const API_ENDPOINT = '/api/ai/chat';

// 类型定义: PascalCase + Interface/Type后缀
interface UserSettings {}
type ThemeType = 'elegant-rose' | 'soft-mint';
```

### Git工作流
```bash
# 分支命名
feature/ai-chat-interface
fix/ios-streaming-bug
refactor/header-component

# Commit消息格式
feat: Add AI chat history functionality
fix: Resolve iOS Safari streaming issue
style: Update theme color palette
docs: Add API documentation
```

---

## 🧪 测试策略

### 单元测试
```
- 工具: Jest + React Testing Library
- 覆盖率目标: >80%
- 关键测试: AI流式处理、状态管理、主题切换
```

### 集成测试
```
- 工具: Playwright
- 测试场景: 用户完整流程
- 跨浏览器: Chrome, Safari, Firefox, Edge
```

### iOS专项测试
```
测试设备:
- iPhone 12/13/14 (iOS 15+)
- iPad Air/Pro (iPadOS 15+)

关键测试项:
- AI对话流式输出
- 图片上传/下载
- 触摸交互
- 性能表现
```

### 性能测试
```
目标指标:
- Lighthouse Performance: >90
- First Contentful Paint: <1.5s
- Time to Interactive: <3.5s
- Cumulative Layout Shift: <0.1
```

---

## 📅 开发时间线

### Phase 1: 基础建设 (2周)
- Week 1: 项目初始化、设计系统、技术栈搭建
- Week 2: Header/Footer组件、主题系统、响应式框架

### Phase 2: 核心功能 (4周)
- Week 3-4: AI对话功能、iOS兼容性优化
- Week 5-6: 图像生成、历史记录、导出功能

### Phase 3: 内容展示 (3周)
- Week 7: 首页、章节浏览
- Week 8: 角色介绍、对话可视化
- Week 9: 术语表、搜索功能

### Phase 4: 优化测试 (2周)
- Week 10: 性能优化、跨浏览器测试
- Week 11: 用户测试、Bug修复

### Phase 5: 上线部署 (1周)
- Week 12: 部署配置、备案完成、正式发布

**总计**: 12周（约3个月）

---

## 💰 预算估算

### 开发成本
```
- 前端开发: 8周 × 5天 × 8小时 = 320小时
- 设计工作: 2周 × 5天 × 8小时 = 80小时
- 测试QA: 2周 × 5天 × 4小时 = 40小时
```

### 服务成本（年）
```
- Vercel Pro: $20/月 × 12 = $240
- AI API: ~$50-200/月（根据使用量）
- 域名: ~$15/年
- CDN/存储: ~$10-50/月
```

### 总预算范围
```
开发阶段: 根据团队配置
年度运营: $1,000 - $3,000
```

---

## 🚀 部署清单

### 上线前检查
- [ ] 所有功能测试通过
- [ ] 性能指标达标 (Lighthouse >90)
- [ ] iOS设备全面测试
- [ ] 跨浏览器兼容性确认
- [ ] SEO优化完成
- [ ] 备案信息准确无误
- [ ] 联系方式链接有效
- [ ] 二维码图片正常显示

### 域名与备案
- [ ] 域名注册并解析
- [ ] SSL证书配置
- [ ] ICP备案完成
- [ ] 公安网备案完成
- [ ] 备案号链接添加

### 监控与分析
- [ ] Google Analytics / Plausible
- [ ] 错误监控 (Sentry)
- [ ] 性能监控 (Vercel Analytics)
- [ ] 用户反馈渠道

---

## 📞 联系信息

**开发团队**
- 项目负责人: [待定]
- GitHub仓库: https://github.com/sooogooo/ebook-injection-art

**医院信息**
- 机构: 重庆联合丽格第五医疗美容医院
- 地址: 重庆市渝中区临江支路28号
- 邮箱: bccsw@cqlhlg.work
- 电话: 023-68726872
- 在线咨询: https://work.weixin.qq.com/kfid/kfcfc2a809493f31e8f

**备案信息**
- ICP备案: 渝ICP备15004871号
- 公安备案: 渝公网安备 50010302001456号

---

**文档版本**: v1.0
**最后更新**: 2025-01-24
**状态**: 规划完成，待开发启动

*"优雅的设计源于对用户需求的深刻理解，卓越的技术实现源于对细节的执着追求。"*
