# 个人主页（Personal Homepage）

一个单文件的个人介绍网页，商务专业风，面向开发者 / 求职场景。

- **零依赖**：所有 HTML / CSS / JS 都写在 `index.html` 里，不加载任何外部资源
- **响应式**：桌面端两栏、移动端单栏，带汉堡菜单
- **可直接打印**：`打印简历` 按钮会把页面转成一份干净的 PDF 简历
- **自带交互**：滚动进场动画、技能条进度、导航高亮、点击复制邮箱 / 电话 / 微信

现在页面上是**占位内容**（名字「许若希」以及示例邮箱、手机号、GitHub 链接），按下面第 2 步替换成你自己的信息即可。

> 已经部署在 GitHub Pages：<https://0131-xr.github.io/homepage/>

---

## 1. 本地预览

**最简单**：直接双击 `index.html`，用浏览器打开就能看效果（没有外部依赖，`file://` 下功能完整）。

如果想用本地服务器预览（和线上环境更接近）：

```powershell
# 在这个目录下执行
python -m http.server 8000
# 然后访问 http://localhost:8000
```

> 注意：Windows 自带的 `python` 可能只是应用商店的占位程序。若提示找不到命令，直接用双击打开的方式即可。

---

## 2. 换成你自己的信息

### 2.1 先做全局替换（能省掉 80% 的功夫）

用编辑器的「查找 / 替换」功能，一次性替换这几组：

| 查找 | 替换为 | 出现次数 |
| --- | --- | --- |
| `许若希` | 你的名字 | 9 处（标题、导航、首屏、头像卡、关于我、页脚） |
| `+86 138 0000 0000` | 你的手机号 | 2 处 |
| `xuruoxi_dev` | 你的微信号 | 2 处 |
| `xuruoxi@example.com` | 你的邮箱 | 7 处 |
| `xuruoxi` | 你的英文 ID / GitHub 用户名 | 13 处 |

> 顺序有讲究：**先替换上面三条具体的（手机号、微信号、邮箱），最后再替换 `xuruoxi`**。因为最后这条是前缀，会同时覆盖邮箱和微信号里的 ID 部分。

替换完，再回头逐块微调下面的内容。

### 2.2 逐块编辑对照表

在 `index.html` 里搜 `✏️` 也能直接跳到需要改的地方。

| 板块 | 位置 | 要改什么 |
| --- | --- | --- |
| 浏览器标题 | `<title>` | 显示在标签页上的文字 |
| 右上角头像 | `<div class="avatar">` | 把 `<span aria-hidden="true">许</span>` 换成 `<img src="avatar.jpg" alt="你的名字">`，并把照片放同目录 |
| 首屏 | `<h1>` / `.hero-role` / `.hero-lede` | 名字、职位、自我介绍。一句话简介建议 2～3 行 |
| 首屏状态徽章 | `.eyebrow` / `.status` | 「开放新机会」这类状态；不找工作可以删掉整行 |
| 首屏数字 | `.profile-stats` | 年经验 / 交付项目 / 开源项目 |
| 关于我 | `#about` | 三段自述 + 右侧四个数字（`.fact`） |
| 技能 | `#skills` | 四张 `.skill-card` 里的 `.tag` 标签；`.tag-key` 是深色高亮，用于你最核心的技能 |
| 能力自评 | `.bar-row` | 改 `<span>` 文字和 `data-width="95"` 里的百分比 |
| 项目 | `#projects` | 4 张 `.project` 卡片：标题、描述、`.tag` 技术栈、`.project-flag` 角色、底部链接与数字 |
| 经历 | `#experience` | 3 个 `.tl-item`：左侧时间（`.tl-when`）、公司、`<li>` 要点。教育那条带 `data-kind="edu"`，圆点是灰色 |
| 联系方式 | `#contact` | 4 张 `.contact-card`，**点击复制的内容在 `data-copy` 属性里**，显示文字在 `<b>` 里，两处都要改 |
| 底部 | `.site-footer` | 版权署名 |

### 2.3 几个注意点

- **`data-copy` 和 `<b>` 要一致**：`data-copy="xuruoxi@example.com"` 是复制到剪贴板的值，`<b>xuruoxi@example.com</b>` 是显示的值。
- **favicon 的姓氏**：浏览器标签页图标里的那个字是写死在 `<link rel="icon" href="data:image/svg+xml,...">` 里的 `%E8%AE%B8`（「许」的 UTF-8 百分号编码）。换姓氏时这一处要单独改，不然图标还是旧字。
- **页头方形标记**：导航左侧那个蓝色方块里的字同样要改，位置在 `<span class="brand-mark" ...>` 里。
- **换配色**：只改文件开头 `:root` 里的 `--blue-*` 变量，整站颜色就跟着变。想换成墨绿、紫色都可以。
- **不要的项目**：整块 `<section id="...">` 删掉即可；记得同步删掉 `<nav>` 里对应的 `<a href="#...">`。
- **换字体**：改 `:root` 里的 `--font`。中文建议保留系统字体栈，加载更快。

---

## 3. 部署到 GitHub Pages

### 方式 A：纯网页操作（推荐，不用装任何软件）

1. 打开 [github.com](https://github.com) 并登录（没有账号就注册一个，免费）。
2. 右上角 **+** → **New repository**。
   - **Repository name**：填 `homepage`（或任意名字）。
     - 如果想让网址是 `https://你的用户名.github.io`，仓库名必须**正好**是 `你的用户名.github.io`。
   - 可见性选 **Public**（GitHub Pages 免费版要求公开仓库）。
   - 不要勾选 "Add a README file"。
   - 点 **Create repository**。
3. 在新仓库页面点 **uploading an existing file**（或 `Add file` → `Upload files`）。
4. 把 `index.html` 和 `README.md` 拖进去，点 **Commit changes**。
5. 进入仓库 **Settings** → 左侧 **Pages**。
   - **Source** 选 `Deploy from a branch`
   - **Branch** 选 `main`，目录选 `/ (root)`，点 **Save**。
6. 等 1～2 分钟，刷新该页面，顶部会显示你的网址：
   - 仓库叫 `homepage` → `https://你的用户名.github.io/homepage/`
   - 仓库叫 `你的用户名.github.io` → `https://你的用户名.github.io`

> 以后要更新：在仓库里点开 `index.html` → 铅笔图标编辑 → 提交，站点会自动重新发布。

### 方式 B：用 Git 命令行（适合要频繁改的场景）

这台机器上目前**没有安装 Git**，需要先装：

```powershell
winget install --id Git.Git -e --source winget
```

装完**重开一个终端**，然后：

```powershell
# 1. 首次使用先设置身份（只做一次）
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"

# 2. 进入这个目录
cd C:\Users\xrx20\.zcode\workspace\default

# 3. 初始化并提交
git init -b main
git add .
git commit -m "feat: 个人主页"

# 4. 关联到第 3 步在网页上创建好的仓库（换成你自己的地址）
git remote add origin https://github.com/你的用户名/homepage.git
git push -u origin main
```

推送时如果弹出登录窗口，选择 **Sign in with your browser** 即可。之后再启用 Pages，步骤同方式 A 的第 5 步。

改完内容后更新线上版本：

```powershell
git add .
git commit -m "更新内容"
git push
```

---

## 4. 其他选择

- **自定义域名**：在仓库 Settings → Pages → Custom domain 填写你的域名，然后按提示在域名服务商处添加 CNAME 记录。
- **其他免费托管**：`index.html` 是一个纯静态文件，可以直接拖到 [Vercel](https://vercel.com)、[Netlify](https://netlify.com)、[Cloudflare Pages](https://pages.cloudflare.com)，都支持免费 HTTPS。
- **导出成 PDF 简历**：浏览器打开页面，点右上角 `打印简历` 或页脚的 `打印 / 存为 PDF`，在打印对话框里选择「另存为 PDF」。样式已经为打印优化过，会自动去掉导航栏和按钮。

---

## 文件说明

```
index.html    # 整个网站（结构 + 样式 + 交互都在里面）
README.md     # 本文件
```

图片资源（头像）需要自己放进来，比如 `avatar.jpg` 放在与 `index.html` 同级目录即可。
