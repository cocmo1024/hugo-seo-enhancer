# hugo-seo-enhancer

📈 **hugo-seo-enhancer** 是一个结构化、模块化、可复用的 Hugo SEO 增强模块，适用于多站点统一管理和优化 `<head>` 元信息，提升搜索引擎友好度和社交平台展示效果。

## ✨ 功能亮点

- ✅ 完整输出 meta、Open Graph、Twitter Card、JSON-LD
- ✅ 支持 `.Params` 与 `site.Params` 动态配置
- ✅ 无站点耦合，适用于站群、模版系统
- ✅ 提供 `partial` 方式集成，可选自定义重写

---

## 📂 模块结构

```text
layouts/
└── partials/
    └── seo/
        ├── head.html           # ✅ 主入口：统一包含所有子模板
        ├── meta.html           # <meta name="description" ...>、keywords、robots
        ├── canonical.html      # <link rel="canonical" ...>
        ├── opengraph.html      # Open Graph 标签，如 og:title、og:image
        ├── twitter-card.html   # Twitter 卡片标签，如 twitter:title、twitter:image
        └── jsonld.html         # JSON-LD Schema.org 结构化数据（文章/网站）
````

---

## ⚙️ 使用方法

### 1️⃣ 模块引入（推荐方式）

在你的 Hugo 站点的 `config.yaml` 中加入：

```yaml
module:
  imports:
    - path: github.com/your-username/hugo-seo-enhancer
```

> ☑️ 请替换为你实际的 GitHub 路径或本地路径。

---

### 2️⃣ 在 `<head>` 中调用主模板

在 `layouts/_default/baseof.html` 中 `<head>` 区域添加：

```gohtml
{{ partial "seo/head.html" . }}
```

---

### 3️⃣ 配置示例（放在 `config.yaml`）

```yaml
params:
  title: My Site
  description: This is a sample site
  keywords: [ "Hugo", "SEO", "Blog" ]
  images: [ "/images/cover.jpg" ]

  social:
    twitter: mytwitterhandle
```

---

## 🧪 局部引入（可选）

你也可以在页面中选择性引入任意模块：

```gohtml
{{ partial "seo/meta.html" . }}
{{ partial "seo/jsonld.html" . }}
```

---

## 🛡 安全与健壮性说明

本模块已处理：

* ✅ `site.Params.images` / `.Params.images` 的空数组或未定义情况
* ✅ 所有文本内容使用 `plainify` + `safeHTMLAttr` 处理，防止标签注入
* ✅ 所有 URL 使用 `absURL` / `safeURL` 输出
* ✅ 所有数组（如 keywords）使用类型检查防止构建崩溃
