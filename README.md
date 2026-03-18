# 烛灵·世界志 — GitHub Pages 部署说明

## 文件结构

```
zhuling-worldbuilding/
├── index.html   ← 前端界面
├── data.json    ← 世界观数据
└── README.md
```

---

## 部署步骤

### 1. 创建 GitHub 仓库

1. 登录 GitHub，点击右上角「+」→「New repository」
2. 仓库名填：`zhuling-worldbuilding`（或任意名称）
3. 设为 **Public**（GitHub Pages 免费版要求公开）
4. 点击「Create repository」

### 2. 上传文件

将 `index.html` 和 `data.json` 上传到仓库根目录：

```bash
git init
git add .
git commit -m "init: zhuling worldbuilding"
git remote add origin https://github.com/你的用户名/zhuling-worldbuilding.git
git push -u origin main
```

或直接在 GitHub 网页上「Add file → Upload files」上传两个文件。

### 3. 开启 GitHub Pages

1. 进入仓库 → Settings → Pages
2. Source 选「Deploy from a branch」
3. Branch 选「main」，目录选「/ (root)」
4. 点击 Save

等待约 1 分钟，网站地址为：
```
https://你的用户名.github.io/zhuling-worldbuilding/
```

### 4. 生成 Personal Access Token

1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. 点击「Generate new token (classic)」
3. Note 填：`zhuling-write`
4. 勾选权限：**repo**（完整仓库权限）
5. 点击「Generate token」，**复制保存**（只显示一次）

### 5. 配置网站

打开网站后，点击「⚙ GitHub 配置」：

| 字段 | 填写内容 |
|------|---------|
| 用户名 | 你的 GitHub 用户名 |
| 仓库名 | zhuling-worldbuilding |
| 分支 | main |
| Token | 上一步生成的 token |

点击「保存配置」，配置仅存在你浏览器的 localStorage 中，不会上传。

---

## 工作原理

- **读取**：页面加载时通过 GitHub Contents API 读取 `data.json`
- **写入**：每次保存/编辑/删除操作，自动通过 API 将新 `data.json` commit 到仓库
- **实时同步**：任何人打开网址 → 点「↺ 刷新数据」即可看到最新内容
- **Token 安全**：Token 只存在你本地浏览器 localStorage，其他访客只读不写

---

## 与 Claude 对话配合使用

在 Claude 对话中告知修改内容 → Claude 更新记忆 → 你在网站手动编辑保存 → GitHub 自动存档 → 其他人访问网址即看到最新版本。
