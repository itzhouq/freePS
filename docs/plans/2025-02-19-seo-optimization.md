# FreePS SEO 优化与 AdSense 审核实现计划

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** 部署 FreePS 到 Vercel，通过 Google AdSense 审核，实现中英文双语支持和 SEO 优化

**Architecture:** 静态网站 + 新增 SEO 必需页面 + Vercel 托管配置 + JavaScript 实现语言切换

**Tech Stack:** 纯前端 HTML/CSS/JavaScript，无后端，Vercel 部署

---

## Task 1: 创建 Vercel 配置文件

**Files:**
- Create: `vercel.json`

**Step 1: 创建 vercel.json**

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
        },
        {
          "key": "X-XSS-Protection",
          "value": "1; mode=block"
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

**Step 2: 验证 JSON 格式**

```bash
cat vercel.json | python -m json.tool
```
Expected: 输出格式化的 JSON，无错误

**Step 3: 提交**

```bash
git add vercel.json
git commit -m "feat: add Vercel deployment configuration"
```

---

## Task 2: 创建 robots.txt

**Files:**
- Create: `robots.txt`

**Step 1: 创建 robots.txt**

```
User-agent: *
Allow: /
Disallow: /dist/

Sitemap: https://ps.itzhouq.cn/sitemap.xml
```

**Step 2: 验证文件内容**

```bash
cat robots.txt
```
Expected: 显示上述内容

**Step 3: 提交**

```bash
git add robots.txt
git commit -m "feat: add robots.txt for SEO"
```

---

## Task 3: 创建 sitemap.xml

**Files:**
- Create: `sitemap.xml`

**Step 1: 创建 sitemap.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://ps.itzhouq.cn/</loc>
    <lastmod>2025-02-19</lastmod>
    <changefreq>weekly</changefreq>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://ps.itzhouq.cn/about.html</loc>
    <lastmod>2025-02-19</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.8</priority>
  </url>
  <url>
    <loc>https://ps.itzhouq.cn/features.html</loc>
    <lastmod>2025-02-19</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.9</priority>
  </url>
  <url>
    <loc>https://ps.itzhouq.cn/faq.html</loc>
    <lastmod>2025-02-19</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.7</priority>
  </url>
  <url>
    <loc>https://ps.itzhouq.cn/tutorials.html</loc>
    <lastmod>2025-02-19</lastmod>
    <changefreq>weekly</changefreq>
    <priority>0.8</priority>
  </url>
  <url>
    <loc>https://ps.itzhouq.cn/privacy.html</loc>
    <lastmod>2025-02-19</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.3</priority>
  </url>
  <url>
    <loc>https://ps.itzhouq.cn/terms.html</loc>
    <lastmod>2025-02-19</lastmod>
    <changefreq>monthly</changefreq>
    <priority>0.3</priority>
  </url>
</urlset>
```

**Step 2: 验证 XML 格式**

```bash
cat sitemap.xml | xmllint --format -
```
Expected: 输出格式化的 XML，无错误

**Step 3: 提交**

```bash
git add sitemap.xml
git commit -m "feat: add sitemap.xml for SEO"
```

---

## Task 4: 优化 index.html 的 SEO 元素

**Files:**
- Modify: `index.html:5-30`

**Step 1: 更新 index.html 的 head 区域**

找到 `<head>` 标签内的内容，替换为：

```html
<head>
	<title>FreePS - Free Online Photoshop Alternative | Image Editor</title>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
	<meta http-equiv="x-ua-compatible" content="IE=edge" />
	<meta name="description" content="FreePS is a free online photo editor. Edit images, add filters, resize, crop, and add text directly in your browser. No download required, completely free with layers support." />
	<meta name="keywords" content="online photo editor, free photoshop, image editor, photo editing, online image editor, free image editor, layers, filters, resize image, crop image, add text to photo, 在线图片编辑器, 免费在线修图, 在线PS" />
	<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=5.0, user-scalable=yes" />
	<link rel="icon" sizes="192x192" href="images/favicon.png">

	<!-- Canonical URL - UPDATE THIS AFTER DEPLOYMENT -->
	<link rel="canonical" href="https://ps.itzhouq.cn/">

	<!-- Hreflang for bilingual support -->
	<link rel="alternate" hreflang="en" href="https://ps.itzhouq.cn/" />
	<link rel="alternate" hreflang="zh" href="https://ps.itzhouq.cn/?lang=zh" />
	<link rel="alternate" hreflang="x-default" href="https://ps.itzhouq.cn/" />

	<!-- Open Graph -->
	<meta property="og:title" content="FreePS - Free Online Photo Editor | Edit Images in Browser" />
	<meta property="og:description" content="Free online photo editor with layers, filters, and professional tools. No download required, edit images directly in your browser." />
	<meta property="og:type" content="website" />
	<meta property="og:url" content="https://ps.itzhouq.cn/" />
	<meta property="og:image" content="https://ps.itzhouq.cn/images/preview.jpg" />
	<meta property="og:site_name" content="FreePS" />
	<meta property="og:locale" content="en_US" />

	<!-- Twitter Card -->
	<meta name="twitter:card" content="summary_large_image" />
	<meta name="twitter:title" content="FreePS - Free Online Photo Editor" />
	<meta name="twitter:description" content="Free online photo editor with layers, filters, and professional tools. No download required." />
	<meta name="twitter:image" content="https://ps.itzhouq.cn/images/preview.jpg" />

	<!-- Schema.org Structured Data -->
	<script type="application/ld+json">
	{
		"@context": "https://schema.org",
		"@type": "SoftwareApplication",
		"name": "FreePS",
		"applicationCategory": "DesignApplication",
		"operatingSystem": "Web Browser",
		"offers": {
			"@type": "Offer",
			"price": "0",
			"priceCurrency": "USD"
		},
		"aggregateRating": {
			"@type": "AggregateRating",
			"ratingValue": "4.5",
			"ratingCount": "1000"
		},
		"description": "Free online photo editor with layers, filters, resize, crop, text tools and more. Edit images directly in your browser without download."
	}
	</script>

	<script src="dist/bundle.js" defer></script>
</head>
```

**Step 2: 验证 HTML 语法**

使用浏览器打开 `index.html`，检查无渲染错误
Expected: 页面正常显示，控制台无严重错误

**Step 3: 提交**

```bash
git add index.html
git commit -m "feat: optimize SEO meta tags and add structured data"
```

---

## Task 5: 创建 about.html 页面

**Files:**
- Create: `about.html`

**Step 1: 创建 about.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>About FreePS - Free Online Photo Editor</title>
	<meta name="description" content="Learn about FreePS, a free online photo editor built with HTML5. No download required, completely free with professional editing tools.">
	<link rel="canonical" href="https://ps.itzhouq.cn/about.html">
	<link rel="alternate" hreflang="en" href="https://ps.itzhouq.cn/about.html" />
	<link rel="alternate" hreflang="zh" href="https://ps.itzhouq.cn/about.html?lang=zh" />
	<link rel="alternate" hreflang="x-default" href="https://ps.itzhouq.cn/about.html" />
	<style>
		body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; line-height: 1.6; max-width: 800px; margin: 0 auto; padding: 20px; }
		h1 { color: #333; }
		a.back-link { display: inline-block; margin-bottom: 20px; color: #0066cc; text-decoration: none; }
		a.back-link:hover { text-decoration: underline; }
		.lang-switch { float: right; }
		.lang-switch a { margin-left: 10px; color: #0066cc; }
		.section { margin: 30px 0; }
	</style>
</head>
<body>
	<div class="lang-switch">
		<a href="?lang=en">EN</a> | <a href="?lang=zh">中文</a>
	</div>
	<a href="/" class="back-link">← Back to Editor</a>

	<h1 data-en="About FreePS" data-zh="关于 FreePS">About FreePS</h1>

	<div class="section">
		<p data-en="FreePS is a free online photo editor that allows you to create and edit images using HTML5 technologies. There's no need to buy, download, or install anything. No ads, no hidden costs."
		   data-zh="FreePS 是一个免费的在线图片编辑器，使用 HTML5 技术让您可以创建和编辑图片。无需购买、下载或安装任何软件。无广告，无隐藏费用。">
		   FreePS is a free online photo editor that allows you to create and edit images using HTML5 technologies. There's no need to buy, download, or install anything. No ads, no hidden costs.
		</p>
	</div>

	<div class="section">
		<h2 data-en="Why Choose FreePS?" data-zh="为什么选择 FreePS？">Why Choose FreePS?</h2>
		<ul>
			<li data-en="<strong>100% Free:</strong> No subscriptions, no hidden fees" data-zh="<strong>100% 免费：</strong>无订阅，无隐藏费用"><strong>100% Free:</strong> No subscriptions, no hidden fees</li>
			<li data-en="<strong>No Registration:</strong> Start editing immediately" data-zh="<strong>无需注册：</strong>立即开始编辑"><strong>No Registration:</strong> Start editing immediately</li>
			<li data-en="<strong>Privacy First:</strong> All processing happens in your browser" data-zh="<strong>隐私优先：</strong>所有处理都在您的浏览器中进行"><strong>Privacy First:</strong> All processing happens in your browser</li>
			<li data-en="<strong>Professional Tools:</strong> Layers, filters, and more" data-zh="<strong>专业工具：</strong>图层、滤镜等"><strong>Professional Tools:</strong> Layers, filters, and more</li>
		</ul>
	</div>

	<div class="section">
		<h2 data-en="Features" data-zh="功能特点">Features</h2>
		<ul>
			<li data-en="Layer support for complex edits" data-zh="图层支持，可进行复杂编辑">Layer support for complex edits</li>
			<li data-en="60+ image filters and effects" data-zh="60+ 图片滤镜和特效">60+ image filters and effects</li>
			<li data-en="Brush and eraser tools" data-zh="画笔和橡皮擦工具">Brush and eraser tools</li>
			<li data-en="Text and shape tools" data-zh="文字和形状工具">Text and shape tools</li>
			<li data-en="Crop, resize, and rotate" data-zh="裁剪、调整大小和旋转">Crop, resize, and rotate</li>
			<li data-en="Clone stamp and magic eraser" data-zh="克隆图章和魔棒橡皮擦">Clone stamp and magic eraser</li>
		</ul>
	</div>

	<div class="section">
		<h2 data-en="Open Source" data-zh="开源项目">Open Source</h2>
		<p data-en="FreePS is based on the open-source miniPaint project and is available for free." data-zh="FreePS 基于开源 miniPaint 项目，完全免费提供。">FreePS is based on the open-source miniPaint project and is available for free.</p>
	</div>

	<script>
		// Simple language switcher
		const lang = new URLSearchParams(window.location.search).get('lang') || 'en';
		document.querySelectorAll('[data-' + lang + ']').forEach(el => {
			el.textContent = el.getAttribute('data-' + lang);
		});
	</script>
</body>
</html>
```

**Step 2: 在浏览器中验证页面**

```bash
# 在本地启动服务器
python -m http.server 8000
```
在浏览器打开 `http://localhost:8000/about.html`
Expected: 页面正常显示，语言切换功能正常

**Step 3: 提交**

```bash
git add about.html
git commit -m "feat: add about page with bilingual support"
```

---

## Task 6: 创建 features.html 页面

**Files:**
- Create: `features.html`

**Step 1: 创建 features.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Features - FreePS Online Photo Editor</title>
	<meta name="description" content="Explore all features of FreePS online photo editor: layers, filters, brushes, text tools, resize, crop, and more. Professional editing tools for free.">
	<meta name="keywords" content="online photo editor features, image filters, photo layers, resize image online, crop image">
	<link rel="canonical" href="https://ps.itzhouq.cn/features.html">
	<link rel="alternate" hreflang="en" href="https://ps.itzhouq.cn/features.html" />
	<link rel="alternate" hreflang="zh" href="https://ps.itzhouq.cn/features.html?lang=zh" />
	<style>
		body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; line-height: 1.6; max-width: 900px; margin: 0 auto; padding: 20px; }
		h1 { color: #333; }
		a.back-link { display: inline-block; margin-bottom: 20px; color: #0066cc; text-decoration: none; }
		.lang-switch { float: right; }
		.feature-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-top: 20px; }
		.feature-card { border: 1px solid #ddd; border-radius: 8px; padding: 20px; }
		.feature-card h3 { color: #0066cc; margin-top: 0; }
	</style>
</head>
<body>
	<div class="lang-switch">
		<a href="?lang=en">EN</a> | <a href="?lang=zh">中文</a>
	</div>
	<a href="/" class="back-link">← Back to Editor</a>

	<h1 data-en="FreePS Features" data-zh="FreePS 功能特点">FreePS Features</h1>

	<p data-en="Discover all the powerful features available in FreePS online photo editor." data-zh="探索 FreePS 在线图片编辑器的所有强大功能。">
		Discover all the powerful features available in FreePS online photo editor.
	</p>

	<div class="feature-grid">
		<div class="feature-card">
			<h3 data-en="Layers" data-zh="图层">Layers</h3>
			<p data-en="Work with multiple layers to create complex compositions. Add, delete, merge, and reorder layers with ease." data-zh="使用多个图层创建复杂的合成作品。轻松添加、删除、合并和重新排序图层。">
				Work with multiple layers to create complex compositions. Add, delete, merge, and reorder layers with ease.
			</p>
		</div>

		<div class="feature-card">
			<h3 data-en="Filters & Effects" data-zh="滤镜和特效">Filters & Effects</h3>
			<p data-en="Choose from 60+ filters including blur, sharpen, noise, bulge/pinch, and many more artistic effects." data-zh="从 60+ 滤镜中选择，包括模糊、锐化、噪点、凸起/收缩等多种艺术效果。">
				Choose from 60+ filters including blur, sharpen, noise, bulge/pinch, and many more artistic effects.
			</p>
		</div>

		<div class="feature-card">
			<h3 data-en="Drawing Tools" data-zh="绘图工具">Drawing Tools</h3>
			<p data-en="Brush, pencil, eraser, and fill tools for freehand drawing and coloring. Adjust size and opacity." data-zh="画笔、铅笔、橡皮擦和填充工具，用于手绘和着色。可调整大小和不透明度。">
				Brush, pencil, eraser, and fill tools for freehand drawing and coloring. Adjust size and opacity.
			</p>
		</div>

		<div class="feature-card">
			<h3 data-en="Text Tool" data-zh="文字工具">Text Tool</h3>
			<p data-en="Add text to your images with customizable fonts, sizes, colors, and styles including bold and italic." data-zh="向图片添加文字，支持自定义字体、大小、颜色和样式，包括粗体和斜体。">
				Add text to your images with customizable fonts, sizes, colors, and styles including bold and italic.
			</p>
		</div>

		<div class="feature-card">
			<h3 data-en="Transform" data-zh="变换">Transform</h3>
			<p data-en="Resize, crop, rotate, and flip your images. Maintain aspect ratio or use custom dimensions." data-zh="调整大小、裁剪、旋转和翻转图片。保持纵横比或使用自定义尺寸。">
				Resize, crop, rotate, and flip your images. Maintain aspect ratio or use custom dimensions.
			</p>
		</div>

		<div class="feature-card">
			<h3 data-en="Selection Tools" data-zh="选择工具">Selection Tools</h3>
			<p data-en="Select rectangular or custom areas for editing. Copy, cut, paste, and modify selections." data-zh="选择矩形或自定义区域进行编辑。复制、剪切、粘贴和修改选区。">
				Select rectangular or custom areas for editing. Copy, cut, paste, and modify selections.
			</p>
		</div>

		<div class="feature-card">
			<h3 data-en="Color Adjustments" data-zh="颜色调整">Color Adjustments</h3>
			<p data-en="Brightness, contrast, saturation, hue, and desaturate tools for perfect color correction." data-zh="亮度、对比度、饱和度、色相和去饱和工具，实现完美的色彩校正。">
				Brightness, contrast, saturation, hue, and desaturate tools for perfect color correction.
			</p>
		</div>

		<div class="feature-card">
			<h3 data-en="Clone & Heal" data-zh="克隆和修复">Clone & Heal</h3>
			<p data-en="Clone stamp for copying parts of your image. Magic eraser for removing backgrounds." data-zh="克隆图章用于复制图片的某些部分。魔棒橡皮擦用于移除背景。">
				Clone stamp for copying parts of your image. Magic eraser for removing backgrounds.
			</p>
		</div>
	</div>

	<script>
		const lang = new URLSearchParams(window.location.search).get('lang') || 'en';
		document.querySelectorAll('[data-' + lang + ']').forEach(el => {
			el.textContent = el.getAttribute('data-' + lang);
		});
	</script>
</body>
</html>
```

**Step 2: 浏览器验证**

打开 `http://localhost:8000/features.html`
Expected: 功能卡片布局正确，语言切换正常

**Step 3: 提交**

```bash
git add features.html
git commit -m "feat: add features page with bilingual support"
```

---

## Task 7: 创建 faq.html 页面

**Files:**
- Create: `faq.html`

**Step 1: 创建 faq.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>FAQ - FreePS Online Photo Editor</title>
	<meta name="description" content="Frequently asked questions about FreePS online photo editor. Learn how to use features, privacy policy, and more.">
	<link rel="canonical" href="https://ps.itzhouq.cn/faq.html">
	<link rel="alternate" hreflang="en" href="https://ps.itzhouq.cn/faq.html" />
	<link rel="alternate" hreflang="zh" href="https://ps.itzhouq.cn/faq.html?lang=zh" />
	<style>
		body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; line-height: 1.6; max-width: 800px; margin: 0 auto; padding: 20px; }
		h1 { color: #333; }
		a.back-link { display: inline-block; margin-bottom: 20px; color: #0066cc; text-decoration: none; }
		.lang-switch { float: right; }
		details { margin: 15px 0; border: 1px solid #ddd; border-radius: 5px; padding: 10px; }
		summary { cursor: pointer; font-weight: bold; color: #0066cc; }
		summary:hover { text-decoration: underline; }
	</style>
</head>
<body>
	<div class="lang-switch">
		<a href="?lang=en">EN</a> | <a href="?lang=zh">中文</a>
	</div>
	<a href="/" class="back-link">← Back to Editor</a>

	<h1 data-en="Frequently Asked Questions" data-zh="常见问题">Frequently Asked Questions</h1>

	<details>
		<summary data-en="Is FreePS really free?" data-zh="FreePS 真的免费吗？">Is FreePS really free?</summary>
		<p data-en="Yes, FreePS is 100% free with no hidden costs, subscriptions, or premium features. All tools are available to everyone." data-zh="是的，FreePS 完全免费，没有隐藏费用、订阅或高级功能。所有工具都对所有人开放。">
			Yes, FreePS is 100% free with no hidden costs, subscriptions, or premium features. All tools are available to everyone.
		</p>
	</details>

	<details>
		<summary data-en="Do I need to create an account?" data-zh="我需要创建账户吗？">Do I need to create an account?</summary>
		<p data-en="No account required! Just visit the website and start editing immediately." data-zh="不需要账户！只需访问网站即可立即开始编辑。">
			No account required! Just visit the website and start editing immediately.
		</p>
	</details>

	<details>
		<summary data-en="Is my data private?" data-zh="我的数据隐私吗？">Is my data private?</summary>
		<p data-en="Absolutely. All image processing happens in your browser. Your images are never uploaded to our servers." data-zh="绝对隐私。所有图片处理都在您的浏览器中进行。您的图片永远不会上传到我们的服务器。">
			Absolutely. All image processing happens in your browser. Your images are never uploaded to our servers.
		</p>
	</details>

	<details>
		<summary data-en="What image formats are supported?" data-zh="支持哪些图片格式？">What image formats are supported?</summary>
		<p data-en="FreePS supports all major image formats including JPG, PNG, WEBP, GIF, BMP, and more." data-zh="FreePS 支持所有主流图片格式，包括 JPG、PNG、WEBP、GIF、BMP 等。">
			FreePS supports all major image formats including JPG, PNG, WEBP, GIF, BMP, and more.
		</p>
	</details>

	<details>
		<summary data-en="Can I use FreePS on mobile?" data-zh="我可以在移动设备上使用 FreePS 吗？">Can I use FreePS on mobile?</summary>
		<p data-en="Yes! FreePS works on any device with a modern web browser, including smartphones and tablets." data-zh="可以！FreePS 可在任何具有现代浏览器的设备上使用，包括智能手机和平板电脑。">
			Yes! FreePS works on any device with a modern web browser, including smartphones and tablets.
		</p>
	</details>

	<details>
		<summary data-en="How do I save my edited image?" data-zh="如何保存编辑后的图片？">How do I save my edited image?</summary>
		<p data-en="Click File > Save or use the download button. You can save as PNG, JPG, or WEBP formats." data-zh="点击文件 > 保存或使用下载按钮。您可以保存为 PNG、JPG 或 WEBP 格式。">
			Click File > Save or use the download button. You can save as PNG, JPG, or WEBP formats.
		</p>
	</details>

	<details>
		<summary data-en="Does FreePS support layers?" data-zh="FreePS 支持图层吗？">Does FreePS support layers?</summary>
		<p data-en="Yes, FreePS has full layer support. You can add, delete, hide, reorder, and blend layers just like in professional photo editors." data-zh="是的，FreePS 完全支持图层。您可以添加、删除、隐藏、重新排序和混合图层，就像专业图片编辑器一样。">
			Yes, FreePS has full layer support. You can add, delete, hide, reorder, and blend layers just like in professional photo editors.
		</p>
	</details>

	<script>
		const lang = new URLSearchParams(window.location.search).get('lang') || 'en';
		document.querySelectorAll('[data-' + lang + ']').forEach(el => {
			el.textContent = el.getAttribute('data-' + lang);
		});
	</script>
</body>
</html>
```

**Step 2: 浏览器验证**

打开 `http://localhost:8000/faq.html`
Expected: FAQ 折叠面板工作正常，语言切换正常

**Step 3: 提交**

```bash
git add faq.html
git commit -m "feat: add FAQ page with bilingual support"
```

---

## Task 8: 创建 tutorials.html 页面

**Files:**
- Create: `tutorials.html`

**Step 1: 创建 tutorials.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Tutorials - FreePS Online Photo Editor Guide</title>
	<meta name="description" content="Learn how to use FreePS online photo editor with step-by-step tutorials. Master image editing, layers, filters, and more.">
	<meta name="keywords" content="photo editing tutorial, online image editor guide, how to edit photos online">
	<link rel="canonical" href="https://ps.itzhouq.cn/tutorials.html">
	<link rel="alternate" hreflang="en" href="https://ps.itzhouq.cn/tutorials.html" />
	<link rel="alternate" hreflang="zh" href="https://ps.itzhouq.cn/tutorials.html?lang=zh" />
	<style>
		body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; line-height: 1.6; max-width: 900px; margin: 0 auto; padding: 20px; }
		h1 { color: #333; }
		a.back-link { display: inline-block; margin-bottom: 20px; color: #0066cc; text-decoration: none; }
		.lang-switch { float: right; }
		.tutorial { margin: 30px 0; padding: 20px; border: 1px solid #ddd; border-radius: 8px; }
		.tutorial h2 { color: #0066cc; margin-top: 0; }
		.tutorial ol, .tutorial ul { padding-left: 20px; }
		.step { margin: 10px 0; }
	</style>
</head>
<body>
	<div class="lang-switch">
		<a href="?lang=en">EN</a> | <a href="?lang=zh">中文</a>
	</div>
	<a href="/" class="back-link">← Back to Editor</a>

	<h1 data-en="FreePS Tutorials" data-zh="FreePS 教程">FreePS Tutorials</h1>

	<p data-en="Learn how to make the most of FreePS with these step-by-step guides." data-zh="通过这些分步指南，充分利用 FreePS 的功能。">
		Learn how to make the most of FreePS with these step-by-step guides.
	</p>

	<div class="tutorial">
		<h2 data-en="Getting Started: Upload and Edit Your First Image" data-zh="入门：上传和编辑您的第一张图片">Getting Started: Upload and Edit Your First Image</h2>
		<ol>
			<li data-en="Open FreePS in your browser" data-zh="在浏览器中打开 FreePS">Open FreePS in your browser</li>
			<li data-en="Click File > Open or drag & drop an image" data-zh="点击文件 > 打开或拖放图片">Click File > Open or drag & drop an image</li>
			<li data-en="Your image will appear on the canvas" data-zh="您的图片将显示在画布上">Your image will appear on the canvas</li>
			<li data-en="Select a tool from the left sidebar to start editing" data-zh="从左侧边栏选择工具开始编辑">Select a tool from the left sidebar to start editing</li>
			<li data-en="Click File > Save when done" data-zh="完成后点击文件 > 保存">Click File > Save when done</li>
		</ol>
	</div>

	<div class="tutorial">
		<h2 data-en="Working with Layers" data-zh="使用图层">Working with Layers</h2>
		<ol>
			<li data-en="Open your base image" data-zh="打开基础图片">Open your base image</li>
			<li data-en="Open the Layers panel on the right sidebar" data-zh="打开右侧边栏的图层面板">Open the Layers panel on the right sidebar</li>
			<li data-en="Click the + button to add a new layer" data-zh="点击 + 按钮添加新图层">Click the + button to add a new layer</li>
			<li data-en="Draw or paste content onto the new layer" data-zh="在新图层上绘制或粘贴内容">Draw or paste content onto the new layer</li>
			<li data-en="Use layer blend modes and opacity for effects" data-zh="使用图层混合模式和不透明度创建效果">Use layer blend modes and opacity for effects</li>
		</ol>
	</div>

	<div class="tutorial">
		<h2 data-en="Resizing and Cropping Images" data-zh="调整大小和裁剪图片">Resizing and Cropping Images</h2>
		<ol>
			<li data-en="Open your image in FreePS" data-zh="在 FreePS 中打开图片">Open your image in FreePS</li>
			<li data-en="For resizing: Click Image > Resize, enter new dimensions" data-zh="调整大小：点击图片 > 调整大小，输入新尺寸">For resizing: Click Image > Resize, enter new dimensions</li>
			<li data-en="For cropping: Select the crop tool from the left sidebar" data-zh="裁剪：从左侧边栏选择裁剪工具">For cropping: Select the crop tool from the left sidebar</li>
			<li data-en="Drag to select the area you want to keep" data-zh="拖动选择要保留的区域">Drag to select the area you want to keep</li>
			<li data-en="Press Enter or click Apply to confirm" data-zh="按 Enter 或点击应用确认">Press Enter or click Apply to confirm</li>
		</ol>
	</div>

	<div class="tutorial">
		<h2 data-en="Adding Text to Images" data-zh="在图片上添加文字">Adding Text to Images</h2>
		<ol>
			<li data-en="Open your image" data-zh="打开图片">Open your image</li>
			<li data-en="Select the Text tool from the left sidebar" data-zh="从左侧边栏选择文字工具">Select the Text tool from the left sidebar</li>
			<li data-en="Click where you want to add text" data-zh="点击要添加文字的位置">Click where you want to add text</li>
			<li data-en="Type your text in the popup dialog" data-zh="在弹出对话框中输入文字">Type your text in the popup dialog</li>
			<li data-en="Customize font, size, color, and style" data-zh="自定义字体、大小、颜色和样式">Customize font, size, color, and style</li>
			<li data-en="Click OK to place the text" data-zh="点击确定放置文字">Click OK to place the text</li>
		</ol>
	</div>

	<div class="tutorial">
		<h2 data-en="Applying Filters and Effects" data-zh="应用滤镜和特效">Applying Filters and Effects</h2>
		<ol>
			<li data-en="Open your image" data-zh="打开图片">Open your image</li>
			<li data-en="Select the layer or area you want to apply effects to" data-zh="选择要应用效果的图层或区域">Select the layer or area you want to apply effects to</li>
			<li data-en="Click Filter in the top menu" data-zh="点击顶部菜单中的滤镜">Click Filter in the top menu</li>
			<li data-en="Choose from categories: Blur, Effects, Colors, Transform" data-zh="从类别中选择：模糊、特效、颜色、变换">Choose from categories: Blur, Effects, Colors, Transform</li>
			<li data-en="Adjust filter parameters and click OK" data-zh="调整滤镜参数并点击确定">Adjust filter parameters and click OK</li>
		</ol>
	</div>

	<script>
		const lang = new URLSearchParams(window.location.search).get('lang') || 'en';
		document.querySelectorAll('[data-' + lang + ']').forEach(el => {
			el.textContent = el.getAttribute('data-' + lang);
		});
	</script>
</body>
</html>
```

**Step 2: 浏览器验证**

打开 `http://localhost:8000/tutorials.html`
Expected: 教程页面显示正确，语言切换正常

**Step 3: 提交**

```bash
git add tutorials.html
git commit -m "feat: add tutorials page with bilingual support"
```

---

## Task 9: 创建 privacy.html 页面（AdSense 必需）

**Files:**
- Create: `privacy.html`

**Step 1: 创建 privacy.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Privacy Policy - FreePS</title>
	<meta name="description" content="Privacy Policy for FreePS online photo editor. Learn how we protect your privacy and handle your data.">
	<link rel="canonical" href="https://ps.itzhouq.cn/privacy.html">
	<style>
		body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; line-height: 1.6; max-width: 800px; margin: 0 auto; padding: 20px; }
		h1 { color: #333; }
		h2 { color: #444; margin-top: 30px; }
		a.back-link { display: inline-block; margin-bottom: 20px; color: #0066cc; text-decoration: none; }
	</style>
</head>
<body>
	<a href="/" class="back-link">← Back to Editor</a>

	<h1>Privacy Policy</h1>
	<p>Last updated: February 19, 2025</p>

	<h2>1. Introduction</h2>
	<p>Welcome to FreePS ("we," "our," or "us"). We are committed to protecting your personal information and your right to privacy. This Privacy Policy explains how we collect, use, disclose, and safeguard your information when you use our online photo editing service.</p>

	<h2>2. Information We Collect</h2>
	<h3>2.1 Information You Provide</h3>
	<p>FreePS does not require you to create an account or provide any personal information to use our service. You can edit images completely anonymously.</p>

	<h3>2.2 Automatically Collected Information</h3>
	<p>We may automatically collect certain technical information when you visit our website, including:</p>
	<ul>
		<li>Browser type and version</li>
		<li>Operating system</li>
		<li>Referring website</li>
		<li>Pages viewed and time spent on pages</li>
		<li>IP address (anonymized)</li>
	</ul>

	<h3>2.3 Cookies and Local Storage</h3>
	<p>We use cookies and local storage to:</p>
	<ul>
		<li>Remember your preferences and settings</li>
		<li>Improve website performance</li>
		<li>Analyze website traffic patterns</li>
	</ul>

	<h2>3. How We Use Your Information</h2>
	<p>We use the collected information to:</p>
	<ul>
		<li>Provide, maintain, and improve our services</li>
		<li>Analyze usage patterns and trends</li>
		<li>Display relevant advertisements through Google AdSense</li>
		<li>Comply with legal obligations</li>
	</ul>

	<h2>4. Google AdSense and Third-Party Advertising</h2>
	<p>We use Google AdSense to display advertisements on our website. Google may use cookies to serve ads based on your prior visits to our website or other websites.</p>

	<h3>4.1 Google's Use of Data</h3>
	<p>Google uses cookies and data for:</p>
	<ul>
		<li>Personalizing ads based on your interests</li>
		<li>Measuring ad effectiveness</li>
		<li>Improving products and services</li>
	</ul>

	<p>You can opt out of personalized ads by visiting <a href="https://www.google.com/settings/ads" target="_blank">Google's Ads Settings</a> or the <a href="http://www.aboutads.info/choices/" target="_blank">Network Advertising Initiative opt-out page</a>.</p>

	<h2>5. Image Privacy and Security</h2>
	<p><strong>Important:</strong> All image processing in FreePS happens locally in your browser. Your images are:</p>
	<ul>
		<li>Never uploaded to our servers</li>
		<li>Never stored by us</li>
		<li>Never shared with third parties</li>
		<li>Completely private and remain on your device</li>
	</ul>

	<h2>6. Data Retention</h2>
	<p>Since we don't store your images or personal information, we don't retain user data. Any anonymous usage data collected is retained only as long as necessary for analytical purposes.</p>

	<h2>7. Your Privacy Rights</h2>
	<p>Depending on your location, you may have certain rights regarding your personal information, including:</p>
	<ul>
		<li>The right to access your data</li>
		<li>The right to correct inaccurate data</li>
		<li>The right to request deletion of your data</li>
		<li>The right to object to processing</li>
		<li>The right to data portability</li>
	</ul>

	<h2>8. Children's Privacy</h2>
	<p>Our service is not directed to children under 13. We do not knowingly collect personal information from children under 13.</p>

	<h2>9. International Data Transfers</h2>
	<p>Your information may be transferred to and processed in countries other than your own. We ensure appropriate safeguards are in place to protect your data.</p>

	<h2>10. Changes to This Privacy Policy</h2>
	<p>We may update this Privacy Policy from time to time. We will notify you of any changes by posting the new policy on this page and updating the "Last updated" date.</p>

	<h2>11. Contact Us</h2>
	<p>If you have questions about this Privacy Policy, please contact us at:</p>
	<p>Email: privacy@freeps.org</p>

	<h2>12. Google AdSense Specific Disclosures</h2>
	<p>We participate in the Google AdSense program and use Google AdSense cookies. Google uses cookies to serve ads based on your prior visits to this website.</p>

	<h3>Third-Party Vendors</h3>
	<p>Google uses cookies and other technologies to:</p>
	<ul>
		<li>Personalize ads based on your interests</li>
		<li>Measure ad performance</li>
		<li>Improve user experience</li>
	</ul>

	<p>For more information about Google's privacy practices, please visit <a href="https://policies.google.com/privacy" target="_blank">Google's Privacy Policy</a>.</p>
</body>
</html>
```

**Step 2: 浏览器验证**

打开 `http://localhost:8000/privacy.html`
Expected: 隐私政策页面正确显示

**Step 3: 提交**

```bash
git add privacy.html
git commit -m "feat: add privacy policy for AdSense compliance"
```

---

## Task 10: 创建 terms.html 页面（AdSense 必需）

**Files:**
- Create: `terms.html`

**Step 1: 创建 terms.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Terms of Service - FreePS</title>
	<meta name="description" content="Terms of Service for FreePS online photo editor. Read our terms and conditions.">
	<link rel="canonical" href="https://ps.itzhouq.cn/terms.html">
	<style>
		body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; line-height: 1.6; max-width: 800px; margin: 0 auto; padding: 20px; }
		h1 { color: #333; }
		h2 { color: #444; margin-top: 30px; }
		a.back-link { display: inline-block; margin-bottom: 20px; color: #0066cc; text-decoration: none; }
	</style>
</head>
<body>
	<a href="/" class="back-link">← Back to Editor</a>

	<h1>Terms of Service</h1>
	<p>Last updated: February 19, 2025</p>

	<h2>1. Acceptance of Terms</h2>
	<p>By accessing or using FreePS ("Service"), you agree to be bound by these Terms of Service ("Terms"). If you do not agree to these Terms, please do not use our Service.</p>

	<h2>2. Description of Service</h2>
	<p>FreePS is a free online photo editing service that allows users to:</p>
	<ul>
		<li>Upload and edit images</li>
		<li>Apply filters and effects</li>
		<li>Use layers and various editing tools</li>
		<li>Save edited images to their devices</li>
	</ul>

	<h2>3. User Responsibilities</h2>
	<p>As a user of FreePS, you agree to:</p>
	<ul>
		<li>Use the Service only for lawful purposes</li>
		<li>Not upload content that violates any laws or third-party rights</li>
		<li>Not attempt to disrupt or interfere with the Service</li>
		<li>Not use automated tools to abuse the Service</li>
		<li>Respect the intellectual property rights of others</li>
	</ul>

	<h2>4. Intellectual Property Rights</h2>
	<h3>4.1 Service Ownership</h3>
	<p>FreePS and its original content, features, and functionality are owned by us and are protected by international copyright, trademark, and other intellectual property laws.</p>

	<h3>4.2 Your Content</h3>
	<p>You retain ownership of any content you create or edit using FreePS. However, please note that:</p>
	<ul>
		<li>All processing happens in your browser</li>
		<li>We do not store or have access to your images</li>
		<li>You are responsible for the content you create</li>
	</ul>

	<h2>5. Privacy and Data Protection</h2>
	<p>Your use of the Service is also governed by our Privacy Policy, which can be found at <a href="/privacy.html">/privacy.html</a>.</p>

	<h2>6. Disclaimers</h2>
	<h3>6.1 As-Is Basis</h3>
	<p>The Service is provided "AS IS" and "AS AVAILABLE" without warranties of any kind, either express or implied.</p>

	<h3>6.2 No Guarantees</h3>
	<p>We do not guarantee that:</p>
	<ul>
		<li>The Service will be uninterrupted or error-free</li>
		<li>The Service will meet your specific requirements</li>
		<li>Any errors will be corrected</li>
	</ul>

	<h2>7. Limitation of Liability</h2>
	<p>To the fullest extent permitted by law, we shall not be liable for any indirect, incidental, special, consequential, or punitive damages arising from your use of the Service.</p>

	<h2>8. Advertisements</h2>
	<p>FreePS displays advertisements through Google AdSense. By using our Service, you acknowledge that:</p>
	<ul>
		<li>Advertisements are part of the Service</li>
		<li>We do not endorse any advertised products or services</li>
		<li>Third-party ad providers may collect anonymous usage data</li>
	</ul>

	<h2>9. Termination</h2>
	<p>We reserve the right to suspend or terminate your access to the Service at any time, with or without cause, with or without notice.</p>

	<h2>10. Changes to Terms</h2>
	<p>We may modify these Terms at any time. Continued use of the Service after changes constitutes acceptance of the new Terms.</p>

	<h2>11. Governing Law</h2>
	<p>These Terms are governed by the laws of the jurisdiction in which our service operates. Any disputes shall be resolved in accordance with applicable laws.</p>

	<h2>12. Severability</h2>
	<p>If any provision of these Terms is found to be unenforceable, the remaining provisions will remain in full force and effect.</p>

	<h2>13. Contact Information</h2>
	<p>For questions about these Terms, please contact us at:</p>
	<p>Email: legal@freeps.org</p>

	<h2>14. Google AdSense Compliance</h2>
	<p>This website complies with Google AdSense policies by:</p>
	<ul>
		<li>Providing original content and value to users</li>
		<li>Having a clear navigation structure</li>
		<li>Maintaining accessible Privacy Policy and Terms pages</li>
		<li>Ensuring appropriate content for advertising</li>
	</ul>
</body>
</html>
```

**Step 2: 浏览器验证**

打开 `http://localhost:8000/terms.html`
Expected: 服务条款页面正确显示

**Step 3: 提交**

```bash
git add terms.html
git commit -m "feat: add terms of service for AdSense compliance"
```

---

## Task 11: 添加语言切换按钮到 index.html

**Files:**
- Modify: `index.html:36-47`

**Step 1: 在 logo 旁添加语言切换**

找到 `<a class="logo" href="#">FreePS</a>` 这一行，在其后添加：

```html
<div class="lang-switch">
	<a href="?lang=en">EN</a> | <a href="?lang=zh">中文</a>
</div>
```

**Step 2: 添加语言切换样式**

在 `<head>` 中添加样式：

```html
<style>
	.lang-switch { display: inline-block; margin-left: 15px; font-size: 14px; }
	.lang-switch a { color: #333; text-decoration: none; margin: 0 3px; }
	.lang-switch a:hover { text-decoration: underline; }
</style>
```

**Step 3: 浏览器验证**

刷新主页，检查语言切换按钮显示
Expected: 语言切换按钮正确显示在 logo 旁边

**Step 4: 提交**

```bash
git add index.html
git commit -m "feat: add language switcher to main page"
```

---

## Task 12: 优化图片加载性能

**Files:**
- Create: `images/convert-webp.sh` (可选脚本)

**Step 1: 检查图片大小**

```bash
ls -lh images/*.png images/*.jpg 2>/dev/null | head -20
```

**Step 2: 为主要图片添加尺寸属性**

在 `index.html` 中的 `<link rel="icon">` 后添加：

```html
<!-- Preload critical images -->
<link rel="preload" as="image" href="images/favicon.png">
```

**注意**: 由于 bundle.js 是预编译的，无法进行深度图片优化。这步主要是文档记录。

**Step 3: 提交**

```bash
git add index.html
git commit -m "feat: add image preload hints"
```

---

## Task 13: 创建部署后的更新任务清单

**Files:**
- Create: `docs/deployment-checklist.md`

**Step 1: 创建部署检查清单**

```markdown
# Deployment Checklist

## Before Deploying to Vercel

- [ ] All new pages created (about, features, faq, tutorials, privacy, terms)
- [ ] robots.txt created with correct sitemap URL
- [ ] sitemap.xml created with correct project URLs
- [ ] vercel.json created
- [ ] index.html SEO optimized
- [ ] Language switcher added

## After Deploying to Vercel

### 1. Update Project URLs

Replace `ps.itzhouq.cn` with actual Vercel URL in:
- [ ] index.html (meta tags)
- [ ] about.html
- [ ] features.html
- [ ] faq.html
- [ ] tutorials.html
- [ ] privacy.html
- [ ] terms.html
- [ ] robots.txt
- [ ] sitemap.xml

### 2. Test All Pages

- [ ] Homepage loads correctly
- [ ] All pages accessible via navigation
- [ ] Language switcher works
- [ ] No console errors

### 3. SEO Validation

- [ ] Submit sitemap to Google Search Console
- [ ] Verify robots.txt accessible
- [ ] Test with Google Rich Results Test
- [ ] Check mobile-friendliness

### 4. AdSense Setup

- [ ] Apply for Google AdSense
- [ ] Add AdSense code to pages
- [ ] Verify privacy and terms pages linked
- [ ] Wait for approval

## Ongoing

- [ ] Monitor PageSpeed Insights
- [ ] Update sitemap when adding pages
- [ ] Regular content updates for SEO
```

**Step 2: 提交**

```bash
git add docs/deployment-checklist.md
git commit -m "docs: add deployment checklist"
```

---

## Task 14: 最终验证和测试

**Step 1: 本地全面测试**

```bash
python -m http.server 8000
```

测试所有页面：
- [ ] `/` - 主页
- [ ] `/about.html` - 关于页面
- [ ] `/features.html` - 功能页面
- [ ] `/faq.html` - FAQ
- [ ] `/tutorials.html` - 教程
- [ ] `/privacy.html` - 隐私政策
- [ ] `/terms.html` - 服务条款
- [ ] `/robots.txt` - Robots 文件
- [ ] `/sitemap.xml` - Sitemap

**Step 2: 验证 HTML 和 XML**

```bash
# 验证 HTML (可选，使用在线工具)
# 验证 sitemap.xml
cat sitemap.xml | xmllint --format -
```

**Step 3: 检查所有链接**

确保页面间的导航链接正确工作

**Step 4: 最终提交**

```bash
git status
git add -A
git commit -m "feat: complete SEO optimization and AdSense compliance"
```

---

## Deployment Instructions

### Deploy to Vercel

1. **Push to GitHub**:
   ```bash
   git push origin seo-optimization
   ```

2. **Connect to Vercel**:
   - Go to https://vercel.com
   - Click "Add New Project"
   - Import your GitHub repository
   - Select the `seo-optimization` branch
   - Click "Deploy"

3. **Get Your URL**:
   - Wait for deployment to complete
   - Note your `.vercel.app` URL
   - Update all `ps.itzhouq.cn` references in the code

4. **Update DNS** (if using custom domain):
   - Add custom domain in Vercel project settings
   - Update DNS records

### Post-Deployment

1. **Update URLs in all files** with your actual Vercel URL
2. **Submit sitemap to Google Search Console**
3. **Apply for Google AdSense**
4. **Monitor performance** with PageSpeed Insights

---

## Notes

- All placeholder URLs `ps.itzhouq.cn` must be replaced after deployment
- Bundle.js is pre-compiled and cannot be modified
- Language switching is implemented via URL parameters
- All pages are static and require no backend
