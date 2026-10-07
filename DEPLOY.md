# 部署指南（GitHub + Cloudflare Pages）

本项目是**纯静态**站点（无框架、无构建、无后端），所以 Cloudflare Pages 的构建命令留空即可。

---

## 一、创建 GitHub 仓库

1. 打开 <https://github.com/new>
2. **Repository name** 填：`Salty-Bland Superman`
3. **Public**（公开项目，开源）
4. ⚠️ 下面四个勾选框**全部不要勾**（不要自动加 README / .gitignore / License），
   因为本地已经有了，直接推上去会冲突。
5. 点 **Create repository**

---

## 二、首次推送（用 GitHub Desktop，命令行零基础）

1. 打开 **GitHub Desktop** → 左上角 `File` → `Add local repository…`
2. 选择文件夹：`D:\Salty-Bland Superman`
   - 如果提示「不是 git 仓库」，见下方「手动初始化」小节
3. 左下角/commit 框里填首次提交信息，例如：`init: 咸淡超人 v1`
4. 点 **Commit to main**
5. 右上角 `Publish repository`（或 `Sync`），确认仓库名 `Salty-Bland Superman`
6. 完成后 GitHub 上就有这个仓库了

> 如果 GitHub Desktop 提示需要先 `Create a repository`，
> 直接在它的引导里选 `Create a repository on GitHub`，
> 名称填 `Salty-Bland Superman`，然后照常 Commit + Publish。

### 手动初始化（可选，命令行）

```bash
cd "D:/Salty-Bland Superman"
git init
git add .
git commit -m "init: 咸淡超人 v1"
git branch -M main
git remote add origin https://github.com/<你的用户名>/Salty-Bland Superman.git
git push -u origin main
```

---

## 三、连接 Cloudflare Pages（自动更新）

1. 登录 <https://dash.cloudflare.com>
2. 左侧边栏 → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
3. 选择刚才的 GitHub 仓库 `Salty-Bland Superman` → **Start deployment**

首次连接会弹出授权页（GitHub 授权 / 选择仓库），点确认即可。

4. **构建设置**（关键）：

| 项目 | 填写 |
|---|---|
| 框架预设 | `None` |
| 构建命令 | **留空** |
| 构建输出目录 | `/` |

5. 点 **Save and Deploy**，等 1 分钟就上线了，
   会得到形如 `https://salty-bland-superman.pages.dev` 的地址

> 之后每次本地 `push` 到 main，Cloudflare 会**自动重新部署**，不用再手动操作。

---

## 四、更新日常流程

```bash
cd "D:/Salty-Bland Superman"
# 改完 index.html 后
git add .
git commit -m "描述你的改动"
git push
```
（同样可以用 GitHub Desktop 点点点完成。）

推送后约 1 分钟站点自动更新。

---

## 五、常见问题

**Q: 改了没生效？**
A: Cloudflare Pages → 你的项目 → `Deployments` 看是否触发；没触发就点 `Retry deployment`。

**Q: 徽标（logo）裂了？**
A: 本项目用相对路径 `assets/logo.png`，确认 `assets/` 文件夹一起提交上去了。

**Q: 改了域名？**
A: Workers & Pages → 你的项目 → `Custom domains` → `Set up a custom domain`。