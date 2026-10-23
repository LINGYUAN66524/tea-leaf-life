# 部署与更新

## 已上线

**https://lingyuan66524.github.io/tea-leaf-life/**

- 仓库：<https://github.com/LINGYUAN66524/tea-leaf-life>
- 托管：GitHub Pages（public 仓库，`main` 分支根目录）
- 更新：改完 `index.html` 或 `assets/` 后

```bash
git add .
git commit -m "update"
git push
```

Pages 通常 30 秒内自动重建，刷新页面即可。

---

## 本地文件

`index.html` 双击能打开；同目录的 `tea-site.zip`（或 `茶文化互动站.zip`）是完整部署包（`index.html` + `assets/` + `.nojekyll`）。

以下方案作为备份/备选。

---

## 方案 A · Netlify Drop

1. 打开 <https://app.netlify.com/drop>
2. 把 `tea-site.zip` 整个拖进页面（**不要只拖 `index.html`**，图片在 `assets/` 里，必须一起上传）
3. 等它解压部署，得到一个 `https://<随机名>.netlify.app` 地址
4. **登录后**可以改站名（Site configuration → Change site name），得到 `https://<你起的名字>.netlify.app`
5. 未登录的临时站点会过期，登录后才是长期站点

适合：先上线看效果、不想碰命令行。

---

## 方案 B · GitHub Pages（长期、免费、可版本管理）

1. 在 GitHub 新建一个 **Public** 仓库，**不要**勾选自动生成 README
2. 在本目录执行（把 `<用户名>` `<仓库名>` 换成你的）：

```bash
git init
git add index.html .nojekyll
git commit -m "tea culture interactive site"
git branch -M main
git remote add origin https://github.com/<用户名>/<仓库名>.git
git push -u origin main
```

3. 仓库 → **Settings → Pages**
   - Source: **Deploy from a branch**
   - Branch: **main**，目录 **/ (root)** → Save
4. 等 1 分钟左右，地址是：

```
https://<用户名>.github.io/<仓库名>/
```

5. 以后更新：改完 `index.html` 后 `git add . && git commit -m "update" && git push`

`.nojekyll` 已经在包里，避免 GitHub 用 Jekyll 处理这个文件。

---

## 方案 C · Cloudflare Pages / Vercel

两个都是「连 Git 仓库 → 自动部署」：

- **Framework preset**：None
- **Build command**：留空
- **Output directory**：`/`（根目录）
- 仓库里只要有 `index.html` 即可

Cloudflare Pages 的免费额度对纯静态站足够，国内访问通常比 GitHub Pages 稳一些。

---

## 方案 D · 自己的服务器 / 虚拟主机

把 `index.html` 传到网站根目录，确保：

- 默认文档包含 `index.html`
- 以 UTF-8 返回（文件本身已是 UTF-8）
- 走 HTTPS（`localStorage` 在 https 下正常）

---

## 上线后自查

- [ ] 用 **https 地址**打开，而不是 `file://`
- [ ] 首屏标题与「开始」按钮正常
- [ ] 首屏背景茶山与毛玻璃卡片正常
- [ ] 五张配图都显示出来，没有裂图
- [ ] 右上角 `EN` / `中文` 能切换，刷新后保持
- [ ] 图鉴从 `0/53` 开始；拖一张茶卡后变 `+3`
- [ ] 手机宽度下不横向滚动
- [ ] 断网后刷新仍能打开（确认没有外部依赖）

> 注意：图鉴进度、错题、称号都存在**访客自己的浏览器**里（localStorage）。
> 换设备、换浏览器不会同步；这是纯静态站的正常行为，不是 bug。
> 如果需要账号、排行榜、后台统计，就要加后端，那是另一套架构。

---

## 自定义域名（可选）

- Netlify：Domain management → Add a domain → 按提示改 DNS
- GitHub Pages：Settings → Pages → Custom domain，并在 DNS 加 CNAME
- 两者都会自动签发 HTTPS 证书
