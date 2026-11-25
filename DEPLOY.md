# 上架说明

这个目录是三个应用的静态站点版本：三个页面各自带 manifest 和图标，可以安装到桌面或手机主屏，装完能离线打开。

## 目录结构

```
上架站点/
├── index.html                 # 入口
├── brake/  index.html + manifest.webmanifest
├── calm/   index.html + manifest.webmanifest
├── slides/ index.html + manifest.webmanifest
├── assets/ 9 张图标（512 / 192 / 180，三种应用）
└── sw.js                      # 共用离线缓存
```

## 已经做的上架准备

- 每个应用都有独立 `manifest.webmanifest`：名称、短名、主题色、图标、`display: standalone`。
- 每页注册同一个 `sw.js`：先请求网络，成功后缓存；断网时返回缓存的上一次页面。
- 图标三种尺寸，512 同时声明 `any` 和 `maskable`。
- 所有路径都是相对路径，放在子目录（比如 GitHub Pages 的 `/repo/`）也能用。

## 发布到 GitHub Pages

```powershell
cd 上架站点
git init -b main
git add .
git commit -m "上架：三个应用"
gh repo create clone-lab --public --source . --remote origin --push
gh api --method POST repos/<你的账号>/clone-lab/pages --input -   # 输入 {"source":{"branch":"main","path":"/"}}
```

地址是 `https://<你的账号>.github.io/clone-lab/`，三个应用分别是 `/brake/`、`/calm/`、`/slides/`。

## 更新流程

1. 改 `复刻实验室` 里的源文件，再复制到对应目录（或直接改这里的副本）。
2. 把 `sw.js` 第一行 `CACHE = "clone-lab-v1"` 的版本号 +1，否则老用户会继续用缓存。
3. `git add . && git commit -m "update" && git push`，等 Pages 自动构建。

## 装到桌面 / 主屏

- 电脑 Chrome / Edge：打开页面 → 地址栏右侧「安装」→ 独立窗口图标。
- iPhone Safari：分享 → 添加到主屏幕。
- Android Chrome：菜单 → 安装应用 / 添加到主屏幕。

## 还没做的上架

- **应用商店**：App Store / Google Play 需要开发者账号、签名证书和原生壳（Capacitor 打包），这三个现在是 PWA，不是原生包。要上商店可以在这套页面上套 Capacitor，但账号和审核得你来。
- **国内安卓商店**：需要企业开发者资质和备案，个人上不了。
- **数据**：仍然只存在浏览器 localStorage，换设备/换浏览器不同步；要同步得加后端账号体系。
