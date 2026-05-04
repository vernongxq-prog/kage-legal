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
https://tepgu.github.io/kage-legal/                ← 着陆页
https://tepgu.github.io/kage-legal/privacy.html    ← 隐私政策
https://tepgu.github.io/kage-legal/terms.html      ← 服务条款
```

App 代码里的 `LEGAL_LINKS` 常量已经预先指向上述 URL,部署后无需修改代码。

---

## 🚀 部署步骤(预计 10 分钟)

### 前提条件
- 你已经有 GitHub 账号(用户名:`tepgu`,如果不是请看下面【备选】)
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
# 进入这个目录
cd /Users/yingzigao/Documents/New\ project/app-store-assets/

# 假设你已经把 kage-legal/ 这个文件夹复制到了 app-store-assets 目录下
cd kage-legal

# 初始化 git
git init
git add .
git commit -m "Initial legal pages"

# 关联到 GitHub 远程仓库
git branch -M main
git remote add origin https://github.com/tepgu/kage-legal.git
git push -u origin main
```

> ⚠️ 第一次 push 时,GitHub 可能要求你登录。推荐用 **Personal Access Token** 方式:
> 1. 打开 https://github.com/settings/tokens/new
> 2. 勾选 `repo` 权限
> 3. 生成 token,复制下来作为密码使用

### Step 3 · 启用 GitHub Pages

1. 打开你刚创建的仓库:`https://github.com/tepgu/kage-legal`
2. 点击 **Settings**(右上角)
3. 左侧菜单点 **Pages**
4. **Source** 选择:
   - Branch: `main`
   - Folder: `/ (root)`
5. 点击 **Save**
6. 等待 30 秒 ~ 2 分钟,刷新页面会显示绿色框:
   > ✓ Your site is live at `https://tepgu.github.io/kage-legal/`

### Step 4 · 验证部署

浏览器打开下面三个 URL,确认都能正常打开:

- ✅ https://tepgu.github.io/kage-legal/
- ✅ https://tepgu.github.io/kage-legal/privacy.html
- ✅ https://tepgu.github.io/kage-legal/terms.html

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
| **Privacy Policy URL** | `https://tepgu.github.io/kage-legal/privacy.html` |
| **EULA / Terms URL** (可选) | `https://tepgu.github.io/kage-legal/terms.html` |
| **Support URL** | `https://tepgu.github.io/kage-legal/` 或 `mailto:vernongxq@gmail.com` |

---

## 🔧 如何修改内容

每次修改后:

```bash
cd kage-legal
# 修改 .html 文件
git add .
git commit -m "Update privacy policy date"
git push
```

GitHub Pages 会在 1-2 分钟内自动更新。**注意:CDN 缓存可能导致用户看到旧版,可在 URL 末尾加 `?v=2` 强制刷新。**

---

## 🎯 备选方案

### 备选 1:使用其他 GitHub 用户名
如果你的 GitHub 用户名不是 `tepgu`,把所有 URL 中的 `tepgu` 替换成你的实际用户名。同时**记得更新 App 代码** `japanese-learning-app.jsx` 里的 `LEGAL_LINKS` 常量:

```js
const LEGAL_LINKS = {
  privacy: 'https://你的用户名.github.io/kage-legal/privacy.html',
  terms: 'https://你的用户名.github.io/kage-legal/terms.html',
  support: 'mailto:vernongxq@gmail.com',
};
```

### 备选 2:绑定自定义域名(可选,更专业)
如果你有 `tepgu.com` 这样的域名,可以设置为 `legal.tepgu.com` 指向 GitHub Pages:

1. 在 GitHub Pages 设置页填入 **Custom domain**: `legal.tepgu.com`
2. 在你的域名 DNS 后台添加 CNAME 记录:
   ```
   legal.tepgu.com  CNAME  tepgu.github.io
   ```
3. 等 5-30 分钟 DNS 生效
4. 回到 GitHub Pages 设置勾选 **Enforce HTTPS**

---

## ⚠️ 上线前必检 Checklist

- [ ] **更新日期**:`Last updated` 改为正式提审日期
- [ ] **公司信息**:确认 `tepgu consulting K.K.` 写法与营业執照一致
- [ ] **联系邮箱**:确认 `vernongxq@gmail.com` 是否切换成正式公司邮箱(如有)
- [ ] **价格**:三档订阅的具体价格已与 App Store Connect 后台一致(¥20 / ¥48 / ¥98)
- [ ] **管辖法院**:东京地裁(本人在日本注册公司,无需修改)
- [ ] **真实测试**:用 iPhone 真机访问页面,确认显示正常
- [ ] **无错别字**:三种语言版本都通读一遍

---

## 💡 法律免责声明

⚠️ 本模板基于通用最佳实践与 Apple App Store 审核要求编写,但**不构成法律建议**。

强烈建议在正式提交 App Store 之前:
1. 让懂日本/国际隐私法的律师审阅一遍(尤其是 GDPR 部分)
2. 如果以后接入 Supabase 用户数据库,需要重新修订隐私政策
3. 如果你将来加入广告/分析(Firebase Analytics 等),需要补充相应条款

可以咨询的资源:
- 经济产業省 個人情報保護法ガイドライン (日本)
- iubenda.com / termsfeed.com (在线生成器,可作交叉参考)

---

**Made with ❤️ for ペラペラ日本語**
