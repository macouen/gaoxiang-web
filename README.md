# 软考高项智能刷题系统 - 部署版本

这是项目的部署目录，包含所有网站运行所需的文件。

## 📁 目录说明

此目录包含：
- `index.html` - 主页面
- `question-bank.json` - 题库数据（必需）
- `section_map.json` - 章节映射表（可选）
- `_redirects` - Cloudflare Pages 路由配置
- `wrangler.toml` - Cloudflare Workers 配置
- `.github/workflows/deploy.yml` - GitHub Actions 自动部署配置
- `package.json` - 项目配置
- `.gitignore` - Git 忽略文件配置

## 🚀 快速开始

### 本地测试

```bash
# 使用 Python
python3 -m http.server 8000

# 或使用 npm
npm run dev
```

访问 `http://localhost:8000`

### 部署到 Cloudflare Pages

#### 方法一：GitHub 自动部署（推荐）

1. 将整个 `web` 目录推送到 GitHub
2. 在 Cloudflare Dashboard 中连接 GitHub 仓库
3. 配置构建设置：
   - **Framework preset**: None
   - **Build command**: (留空)
   - **Build output directory**: `/` (根目录)
4. 点击 **Save and Deploy**

#### 方法二：使用 Wrangler CLI

```bash
npm install -g wrangler
wrangler login
cd web
wrangler pages deploy .
```

#### 方法三：手动上传

1. 登录 Cloudflare Dashboard
2. 进入 **Pages** → **Create a project** → **Upload assets**
3. 将 `web` 目录打包为 zip 并上传

## 📝 重要提示

- 确保 `question-bank.json` 和 `section_map.json` 与 `index.html` 在同一目录
- 部署后系统会自动加载数据，无需手动操作
- 如果文件很大（>10MB），可能需要更长的部署时间

## 🔧 其他部署方式

### Vercel

```bash
npm i -g vercel
cd web
vercel
```

### Netlify

```bash
npm install -g netlify-cli
cd web
netlify deploy --prod
```

### GitHub Pages

1. 在 GitHub 仓库设置中启用 GitHub Pages
2. 选择 Source: `main` branch `/ (root)`
3. 确保 `web` 目录是仓库根目录

## 📚 更多信息

详细功能说明和部署指南，请查看项目主目录的 README.md
