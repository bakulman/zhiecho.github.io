 用 Hugo + PaperMod + GitHub Pages 搭建“最强”个人博客

这套方案：极速渲染、外观高级、维护轻，支持暗黑模式、站内搜索、RSS、站点地图、标签/归档、代码高亮、评论和分析。

## 0. 新建仓库
- 在 GitHub 创建公共仓库：`bakulman/bakulman.github.io`

## 1. 添加主题（两种方法二选一）

A) Git Submodule（推荐，后续升级主题最方便）
```bash
# 本地在仓库根目录执行：
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
git submodule update --init --recursive
```

B) 直接拷贝主题
- 打开 https://github.com/adityatelange/hugo-PaperMod → Code → Download ZIP
- 解压得到 `hugo-PaperMod` 文件夹，改名为 `PaperMod`，上传到仓库的 `themes/PaperMod/`

> 注意：如果使用 A) 子模块，工作流中已设置 `submodules: true`，Actions 会自动拉取主题。

## 2. 提交本仓库里的文件
- 把 `hugo.toml`、`.github/workflows/pages-hugo.yml`、`content/`、`static/`、`.gitignore`、`README.md` 等放到仓库并提交
- 首次推送后，GitHub Actions 会自动构建并发布到 GitHub Pages

## 3. 开启 GitHub Pages
- 等待 Actions 成功后，访问仓库的 Settings → Pages，或直接看 Actions 里的 “Deploy to GitHub Pages” 日志里的站点 URL
- 访问：https://bakulman.github.io

## 4. 写文章
- 复制 `content/posts/hello-world/index.md` 改个名字即可
- 文件名建议：`content/posts/YYYY-MM-DD-my-post/index.md`
- 支持 Markdown/代码块/图片（把图片放到同级的 `index.md` 目录里引用 `./image.png`）

## 5. 站内搜索
- 已启用 `outputs.home = ["HTML","RSS","JSON"]`，PaperMod 会生成 `index.json`
- 主题自带 Fuse.js 搜索，顶部有放大镜（首次构建后生效）

## 6. 评论（giscus，可选）
1) 访问 https://giscus.app 按向导绑定你的博客仓库 Discussions
2) 复制生成的参数（repoId、category、categoryId 等）填入 `hugo.toml` 的 `[params.giscus]`
3) 提交后刷新页面即可使用 GitHub 账号评论

## 7. 分析/统计（可选）
- Google Analytics 4：把 `googleAnalytics = "G-XXXXXXXXXX"` 替换为你的 GA4 测量 ID
- 或使用 Plausible/Umami（参考其 Hugo 用法，加自定义脚本到 `layouts/partials/`，PaperMod 也支持自定义头/尾部）

## 8. 自定义域名（可选）
- 在仓库根目录新建 `CNAME` 文件，里面只写你的域名，如：
```
blog.example.com
```
- DNS 添加一条 CNAME：`blog.example.com -> bakulman.github.io`
- Settings → Pages 勾选 Enforce HTTPS

## 9. 本地开发（可选）
- 安装 Hugo Extended：
  - macOS: `brew install hugo`
  - Windows (Scoop): `scoop install hugo-extended`
  - Windows (Chocolatey): `choco install hugo-extended`
- 本地预览：
```bash
hugo server -D
```
- 浏览器打开 http://localhost:1313

## 10. 常见问题
- 页面 404 或不更新：等 1–2 分钟缓存；看 Actions 是否成功；确认主题已存在（子模块/拷贝）
- 文章不显示：确认 front matter 的 `draft: false`，日期不要未来时间
- 子模块没拉到：工作流 `actions/checkout@v4` 要 `submodules: true`（本仓库已配置）
- 私有仓库：私有 Pages 需要付费（Pro/Team/Enterprise）

## 11. 结构说明
```
.
├── content
│   ├── about
│   │   └── index.md
│   └── posts
│       └── hello-world
│           └── index.md
├── themes
│   └── PaperMod   # 主题（子模块或手动复制）
├── static         # 静态资源（favicon、图片等）
├── .github/workflows/pages-hugo.yml
├── hugo.toml
└── README.md
```

祝写博愉快！需要我把这些文件直接提 PR 到你的仓库吗？也可以帮你把第一篇文章内容替换成你想要的主题。
