# Kage Legal · GitHub Pages 部署指南

ペラペラ日本語(Kage Japanese Shadowing)的法务页面静态站点。

```
kage-legal/
├── index.html       ← 着陆页(三种语言入口)
├── privacy.html     ← 隐私政策(中 / 日 / 英 三语切换)
├── terms.html       ← 服务条款(中 / 日 / 英 三语切换)
└── logo.png         ← App Logo(1024×1024,所有页面引用此文件)
```

⚠️ **`logo.png` 必须和 HTML 一起推到 GitHub Pages**,否则页面上的 Logo 会显示不出来(404)。

部署后访问路径:

```
https://vernongxq-prog.github.io/kage-legal/                ← 着陆页
https://vernongxq-prog.github.io/kage-legal/privacy.html    ← 隐私政策
https://vernongxq-prog.github.io/kage-legal/terms.html      ← 服务条款
```

App 代码里的 `LEGAL_LINKS` 常量已经预先指向上述 URL,部署后无需修改代码。

---

## 🏢 主体身份

- **GitHub 用户名 / 仓库 owner**: `vernongxq-prog`(个人账号,负责代码 + 部署)
- **Apple 开发者账号 / 法人**: `tepgu consulting K.K.`(日本注册公司,负责签约 + 收款 + 法务)
- **联系邮箱**: `vernongxq@gmail.com`

> ⚠️ 注意:`tepgu` 是 Apple 注册公司名,不是 GitHub 用户名。
> 旧版本 README 错把 `tepgu` 当成 GitHub 用户名,所有 `tepgu.github.io` 的链接都是错的,正确的是 `vernongxq-prog.github.io`。

---

## 🚀 部署步骤(预计 10 分钟)

### 前提条件
- GitHub 账号:`vernongxq-prog`
- 电脑装了 Git(macOS 自带)

### Step 1 · 在 GitHub 创建新仓库

1. 打开 https://github.com/new
2. 填写以下信息:
   - **Repository name**: `kage-legal`
   - **Description**: `Legal pages for ペラペラ日本語 (Kage Japanese Shadowing)`
   - **Public** ✅ (必须公开,GitHub Pages 免费版要求)
   - **不要**勾选 "Add a README file"(我们已经有了)
3. 点击 **Create repository**

### Step 2 · 把本地文件推到 GitHub

打开 macOS 终端(Terminal),执行以下命令:

```bash
cd /Users/yingzigao/Documents/NewProject/Kage-Project-Bundle2/kage-legal

# 初始化 git(已经初始化过的可以跳过)
git init -b main
git add index.html privacy.html terms.html logo.png README.md
git commit -m "Initial legal pages"

# 关联到 GitHub 远程仓库
git remote add origin https://github.com/vernongxq-prog/kage-legal.git
git push -u origin main
```

> ⚠️ 第一次 push 时,GitHub 要求登录。HTTPS 推荐用 **Personal Access Token** 方式:
> 1. 打开 https://github.com/settings/tokens/new
> 2. 勾选 `repo` 权限
> 3. 生成 token,复制下来作为密码使用(用户名仍是 `vernongxq-prog`)

### Step 3 · 启用 GitHub Pages

1. 打开你刚创建的仓库:`https://github.com/vernongxq-prog/kage-legal`
2. 点击 **Settings**(右上角)
3. 左侧菜单点 **Pages**
4. **Source** 选择:
   - Branch: `main`
   - Folder: `/ (root)`
5. 点击 **Save**
6. 等待 30 秒 ~ 2 分钟,刷新页面会显示绿色框:
   > ✓ Your site is live at `https://vernongxq-prog.github.io/kage-legal/`

### Step 4 · 验证部署

浏览器打开下面三个 URL,确认都能正常打开:

- ✅ https://vernongxq-prog.github.io/kage-legal/
- ✅ https://vernongxq-prog.github.io/kage-legal/privacy.html
- ✅ https://vernongxq-prog.github.io/kage-legal/terms.html

测试时检查:
- [ ] 顶部三种语言切换 tab 正常工作(中文 / 日本語 / English)
- [ ] 浏览器自动检测语言,中文用户默认中文,日本用户默认日本語
- [ ] 移动端显示正常(用 iPhone 浏览器打开测试)
- [ ] 所有链接跳转正常

---

## 📝 提交 App Store 时怎么用

在 App Store Connect 里填写隐私政策时:

| 字段 | 填什么 |
|---|---|
| **Privacy Policy URL** | `https://vernongxq-prog.github.io/kage-legal/privacy.html` |
| **EULA / Terms URL** (可选) | `https://vernongxq-prog.github.io/kage-legal/terms.html` |
| **Support URL** | `https://vernongxq-prog.github.io/kage-legal/` 或 `mailto:vernongxq@gmail.com` |

---

## 🔧 如何修改内容

每次修改后:

```bash
cd /Users/yingzigao/Documents/NewProject/Kage-Project-Bundle2/kage-legal
# 修改 .html 文件
git add .
git commit -m "Update privacy policy date"
git push
```

GitHub Pages 会在 1-2 分钟内自动更新。**注意:CDN 缓存可能导致用户看到旧版,可在 URL 末尾加 `?v=2` 强制刷新。**

---

## 🎯 备选方案:绑定自定义域名(可选)

如果你有自有域名(比如 `tepgu.co.jp`),可以设置为 `legal.tepgu.co.jp` 指向 GitHub Pages:

1. 在 GitHub Pages 设置页填入 **Custom domain**: `legal.tepgu.co.jp`
2. 在你的域名 DNS 后台添加 CNAME 记录:
   ```
   legal.tepgu.co.jp  CNAME  vernongxq-prog.github.io
   ```
3. 等 5-30 分钟 DNS 生效
4. 回到 GitHub Pages 设置勾选 **Enforce HTTPS**

---

## ⚠️ 上线前必检 Checklist

- [x] **更新日期**:`Last updated` = 2026-05-04
- [x] **公司信息**:`tepgu consulting K.K.` 与日本登记的法人名称一致
- [x] **联系邮箱**:`vernongxq@gmail.com`
- [x] **第三方服务披露**:Supabase / Google Gemini / Microsoft Azure / Jisho.org / Apple / RevenueCat 全部列明
- [x] **录音 + 个人资料 + 邮箱**:已写入数据收集声明
- [ ] **真实测试**:用 iPhone 真机访问页面,确认显示正常
- [ ] **无错别字**:三种语言版本都通读一遍

---

## 💡 法律免责声明

⚠️ 本模板基于通用最佳实践与 Apple App Store 审核要求编写,但**不构成法律建议**。

正式提交 App Store 之前建议:
1. 让懂日本/国际隐私法的律师审阅一遍(尤其是 GDPR 部分)
2. 接入新的第三方服务时需要更新本政策(本版本已涵盖 Supabase / Gemini / Azure)
3. 如果将来加入广告/分析(Firebase Analytics 等),需要补充相应条款

可以咨询的资源:
- 経済産業省 個人情報保護法ガイドライン(日本)
- iubenda.com / termsfeed.com(在线生成器,可作交叉参考)

---

**Made with ❤️ for ペラペラ日本語**
