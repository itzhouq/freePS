# FreePS SEO 优化与 AdSense 审核设计方案

**日期**: 2025-02-19
**方案**: 方案 B - 标准 SEO 优化
**目标**: Vercel 部署 + Google AdSense 审核通过 + 双语 SEO

---

## 1. 项目概述

FreePS 是一个基于 miniPaint 的在线图像编辑器，需要部署到 Vercel 并通过 Google AdSense 审核，同时面向中英文双语用户市场。

**关键需求**:
- 使用 Vercel 提供的 `.vercel.app` 子域名
- 面向双语市场（中英文）
- 通过 Google AdSense 审核
- 全面覆盖关键词（通用、长尾、功能性）

---

## 2. 新增页面结构

```
/
├── index.html          (主页 - 现有，需优化)
├── about.html          (关于我们 - 新增)
├── features.html       (功能介绍 - 新增)
├── faq.html            (常见问题 - 新增)
├── tutorials.html      (教程指南 - 新增)
├── privacy.html        (隐私政策 - AdSense 必需)
├── terms.html          (服务条款 - AdSense 必需)
├── robots.txt          (SEO 必需)
├── sitemap.xml         (SEO 必需)
├── vercel.json         (Vercel 配置)
└── /images/
```

---

## 3. SEO 元素优化

### 3.1 index.html 优化

| 项目 | 当前状态 | 优化目标 |
|------|----------|----------|
| Canonical URL | `freeps.org` | 更新为 Vercel 子域名 |
| Open Graph 图片 | 缺失 | 添加 `og:image` |
| hreflang 标签 | 缺失 | 添加中英文版本 |
| Title | 基础 | 优化关键词 |
| Description | 基础 | 更具吸引力 |
| 结构化数据 | 缺失 | 添加 JSON-LD |

### 3.2 robots.txt

```
User-agent: *
Allow: /
Sitemap: https://your-project.vercel.app/sitemap.xml
```

### 3.3 sitemap.xml

包含所有页面 URL，设置合理的 priority 和 changefreq。

---

## 4. AdSense 合规页面

### 4.1 Privacy Policy (隐私政策)

- 收集的数据类型（使用情况数据、Cookie）
- Google AdSense 和 Google Analytics 使用说明
- 用户权利（访问、删除数据）
- 联系方式
- Cookie 政策

### 4.2 Terms of Service (服务条款)

- 服务描述
- 用户责任
- 知识产权说明
- 免责声明
- 服务变更条款

### 4.3 FAQ 页面

- 与 AdSense 相关问题
- 工具使用问题
- 隐私和数据问题
- 技术支持问题

---

## 5. 性能优化 (Core Web Vitals)

### 5.1 Bundle.js 加载优化

- 添加 `defer` 属性替代 `async`
- 确保准备好后再执行

### 5.2 图片优化

- PNG 图标转换为 WebP 格式
- 添加 `width` 和 `height` 属性
- 使用 `loading="lazy"` 延迟加载

### 5.3 关键 CSS 内联

- 提取首屏关键 CSS
- 减少 FCP 时间

### 5.4 资源压缩

- 确保 `bundle.js.gz` 正确使用
- Vercel 自动处理 Brotli 压缩

---

## 6. 双语支持实现

### 6.1 URL 结构

- `/` - 默认英文版本
- `?lang=zh` - 中文版本

### 6.2 语言切换实现

- 通过 URL 参数或 localStorage 存储语言偏好
- JavaScript 动态切换页面文本内容
- 每个页面维护中英文文本映射

### 6.3 hreflang 标签

```html
<link rel="alternate" hreflang="en" href="https://your-project.vercel.app/" />
<link rel="alternate" hreflang="zh" href="https://your-project.vercel.app/?lang=zh" />
<link rel="alternate" hreflang="x-default" href="https://your-project.vercel.app/" />
```

### 6.4 语言切换按钮

- 位于导航栏右上角
- 显示 "EN / 中文" 切换选项

---

## 7. Vercel 部署配置

### 7.1 vercel.json

```json
{
  "cleanUrls": true,
  "trailingSlash": false,
  "headers": [
    {
      "source": "/images/(.*)",
      "headers": [
        {
          "key": "Cache-Control",
          "value": "public, max-age=31536000, immutable"
        }
      ]
    },
    {
      "source": "/(.*)",
      "headers": [
        {
          "key": "X-Content-Type-Options",
          "value": "nosniff"
        },
        {
          "key": "X-Frame-Options",
          "value": "DENY"
        }
      ]
    }
  ],
  "redirects": [
    {
      "source": "/home",
      "destination": "/",
      "permanent": true
    }
  ]
}
```

### 7.2 部署步骤

1. 连接 GitHub 仓库到 Vercel
2. 配置构建命令（留空，静态文件）
3. 设置输出目录为 `/`
4. 部署完成后获取 `.vercel.app` 域名
5. 更新代码中的所有 URL 引用

---

## 8. 关键词策略

### 8.1 通用关键词

- online photo editor
- free photoshop
- 在线图片编辑器

### 8.2 长尾关键词

- online photo editor with layers
- 免费在线修图工具 无需注册

### 8.3 功能性关键词

- online image resize
- remove background online
- 图片裁剪工具

---

## 9. 预期成果

- **SEO**: 提升搜索引擎排名，覆盖目标关键词
- **AdSense**: 通过审核并开始变现
- **用户体验**: 双语支持，性能优化
- **部署**: Vercel 稳定托管

---

## 10. 下一步

创建详细的实现计划，包括：
1. 文件创建顺序
2. 代码实现细节
3. 测试验证步骤
4. 部署流程
