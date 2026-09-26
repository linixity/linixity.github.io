# 个人学术主页（Quarto · 中英双语）

## 文件夹里都是什么

| 文件 | 作用 |
|---|---|
| `_quarto.yml` | 网站设置：网站标题、导航栏、页脚 |
| `index.qmd`、`research.qmd`、`teaching.qmd`、`code.qmd`、`cv.qmd` | 英文页面：首页、研究、教学、数据与代码、简历 |
| `zh/` | 中文页面，文件名和英文页面一一对应 |
| `images/profile.svg` | 头像占位图 |
| `files/cv-en.pdf`、`files/cv-zh.pdf` | 简历占位文件，直接用你的 PDF 覆盖 |
| `files/papers/` | 放论文 PDF |
| `assets/styles.scss` | 配色和字体（主色在第 3 行） |
| `assets/lang-switch.html` | 中英切换按钮的脚本，不用改 |
| `docs/` | 生成好的网站，**不要手动改**，每次运行 `quarto render` 会自动更新 |

## 第一步：安装 Quarto 并在本地预览

```bash
brew install --cask quarto      # 没有 Homebrew 的话，到 https://quarto.org 下载安装包
cd ~/Desktop/个人主页
quarto preview                  # 浏览器会自动打开，改文件保存后页面自动刷新
```

## 第二步：替换占位内容

1. 全局搜索 `Your Name`、`你的名字`、`[Your University]`、`[你的学校]`、`20XX`，换成你的信息。
2. 换头像：把照片放进 `images/`（例如 `profile.jpg`），再把 `index.qmd` 和 `zh/index.qmd` 里的 `image:` 改成对应的文件名（中文页面要写 `../images/profile.jpg`）。
3. 换简历：用你的 PDF 覆盖 `files/cv-en.pdf` 和 `files/cv-zh.pdf`。
4. 加论文：在 `research.qmd` 里复制一个 `::: {.paper}` 块。论文 PDF 放进 `files/papers/`，英文页链接写 `files/papers/xxx.pdf`，中文页写 `../files/papers/xxx.pdf`。
5. **中英文要同步改**：英文页改了，记得对应的 `zh/` 页面也改。
6. 想新增页面，比如 `blog.qmd`，要同时建 `zh/blog.qmd`，然后在 `_quarto.yml` 的导航栏里把英文、中文两条都加上。

改完运行一次：

```bash
quarto render
```

## 第三步：发布到 GitHub Pages（免费）

1. 注册 GitHub 账号，新建一个仓库，名字**必须**是 `你的用户名.github.io`，设为 Public。
2. 在这个文件夹里上传代码：

   ```bash
   cd ~/Desktop/个人主页
   git init
   git add .
   git commit -m "first version"
   git branch -M main
   git remote add origin https://github.com/你的用户名/你的用户名.github.io.git
   git push -u origin main
   ```

   不熟悉命令行的话，也可以用 GitHub Desktop 客户端把这个文件夹发布上去。
3. 在仓库页面依次点 **Settings → Pages**，把 Source 设为 **Deploy from a branch**，Branch 选 `main`，文件夹选 `/docs`，然后保存。
4. 等一两分钟，打开 `https://你的用户名.github.io` 就能看到网站了。
5. 回到 `_quarto.yml`，把 `site-url` 那一行前面的 `#` 删掉，填上这个网址。

**以后每次更新**：改好文件 → `quarto render` → `git add . && git commit -m "update" && git push`。

## 可选：绑定自己的域名

买一个域名（如 `yourname.com`），在 GitHub 仓库的 Settings → Pages → Custom domain 里填上，再按提示到域名服务商那里添加 DNS 记录。如果国内访问 GitHub Pages 太慢，也可以把同一个仓库接到 Cloudflare Pages 上托管（构建命令留空，输出目录填 `docs`）。
