# 部署指南

## 📦 目录结构

```
web/
├── index.html              # 主页面
├── question-bank.json      # 题库数据（必需）
├── section_map.json        # 章节映射表（可选）
├── _redirects              # Cloudflare Pages 路由配置
├── wrangler.toml          # Cloudflare Workers 配置
├── package.json           # 项目配置
├── .gitignore             # Git 忽略文件
├── .github/
│   └── workflows/
│       └── deploy.yml     # GitHub Actions 自动部署
└── README.md              # 项目说明
```

## 🚀 部署步骤

### 1. 提交到 GitHub

```bash
cd web
git init
git add .
git commit -m "Initial commit: 软考高项智能刷题系统"
git branch -M main
git remote add origin https://github.com/yourusername/question-bank-app.git
git push -u origin main
```

### 2. 部署到 Cloudflare Pages

#### 方式一：通过 Cloudflare Dashboard（推荐）

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. 进入 **Pages** → **Create a project**
3. 选择 **Connect to Git**
4. 选择你的 GitHub 仓库
5. 配置构建设置：
   - **Framework preset**: None
   - **Build command**: (留空)
   - **Build output directory**: `/` (根目录)
6. 点击 **Save and Deploy**

#### 方式二：使用 GitHub Actions（自动部署）

1. 在 GitHub 仓库设置中添加 Secrets：
   - `CLOUDFLARE_API_TOKEN`: 你的 Cloudflare API Token
   - `CLOUDFLARE_ACCOUNT_ID`: 你的 Cloudflare Account ID

2. 获取方式：
   - **API Token**: 
     - 访问 https://dash.cloudflare.com/profile/api-tokens
     - 点击 "Create Token"
     - 选择 "Edit Cloudflare Workers" 模板
     - 或自定义权限：Account → Cloudflare Pages → Edit
   - **Account ID**: 
     - 在 Cloudflare Dashboard 右侧边栏查看

3. 每次推送到 `main` 分支时，GitHub Actions 会自动部署

#### 方式三：使用 Wrangler CLI

```bash
npm install -g wrangler
wrangler login
cd web
wrangler pages deploy .
```

## ✅ 验证部署

部署成功后，访问 Cloudflare Pages 提供的 URL，应该能够：
- 自动加载题库数据
- 正常显示首页
- 可以选择章节开始刷题

## 🔧 故障排查

### 问题：无法加载 question-bank.json

**解决方案**：
1. 检查文件是否存在于仓库根目录
2. 检查文件路径是否正确（相对于 index.html）
3. 查看浏览器控制台的错误信息
4. 确认 Cloudflare Pages 构建输出目录设置正确

### 问题：GitHub Actions 部署失败

**解决方案**：
1. 检查 Secrets 是否正确配置
2. 检查 API Token 权限是否足够
3. 查看 GitHub Actions 日志获取详细错误信息

### 问题：页面显示空白

**解决方案**：
1. 检查浏览器控制台是否有 JavaScript 错误
2. 确认所有文件都已提交到 GitHub
3. 检查 Cloudflare Pages 构建日志

## 📝 注意事项

1. **文件大小**：如果 `question-bank.json` 很大（>10MB），Cloudflare Pages 可能需要更长的构建时间
2. **CORS**：Cloudflare Pages 默认支持 CORS，无需额外配置
3. **缓存**：部署后如果看不到更新，尝试清除浏览器缓存或使用无痕模式

## 🔗 相关链接

- [Cloudflare Pages 文档](https://developers.cloudflare.com/pages/)
- [GitHub Actions 文档](https://docs.github.com/en/actions)
- [Wrangler CLI 文档](https://developers.cloudflare.com/workers/wrangler/)

