# 网站开发快速启动指南
## Website Development Quick Start Guide

---

## 🚀 快速开始

### 1. 项目初始化

```bash
# 创建Next.js项目
npx create-next-app@latest injection-arts-web --typescript --tailwind --app

cd injection-arts-web

# 安装核心依赖
npm install zustand @tanstack/react-query framer-motion
npm install lucide-react class-variance-authority clsx tailwind-merge
npm install react-hook-form zod @hookform/resolvers

# 安装shadcn/ui CLI
npx shadcn-ui@latest init

# 安装常用组件
npx shadcn-ui@latest add button card dialog dropdown-menu input textarea
npx shadcn-ui@latest add select switch tabs toast accordion
```

### 2. 配置图标库

```bash
# 安装Remix Icon (推荐)
npm install remixicon

# 或者使用Lucide React (已包含在shadcn/ui中)
# lucide-react 已安装
```

### 3. 下载资源文件

```bash
# 创建public目录结构
mkdir -p public/images

# 下载logo和favicon
curl -o public/logo.png https://docs.bccsw.cn/logo.png
curl -o public/favicon.png https://docs.bccsw.cn/favicon.png
curl -o public/images/consultant.png https://docs.bccsw.cn/consultant.png
```

---

## 📁 项目结构

```
injection-arts-web/
├── app/
│   ├── globals.css
│   ├── layout.tsx
│   ├── page.tsx
│   ├── (routes)/
│   │   ├── chapters/
│   │   │   └── page.tsx
│   │   ├── characters/
│   │   │   └── page.tsx
│   │   ├── ai-chat/
│   │   │   └── page.tsx
│   │   └── image-gen/
│   │       └── page.tsx
│   └── api/
│       ├── ai/
│       │   └── chat/
│       │       └── route.ts
│       └── images/
│           └── generate/
│               └── route.ts
├── components/
│   ├── ui/              # shadcn/ui components
│   ├── layout/
│   │   ├── header.tsx
│   │   ├── footer.tsx
│   │   └── settings-panel.tsx
│   ├── chat/
│   │   ├── chat-interface.tsx
│   │   ├── message-list.tsx
│   │   └── suggested-questions.tsx
│   ├── image/
│   │   ├── image-generator.tsx
│   │   └── image-history.tsx
│   └── visualization/
│       ├── chapter-map.tsx
│       └── character-dialogue.tsx
├── lib/
│   ├── ai/
│   │   ├── openai.ts
│   │   └── stream-handler.ts
│   ├── store/
│   │   └── settings-store.ts
│   ├── utils/
│   │   └── cn.ts
│   └── constants/
│       └── themes.ts
├── types/
│   └── index.ts
├── public/
│   ├── logo.png
│   ├── favicon.png
│   └── images/
│       └── consultant.png
└── styles/
    └── themes.css
```

---

## 🎨 核心配置文件

### tailwind.config.ts

```typescript
import type { Config } from "tailwindcss";

const config: Config = {
  darkMode: ["class"],
  content: [
    "./pages/**/*.{ts,tsx}",
    "./components/**/*.{ts,tsx}",
    "./app/**/*.{ts,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        // Elegant Rose Theme
        'elegant-rose': {
          primary: '#E5C3C6',
          secondary: '#D4B3B6',
          background: '#FAF9F6',
          surface: '#F5F5F0',
        },
        // Soft Mint Theme
        'soft-mint': {
          primary: '#B8E6D5',
          secondary: '#A8D5C5',
          background: '#F5FAF8',
          surface: '#FFFFFF',
        },
        // Lavender Dream Theme
        'lavender-dream': {
          primary: '#D5C6E1',
          secondary: '#C4B5D5',
          background: '#F8F7FA',
          surface: '#FFFFFF',
        },
        // Warm Caramel Theme
        'warm-caramel': {
          primary: '#D4C5B9',
          secondary: '#C9B8A8',
          background: '#FAF8F5',
          surface: '#F5F3F0',
        },
      },
      fontFamily: {
        sans: ['var(--font-inter)', 'PingFang SC', 'Microsoft YaHei', 'sans-serif'],
        mono: ['JetBrains Mono', 'Fira Code', 'monospace'],
      },
      fontSize: {
        'xs': ['0.75rem', { lineHeight: '1.4' }],
        'sm': ['0.875rem', { lineHeight: '1.5' }],
        'base': ['1rem', { lineHeight: '1.6' }],
        'lg': ['1.125rem', { lineHeight: '1.6' }],
        'xl': ['1.25rem', { lineHeight: '1.5' }],
        '2xl': ['1.5rem', { lineHeight: '1.4' }],
        '3xl': ['1.875rem', { lineHeight: '1.3' }],
        '4xl': ['2.25rem', { lineHeight: '1.2' }],
      },
      screens: {
        'mobile': '375px',
        'tablet': '768px',
        'laptop': '1024px',
        'desktop': '1440px',
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
};

export default config;
```

### app/globals.css

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    /* 默认主题：Elegant Rose */
    --background: 250 249 246;
    --foreground: 58 58 58;
    --primary: 229 195 198;
    --primary-foreground: 58 58 58;
    --secondary: 212 179 182;
    --secondary-foreground: 58 58 58;
    --muted: 245 245 240;
    --muted-foreground: 107 107 107;
    --accent: 229 195 198;
    --accent-foreground: 58 58 58;
    --border: 229 229 229;
    --input: 229 229 229;
    --ring: 229 195 198;
    --radius: 0.5rem;
  }
}

@layer utilities {
  /* 字号工具类 */
  .text-size-small {
    font-size: 0.875rem;
  }
  
  .text-size-medium {
    font-size: 1rem;
  }
  
  .text-size-large {
    font-size: 1.125rem;
  }
  
  /* 主题切换动画 */
  .theme-transition {
    transition: background-color 0.3s ease, color 0.3s ease;
  }
}
```

---

## 🔧 核心代码示例

### 1. 设置状态管理 (lib/store/settings-store.ts)

```typescript
import { create } from 'zustand';
import { persist } from 'zustand/middleware';

export type Theme = 'elegant-rose' | 'soft-mint' | 'lavender-dream' | 'warm-caramel';
export type FontSize = 'small' | 'medium' | 'large';
export type AIStyle = 'casual' | 'standard' | 'scientific';
export type AILength = 'detailed' | 'standard' | 'concise';

interface SettingsState {
  theme: Theme;
  fontSize: FontSize;
  aiStyle: AIStyle;
  aiLength: AILength;
  setTheme: (theme: Theme) => void;
  setFontSize: (size: FontSize) => void;
  setAIStyle: (style: AIStyle) => void;
  setAILength: (length: AILength) => void;
}

export const useSettingsStore = create<SettingsState>()(
  persist(
    (set) => ({
      theme: 'elegant-rose',
      fontSize: 'medium',
      aiStyle: 'standard',
      aiLength: 'concise',
      setTheme: (theme) => set({ theme }),
      setFontSize: (fontSize) => set({ fontSize }),
      setAIStyle: (aiStyle) => set({ aiStyle }),
      setAILength: (aiLength) => set({ aiLength }),
    }),
    {
      name: 'user-settings',
    }
  )
);
```

### 2. Header组件 (components/layout/header.tsx)

```typescript
'use client';

import Image from 'next/image';
import Link from 'next/link';
import { Settings, Info, HelpCircle, Menu } from 'lucide-react';
import { Button } from '@/components/ui/button';
import { SettingsPanel } from './settings-panel';
import { useState } from 'react';

export function Header() {
  const [settingsOpen, setSettingsOpen] = useState(false);
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);

  return (
    <header className="sticky top-0 z-50 w-full border-b bg-background/95 backdrop-blur supports-[backdrop-filter]:bg-background/60">
      <div className="container flex h-16 items-center justify-between px-4">
        {/* Logo & Title */}
        <Link href="/" className="flex items-center gap-3">
          <Image 
            src="/logo.png" 
            alt="Logo" 
            width={40} 
            height={40}
            className="h-10 w-auto"
          />
          <h1 className="hidden text-lg font-medium sm:block">
            美容注射的艺术与生活美学
          </h1>
          <h1 className="text-base font-medium sm:hidden">
            美学之艺
          </h1>
        </Link>

        {/* Desktop Navigation */}
        <nav className="hidden items-center gap-2 md:flex">
          <Button variant="ghost" size="icon" asChild>
            <Link href="/guide">
              <HelpCircle className="h-5 w-5" />
              <span className="sr-only">使用说明</span>
            </Link>
          </Button>
          <Button variant="ghost" size="icon" asChild>
            <Link href="/about">
              <Info className="h-5 w-5" />
              <span className="sr-only">关于</span>
            </Link>
          </Button>
          <Button 
            variant="ghost" 
            size="icon"
            onClick={() => setSettingsOpen(true)}
          >
            <Settings className="h-5 w-5" />
            <span className="sr-only">设置</span>
          </Button>
        </nav>

        {/* Mobile Menu Button */}
        <Button 
          variant="ghost" 
          size="icon"
          className="md:hidden"
          onClick={() => setMobileMenuOpen(!mobileMenuOpen)}
        >
          <Menu className="h-5 w-5" />
        </Button>
      </div>

      {/* Settings Panel */}
      <SettingsPanel 
        open={settingsOpen} 
        onOpenChange={setSettingsOpen} 
      />
    </header>
  );
}
```

### 3. Footer组件 (components/layout/footer.tsx)

```typescript
import Image from 'next/image';
import Link from 'next/link';

export function Footer() {
  return (
    <footer className="border-t bg-muted/50">
      <div className="container px-4 py-8">
        {/* Main Navigation */}
        <nav className="mb-8 grid grid-cols-2 gap-4 md:grid-cols-4">
          <Link href="/" className="text-sm hover:underline">首页</Link>
          <Link href="/chapters" className="text-sm hover:underline">章节浏览</Link>
          <Link href="/ai-chat" className="text-sm hover:underline">AI对话</Link>
          <Link href="/image-gen" className="text-sm hover:underline">图像生成</Link>
        </nav>

        {/* Company Info */}
        <div className="mb-6 flex flex-col items-center gap-4 md:flex-row md:justify-between">
          <div className="text-center text-sm md:text-left">
            <p className="font-medium">重庆联合丽格第五医疗美容医院</p>
            <p className="text-muted-foreground">地址：重庆市渝中区临江支路28号</p>
          </div>
          
          {/* QR Code */}
          <Link 
            href="https://work.weixin.qq.com/kfid/kfcfc2a809493f31e8f"
            target="_blank"
            rel="noopener noreferrer"
            className="flex flex-col items-center gap-2"
          >
            <Image 
              src="/images/consultant.png"
              alt="联系二维码"
              width={120}
              height={120}
              className="rounded-lg border"
            />
            <span className="text-xs text-muted-foreground">扫码咨询</span>
          </Link>
        </div>

        {/* Registration Info */}
        <div className="border-t pt-4 text-center text-xs text-muted-foreground/60">
          <p className="mb-1">
            <Link 
              href="https://beian.miit.gov.cn/" 
              target="_blank"
              className="hover:underline"
            >
              渝ICP备15004871号
            </Link>
            {' | '}
            <Link 
              href="http://www.beian.gov.cn/portal/registerSystemInfo"
              target="_blank"
              className="hover:underline"
            >
              渝公网安备 50010302001456号
            </Link>
          </p>
          <p>
            电子邮件：
            <a href="mailto:bccsw@cqlhlg.work" className="hover:underline">
              bccsw@cqlhlg.work
            </a>
            {' | '}
            联系电话：
            <a href="tel:023-68726872" className="hover:underline">
              023-68726872
            </a>
          </p>
        </div>
      </div>
    </footer>
  );
}
```

### 4. AI Chat API (app/api/ai/chat/route.ts)

```typescript
import { OpenAI } from 'openai';
import { OpenAIStream, StreamingTextResponse } from 'ai';

// 初始化OpenAI客户端
const openai = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY,
});

export const runtime = 'edge';

export async function POST(req: Request) {
  try {
    const { messages, settings } = await req.json();

    // 根据设置调整系统提示词
    const systemPrompt = getSystemPrompt(settings);

    const response = await openai.chat.completions.create({
      model: 'gpt-4-turbo-preview',
      stream: true,
      messages: [
        { role: 'system', content: systemPrompt },
        ...messages,
      ],
      temperature: settings.aiStyle === 'casual' ? 0.9 : 
                   settings.aiStyle === 'scientific' ? 0.3 : 0.7,
      max_tokens: settings.aiLength === 'detailed' ? 2000 :
                  settings.aiLength === 'concise' ? 500 : 1000,
    });

    // 使用Vercel AI SDK处理流
    const stream = OpenAIStream(response);
    return new StreamingTextResponse(stream);
    
  } catch (error) {
    console.error('AI Chat Error:', error);
    return new Response('Error processing request', { status: 500 });
  }
}

function getSystemPrompt(settings: any): string {
  const basePrompt = `你是一个医美科普助手，基于《美容注射的艺术与生活美学》这本书的内容...`;
  
  if (settings.aiStyle === 'casual') {
    return basePrompt + '\n请用轻松幽默的方式回答。';
  } else if (settings.aiStyle === 'scientific') {
    return basePrompt + '\n请用科学严谨的方式回答，引用相关研究和数据。';
  }
  
  return basePrompt + '\n请用标准日常的方式回答。';
}
```

---

## 🧪 测试命令

```bash
# 运行开发服务器
npm run dev

# 构建生产版本
npm run build

# 本地预览生产版本
npm run start

# 运行测试
npm run test

# 类型检查
npm run type-check

# Lint检查
npm run lint
```

---

## 📱 iOS测试清单

### Safari开发者工具
```bash
# 在Mac上启用Safari开发菜单
# Safari -> 偏好设置 -> 高级 -> 勾选"在菜单栏中显示开发菜单"

# 连接iOS设备调试
# 开发 -> [您的iPhone] -> [网页]
```

### 关键测试点
- [ ] AI对话流式输出是否正常
- [ ] 文本选择是否触发划词AI
- [ ] 图片上传/生成是否成功
- [ ] 触摸手势是否流畅
- [ ] 页面滚动是否卡顿
- [ ] 主题切换是否生效
- [ ] 设置是否正确保存

---

## 🚀 部署到Vercel

```bash
# 安装Vercel CLI
npm i -g vercel

# 登录
vercel login

# 部署
vercel

# 部署到生产环境
vercel --prod
```

### 环境变量配置
在Vercel Dashboard中设置：
```
OPENAI_API_KEY=your_openai_api_key
NEXT_PUBLIC_SITE_URL=https://your-domain.com
```

---

## 📚 参考资源

### 官方文档
- [Next.js 文档](https://nextjs.org/docs)
- [TailwindCSS 文档](https://tailwindcss.com/docs)
- [shadcn/ui 文档](https://ui.shadcn.com)
- [Framer Motion 文档](https://www.framer.com/motion/)

### 设计资源
- [Remix Icon](https://remixicon.com/)
- [Phosphor Icons](https://phosphoricons.com/)
- [Lucide Icons](https://lucide.dev/)

### AI集成
- [Vercel AI SDK](https://sdk.vercel.ai/docs)
- [OpenAI API 文档](https://platform.openai.com/docs)

---

**准备就绪，开始构建吧！** 🚀
