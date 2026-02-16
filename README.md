# Chenzhou Blog

基于 [Hugo](https://gohugo.io/) 的 GitHub Pages 博客项目。

## 一、本地准备

### 1. 安装 Hugo

**macOS (Homebrew):**
```bash
brew install hugo
```

**或从官网下载：**  
https://gohugo.io/installation/

安装后验证：
```bash
hugo version
```

### 2. 本地运行

```bash
# 在项目根目录
hugo server -D
```

浏览器打开 http://localhost:1313 预览。`-D` 会包含草稿文章。

### 3. 修改博客地址（重要）

在 `hugo.toml` 中把 `baseURL` 改成你的实际地址：

- **项目站**（例如仓库名 `chenzhoublog`）：  
  `https://<你的GitHub用户名>.github.io/chenzhoublog/`
- **用户/组织站**（仓库名为 `用户名.github.io`）：  
  `https://<你的GitHub用户名>.github.io/`

本地预览时也可暂时用 `http://localhost:1313/`。

## 二、推送到 GitHub 并开启 Pages

### 1. 创建仓库并推送

```bash
git init
git add .
git commit -m "Initial commit: Hugo blog for GitHub Pages"
git branch -M main
git remote add origin https://github.com/<你的用户名>/<仓库名>.git
git push -u origin main
```

### 2. 启用 GitHub Pages（使用 Actions）

1. 打开仓库 → **Settings** → **Pages**
2. 在 **Build and deployment** 里：
   - **Source** 选 **GitHub Actions**
3. 无需再选分支或目录，保存即可。

### 3. 自动部署

- 每次推送到 `main` 分支会触发 `.github/workflows/hugo.yaml`
- Actions 会构建 Hugo 并部署到 GitHub Pages
- 在 **Actions** 里可看运行日志，完成后在 Pages 设置里会看到站点地址

## 三、日常写文章

### 新建文章

```bash
hugo new posts/我的新文章.md
```

编辑 `content/posts/我的新文章.md`，把 front matter 里的 `draft: true` 改为 `draft: false` 再推送即可发布。

### 使用主题（可选）

1. 在 [Hugo 主题](https://themes.gohugo.io/) 选一个主题
2. 以 submodule 方式添加（示例：Ananke）：

   ```bash
   git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
   ```

3. 在 `hugo.toml` 中设置：

   ```toml
   theme = "ananke"
   ```

4. 提交并推送：

   ```bash
   git add .gitmodules themes/
   git commit -m "Add theme ananke"
   git push
   ```

## 四、项目结构说明

```
chenzhoublog/
├── .github/workflows/hugo.yaml   # GitHub Actions 构建与部署
├── archetypes/                   # 新内容的模板
├── content/                      # 文章与页面
│   ├── posts/                    # 博客文章
│   ├── about/                    # 关于页
│   └── _index.md                 # 首页内容
├── hugo.toml                     # Hugo 配置
├── public/                       # 构建输出（自动生成，已加入 .gitignore）
└── README.md                     # 本说明
```

构建产物在 `public/`，由 CI 生成并部署，无需提交。

## 五、常见问题

- **站点 404 或空白**  
  检查 Settings → Pages 的 Source 是否为 **GitHub Actions**，并确认 Actions 里最后一次 workflow 已成功完成。

- **样式/主题不生效**  
  若使用 theme submodule，需在 workflow 里已使用 `submodules: recursive`（当前配置已包含）。

- **自定义域名**  
  在仓库 **Settings → Pages → Custom domain** 中填写域名，并按提示配置 DNS 和 HTTPS。

完成以上步骤后，你的 Hugo 博客就会通过 GitHub Pages 自动构建和发布。
# chenzhoublog.github.io
